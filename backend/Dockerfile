FROM node:lts-slim
label maintainer="Patricia Wanjiku <cikunjoroge4@gmail.com>"
WORKDIR /app
COPY package*.json ./
RUN npm install 
COPY . .
EXPOSE $PORT
CMD ["npm","start"]