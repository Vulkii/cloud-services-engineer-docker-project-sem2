FROM node:24-alpine AS builder
ARG NODE_OPTIONS=--openssl-legacy-provider
ENV NODE_OPTIONS=${NODE_OPTIONS}

ARG VUE_APP_API_URL=/api
ENV VUE_APP_API_URL=${VUE_APP_API_URL}

WORKDIR /app
COPY frontend/package*.json ./
RUN npm ci --no-audit --no-fund
COPY frontend/ ./
RUN npm run build

FROM nginxinc/nginx-unprivileged:1.27-alpine
COPY frontend/nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /app/dist/ /usr/share/nginx/html/momo-store/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
