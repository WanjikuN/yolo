FROM node:lts-slim as build
label maintainer="Patricia Wanjiku <cikunjoroge4@gmail.com>"
WORKDIR /app
COPY package*.json ./
RUN npm install 
COPY . .
RUN npm run build 
FROM node:alpine as main
COPY --from=build /app /
EXPOSE $PORT
ENV NUXT_HOST=0.0.0.0
ENV NUXT_PORT=$PORT
ENV PROXY_API=$PROXY_API

CMD ["npm","start"]