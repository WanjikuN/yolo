FROM node:lts-slim
label maintainer="Patricia Wanjiku <cikunjoroge4@gmail.com>"
WORKDIR /app
COPY backend/package.json ./
RUN npm install 
COPY backend/ .
EXPOSE $PORT
CMD ["npm","start"]