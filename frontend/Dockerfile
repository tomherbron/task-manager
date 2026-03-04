FROM node:20-alpine AS build

WORKDIR /app

# Copy frontend source
COPY frontend/ .

RUN npm install && npm run build

FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*

# Copy frontend files to nginx folder
COPY --from=build /app /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
