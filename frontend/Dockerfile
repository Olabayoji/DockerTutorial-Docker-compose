FROM node

WORKDIR /app

COPY package.json .

RUN npm install

EXPOSE 8100

COPY . .

CMD [ "npm" , "start"]