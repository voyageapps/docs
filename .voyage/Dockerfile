FROM node as build

WORKDIR /app

RUN npm i -g retypeapp

COPY . .

RUN retype build

FROM nginx

COPY --from=build /app/.retype/ /usr/share/nginx/html
