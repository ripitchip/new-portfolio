# Stage 1: Build Hugo site with nightly version
FROM hugomods/hugo:nightly AS builder

WORKDIR /src

# Copy entire project into container
COPY . .

# Build the site
RUN hugo --minify

# Stage 2: Serve with nginx
FROM nginx:alpine

# Clean default nginx files
RUN rm -rf /usr/share/nginx/html/*

# Copy built site from builder
COPY --from=builder /src/public /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

