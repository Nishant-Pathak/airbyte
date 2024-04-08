#FROM ruby:3.0-alpine
FROM nishantpathak/kursaha-base:latest

RUN apk update
RUN apk add --update build-base libffi-dev
RUN apk add ruby ruby-dev
RUN apk add --no-cache ffmpeg

RUN echo 'https://storage.sev.monster/alpine/edge/testing' | tee -a /etc/apk/repositories \
    && wget https://storage.sev.monster/alpine/edge/testing/x86_64/sevmonster-keys-1-r0.apk \
    && apk add --allow-untrusted ./sevmonster-keys-1-r0.apk \
    && apk update \
    && apk add gcompat \
    && rm /lib/ld-linux-x86-64.so.2 \
    && apk add --force-overwrite glibc \
    && apk add glibc-bin

WORKDIR /airbyte

COPY . ./

RUN gem install bundler
RUN bundle install

ENV AIRBYTE_ENTRYPOINT "ruby /airbyte/source.rb"

#ENTRYPOINT ["ruby", "/airbyte/source.rb"]

LABEL io.airbyte.name=airbyte/source-mongodb
LABEL io.airbyte.version=0.3.3
