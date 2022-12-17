FROM node:16-alpine as build

WORKDIR /frontend

COPY . .

RUN npm ci 

RUN npm run build

FROM nginx:1.21.0-alpine as production

ENV NODE_ENV production

COPY --from=build /frontend/build /usr/share/nginx/html

RUN rm /etc/nginx/conf.d/default.conf

COPY nginx/nginx.conf /etc/nginx/conf.d

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]