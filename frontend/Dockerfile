FROM node:20-alpine AS build

WORKDIR /app

ARG HTTP_PROXY
ARG HTTPS_PROXY

ENV HTTP_PROXY="${HTTP_PROXY}"
ENV HTTPS_PROXY="${HTTPS_PROXY}"

# Copy package.json and package-lock.json first
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy all other frontend source code
COPY . .

# ----------------------------
# Serve with nginx
FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*

# Copy built frontend from the build stage
COPY --from=build /app /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
