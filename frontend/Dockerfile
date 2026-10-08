# Construye la aplicación y la sirve con nginx.
#
# VITE_API_URL se fija a /api y nginx hace de proxy hacia el backend. Es a
# propósito: las variables VITE_ se incrustan en el bundle en tiempo de
# compilación, así que apuntar directamente al contenedor del backend ataría la
# imagen a un entorno concreto. Con el proxy, la misma imagen sirve en local y
# en producción.
FROM node:22-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
ENV VITE_API_URL=/api
RUN npm run build

FROM nginx:1.27-alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
