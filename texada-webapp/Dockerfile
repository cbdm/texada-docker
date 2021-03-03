FROM texada:latest

# port that will be used to serve the webapp (internal to docker)
# can be changed as a build argument
ARG TEXADA_PORT=8080
ENV TEXADA_PORT=$TEXADA_PORT

# intall node.js web-app dependencies
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:chris-lea/node.js
RUN add-apt-repository ppa:gophers/go
RUN apt-get update
RUN apt-get install -y nodejs golang git python-software-properties python make

# install the web-app
RUN cd $TEXADA_HOME/www/client && npm install && cd app && ../node_modules/bower/bin/bower install --allow-root

# define the command to run when the image is used
CMD cd $TEXADA_HOME/www && go run $TEXADA_HOME/www/server.go $TEXADA_HOME/texada $TEXADA_PORT

# Remember to expose the port! (docker run -p 127.0.0.1:1234:8080 texada-webapp)
