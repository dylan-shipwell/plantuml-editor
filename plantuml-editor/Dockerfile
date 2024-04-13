FROM node:12 AS builder

# fetch sources
COPY . /usr/app
#RUN wget "https://github.com/kkeisuke/plantuml-editor/archive/refs/heads/master.zip" && \
#    unzip "master.zip" && \
#    mv plantuml-editor-master /usr/app

WORKDIR /usr/app

# NOTE
#   - tailing "/" is important! (At least for VUE_APP_CDN.)
#   - VUE_APP_SERVER will never used. (Drop it?)
# See PR#19
# https://github.com/kkeisuke/plantuml-editor/pull/19
ARG VUE_APP_URL
ARG VUE_APP_SERVER
ARG VUE_APP_CDN

# build app
RUN npm install && \
    npm run flow-typed && \
    npm run build

FROM node:12 AS builder2

WORKDIR /plantuml-editor-build/
COPY package.json .
COPY package-lock.json .
RUN --mount=type=cache,target=/root/.cache/,rw \
    npm install

COPY .flowconfig .
RUN npm run flow-typed

COPY . .


RUN --mount=type=cache,target=/root/.cache/,rw \
    npm install \
    npm run flow-typed \
    npm run build

# NGINX Alpine as minimal web server
FROM nginx:alpine

WORKDIR /usr/share/nginx/html

COPY --from=builder /usr/app/dist/ .
