FROM node:alpine
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
LABEL authors="dimitriaigle"
CMD ["npm", "start"]