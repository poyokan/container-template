FROM node:16.15-alpine

WORKDIR /react-project/

COPY package*.json /react-project/

RUN npm install

COPY ./ /react-project/

EXPOSE 3000

CMD ["npm", "start"]