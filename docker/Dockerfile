# Stage 1: Hugo build
FROM klakegg/hugo:ext-alpine AS builder

WORKDIR /src
COPY . .
RUN hugo --minify

# Stage 2: Serve with nginx
FROM nginx:alpine
COPY --from=builder /src/public /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

