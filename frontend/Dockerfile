# build stage
FROM node:18-alpine AS build
WORKDIR /app

COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build -- --configuration production

# runtime stage
FROM nginx:alpine
COPY --from=build /app/dist/angular-15-crud/ /usr/share/nginx/html/
COPY frontend.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

