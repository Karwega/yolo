FROM node:alpine

WORKDIR /usr/src/yolo-back

COPY package*.json .

RUN npm install

COPY . .

CMD [ "npm", "run" , "start" ]