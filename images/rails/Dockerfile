FROM ruby:3.1.2-alpine3.16

WORKDIR /usr/src/app

COPY Gemfile* ./

RUN apk update && \
    apk add --virtual build-dependencies build-base && \
    apk add --no-cache gcc wget git gcompat tzdata && \
    apk add --no-cache ruby-rdoc libpq-dev postgresql-libs && \
    apk add --update-cache --no-cache --virtual .build-deps g++ make postgresql-dev

RUN bundle add solargraph
RUN bundle add yard

RUN bundle install --jobs 4 --retry 3 \
    && rm -rf /usr/local/bundle/cache/*.gem \
    && find /usr/local/bundle/gems/ -name "*.c" -delete \
    && find /usr/local/bundle/gems/ -name "*.o" -delete \
    && apk --purge del .build-deps

RUN bundle exec yard gems

RUN solargraph bundle
RUN solargraph download-core

CMD [ "solargraph", "socket", "--host=0.0.0.0", "--port=7658" ]
