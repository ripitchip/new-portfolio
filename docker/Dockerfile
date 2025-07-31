# Stage 1: Build with Hugo
FROM hugomods/hugo:nightly AS builder

WORKDIR /src
COPY . .
RUN hugo --minify

# Stage 2: Serve with Nginx
FROM nginx:alpine

COPY --from=builder /src/public /usr/share/nginx/html

EXPOSE 80

