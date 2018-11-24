FROM ruby:2.5.3-slim-stretch

ENV LANG C.UTF-8

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
      build-essential \
      default-libmysqlclient-dev \
      curl \
      wget \
      vim \
      gnupg \
 && apt-get clean \
 && rm -r /var/lib/apt/lists/*

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
 && apt-get install -y --no-install-recommends nodejs

RUN wget https://github.com/yarnpkg/yarn/releases/download/v1.7.0/yarn_1.7.0_all.deb \
 && dpkg -i yarn_1.7.0_all.deb

WORKDIR /myapp

COPY Gemfile  .
COPY Gemfile.lock .
RUN bundle install

COPY package.json .
COPY yarn.lock .
RUN yarn install

COPY . .
