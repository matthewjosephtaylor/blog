FROM ubuntu:16.04

RUN apt-get update && apt-get install -y \
	ruby \
	ruby-dev \
	make \
	gcc

RUN gem install \
	bundle \ 
	jekyll \
	minima

COPY src/* /opt/jekyll_compiler/
COPY config/* /opt/jekyll_compiler/config/

ENTRYPOINT ["/opt/jekyll_compiler/compile"]
