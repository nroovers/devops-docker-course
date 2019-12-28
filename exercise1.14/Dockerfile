FROM ruby:2.6

EXPOSE 3000

RUN apt-get update && apt-get install -y curl wget 
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs

WORKDIR /mydir 
COPY . .
WORKDIR /mydir/rails-example-project

RUN bundle install
RUN rails db:migrate
CMD rails s