FROM node:alpine

RUN mkdir -p /usr/src/node-app && chown -R node:node /usr/src/node-app

WORKDIR /usr/src/node-app

COPY package.json  ./

CMD yarn dev

RUN yarn install 

COPY --chown=node:node . .

EXPOSE 3000
