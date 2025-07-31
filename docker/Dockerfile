# Stage 1: Build Hugo site
FROM klakegg/hugo:ext-alpine AS builder

WORKDIR /site

# Copy source files including theme submodule
COPY . .

# Build site (assumes config file exists)
RUN hugo --minify

# Stage 2: Serve with Nginx
FROM nginx:alpine

# Remove default Nginx index
RUN rm -rf /usr/share/nginx/html/*

# Copy built static site to Nginx directory
COPY --from=builder /site/public /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

