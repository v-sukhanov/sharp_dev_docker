FROM node:alpine as builder
RUN apk update && apk add --no-cache make git
WORKDIR /app
COPY package*.json /app/
RUN cd /app && npm set progress=false && npm install
COPY .  /app
RUN cd /app && npm run build -- --configuration=production
FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*
COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /app/dist/docker-test /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
