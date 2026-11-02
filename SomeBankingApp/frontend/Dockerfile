# --- STAGE 1: Build dell'applicazione Angular ---
FROM node:20-alpine AS build
WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build -- --configuration production

# --- STAGE 2: Servire l'app con Nginx ---
FROM nginx:alpine
# Copia i file dalla cartella 'browser' generata dal nuovo builder di Angular
COPY --from=build /app/dist/SomeBankingFrontend/browser /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]