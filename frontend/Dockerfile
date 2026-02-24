# ---------- build ----------
FROM node:18-alpine AS build

WORKDIR /app
COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

# ---------- nginx ----------
FROM nginx:alpine

# remove default config
RUN rm /etc/nginx/conf.d/default.conf

# copy our config
COPY nginx.conf /etc/nginx/conf.d/default.conf

# copy angular build
RUN rm -rf /usr/share/nginx/html/*
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
