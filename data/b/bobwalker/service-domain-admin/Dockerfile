FROM ruby:2.4.1  
  
RUN apt-get update -qq && apt-get install -y build-essential  
  
# for postgres  
RUN apt-get install -y libpq-dev  
  
# for nokogiri  
RUN apt-get install -y libxml2-dev libxslt1-dev  
  
# for a JS runtime  
RUN apt-get install -y nodejs  
  
ENV APP_HOME /myapp  
RUN mkdir $APP_HOME  
WORKDIR $APP_HOME  
ADD Gemfile* $APP_HOME/  
RUN bundle install  
  
ADD . $APP_HOME  
CMD bin/rails server \--port 3000 --binding 0.0.0.0  
EXPOSE 3000  

