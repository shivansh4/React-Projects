# Stage 1: Build the React app
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package.json and package-lock.json/yarn.lock
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .
ENV NODE_OPTIONS=--openssl-legacy-provider

# Build the React app for production
RUN npm run build

# Stage 2: Serve using Nginx
FROM nginx:alpine

# Remove default Nginx static assets
RUN rm -rf /usr/share/nginx/html/*

# Copy the React build output to Nginx's public folder
COPY --from=builder /app/build /usr/share/nginx/html

# Copy a custom nginx config file if needed (optional)
# COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 3000
EXPOSE 3000

CMD ["nginx", "-g", "daemon off;"]
