FROM node:24-alpine AS builder
ARG NODE_OPTIONS=--openssl-legacy-provider
ENV NODE_OPTIONS=${NODE_OPTIONS}

WORKDIR /app

COPY frontend/package*.json ./
RUN npm ci --no-audit --no-fund

COPY frontend/ ./
RUN npm run build

FROM nginx:1.29.1-alpine

COPY frontend/nginx.conf /etc/nginx/nginx.conf

COPY --from=builder /app/dist/ /usr/share/nginx/html/

RUN chown -R nginx:nginx /usr/share/nginx

USER nginx

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
