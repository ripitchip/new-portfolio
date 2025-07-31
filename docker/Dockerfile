# Stage 1: Build Hugo site
FROM hugomods/hugo:nightly AS builder

WORKDIR /src
COPY . .
RUN hugo --minify

# Stage 2: Serve with nginx
FROM nginx:alpine

RUN rm -rf /usr/share/nginx/html/*
COPY --from=builder /src/public /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

