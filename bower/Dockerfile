FROM node:alpine

RUN apk --no-cache add \
		git \
        perl \
        openssh && \
    npm install -g bower

RUN mkdir /data
VOLUME /data
WORKDIR /data

ENTRYPOINT ["bower", "--allow-root"]
CMD ["update"]
