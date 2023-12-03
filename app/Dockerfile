FROM node:14

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 8081

CMD ["node", "index.js"]
