FROM node:22.15.0-alpine3.20 AS builder
WORKDIR /app
COPY ./ /app
RUN yarn install
RUN yarn build

FROM nginx:1.27.5-alpine3.21
COPY --from=builder /app/build /usr/share/nginx/html
