
FROM node:latest AS build
WORKDIR /home/vscode/src
COPY . .

ENV HTTPS_PROXY=http://liudhNB.lan:50000 \
    https_proxy=$HTTPS_PROXY \
    HTTP_RPOXY=$HTTPS_PROXY \
    http_proxy=$HTTPS_PROXY

RUN npm run install:peer-deps && npm run build

FROM build AS development
RUN apt-get update \
    && apt-get install -y git
CMD ["npm", "run", "dev"]

FROM alpine:3.12
EXPOSE 3000
COPY --from=build /home/vscode/src /server
CMD ["/server"]
