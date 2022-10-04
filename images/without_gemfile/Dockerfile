FROM ruby:3.1.2-alpine3.16

WORKDIR /usr/src/app

COPY . .

RUN apk add --no-cache gcompat tzdata && \
    apk add --update-cache --no-cache --virtual .build-deps g++ make

RUN gem install bundler
RUN gem install solargraph rubocop

RUN solargraph bundle
RUN solargraph download-core

CMD [ "solargraph", "socket", "--host=0.0.0.0", "--port=7658" ]
