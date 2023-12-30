FROM node:alpine

WORKDIR /app

COPY ./package.json .

RUN npm install

COPY . .

ENV PATH="$PATH:/app/node_modules/.bin"

CMD ["npm", "start"]