FROM centos:7

ARG GO_VERSION='1.14.4'
ARG REVEL_VERSION='0.21.0'

# yum インストール
RUN yum -y update && \
    yum clean all

RUN yum install -y \
        wget \
        git \
        make \
        cmake \
        sudo \
        unzip \
        gcc

RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
ENV LANG="ja_JP.UTF-8" \
    LANGUAGE="ja_JP:ja" \
    LC_ALL="ja_JP.UTF-8"

WORKDIR /opt/go_lang/

RUN wget https://storage.googleapis.com/golang/go${GO_VERSION}.linux-amd64.tar.gz
RUN tar zxvf go${GO_VERSION}.linux-amd64.tar.gz

RUN mv go .go
RUN mkdir go

## 環境変数
ENV GOROOT /opt/go_lang/.go
ENV GOPATH /opt/go_lang/go
ENV PATH $GOROOT/bin:$GOPATH/bin:$PATH

RUN source $HOME/.bashrc && \
    go get github.com/revel/revel && \
    go get github.com/revel/cmd/revel

RUN cd /opt/go_lang/go/src/github.com/revel/revel && \
    git checkout release/v${REVEL_VERSION}
# --- revelインストール END ---

# --- デバッグツールインストール
RUN go get github.com/labstack/echo && \
    go get github.com/labstack/echo/middleware && \
    go get github.com/derekparker/delve/cmd/dlv

RUN mkdir /var/log/code

## 作業ディレクトリへ移動
WORKDIR /opt/go_lang/go/src

# nginxインストール
COPY ./nginx/nginx.repo /etc/yum.repos.d/nginx.repo
RUN yum install -y nginx
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
RUN systemctl enable nginx

CMD ["/sbin/init"]
