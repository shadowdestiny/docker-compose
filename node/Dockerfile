FROM ubuntu:xenial
FROM node
RUN apt-get -y update
RUN apt-get --yes install libav-tools
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
COPY package.json /usr/src/app
RUN npm install
COPY . /usr/src/app
RUN npm run build
ENV NODE_ENV production
EXPOSE 8000
CMD ["npm", "run", "start:prod"]