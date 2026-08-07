FROM node:22-alpine AS builder      # ← Stage 1: Build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM nginx:alpine                   # ← Stage 2: Serve
COPY --from=builder /app/dist /usr/share/nginx/html   # ← Copies from Stage 1
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
