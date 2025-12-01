# frontend/Dockerfile
# build stage
FROM node:18-alpine AS build
WORKDIR /app

# copy only package files first for layer caching
COPY package*.json ./
RUN npm ci --silent

COPY . .
# build Angular app into /app/dist/
RUN npm run build -- --configuration production

# runtime stage (nginx)
FROM nginx:alpine
# copy built app into nginx html
COPY --from=build /app/dist/angular-15-crud/ /usr/share/nginx/html/
# nginx config (we'll copy frontend.conf)
COPY frontend.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
