FROM node:16-alpine as builder

USER node

RUN mkdir /home/node/app && chmod -R 777 /home/node/app

WORKDIR '/home/node/app'

COPY ./package.json ./

RUN npm install

COPY . .

RUN npm run build

FROM nginx

EXPOSE 3000

COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

COPY --from=builder /home/node/app/build /usr/share/nginx/html