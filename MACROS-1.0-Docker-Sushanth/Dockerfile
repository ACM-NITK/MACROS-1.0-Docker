FROM ruby:2.6.1 
RUN apt-get update && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt-get install -y nodejs \
                       default-libmysqlclient-dev \
                       --no-install-recommends
RUN mkdir /app
WORKDIR /app
RUN gem install bundler -v 2.1.4
ADD ./Gemfile /app/Gemfile
ADD ./Gemfile.lock /app/Gemfile.lock
RUN bundle install
COPY . /app

RUN chmod +x bin/entry
RUN chmod +x lib/wait-for-it.sh
EXPOSE 3000

ENTRYPOINT [ "lib/wait-for-it.sh", "db:3306", "--strict", "--timeout=600", "--", "bin/entry" ]
CMD /bin/sh; \
    bin/rails s -p 3000 -b 0.0.0.0;