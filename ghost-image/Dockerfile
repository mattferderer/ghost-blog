FROM mhart/alpine-node:4.5

ENV NODE_ENV production
ENV GHOST_PORT 2368

RUN apk --update add unzip curl

USER root
WORKDIR /root/

WORKDIR /var/www/

RUN curl -sSLO https://github.com/mattferderer/ghost-blog/archive/master.zip
RUN unzip ./master.zip -d ghost-git
RUN rm ./master.zip
RUN mv ./ghost-git/ghost-blog-master/ghost-image ./ghost
RUN rm -rf ./ghost-git

WORKDIR /var/www/ghost

RUN addgroup www-data
RUN adduser ghost -G www-data -S /bin/bash
RUN chown ghost:www-data .
RUN chown ghost:www-data /var/www/ghost
RUN chown ghost:www-data -R /var/www/ghost/*
RUN npm install -g pm2
RUN npm install --production
USER ghost


EXPOSE $GHOST_PORT

VOLUME ["/var/www/ghost/content/data"]
VOLUME ["/var/www/ghost/content/themes"]

#CMD ["pm2", "start", "index.js", "--name", "blog", "--no-daemon"]
CMD ["npm", "start"]
