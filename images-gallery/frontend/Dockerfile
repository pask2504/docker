# Stage 1: build della React app
FROM node:20-alpine AS build

# Imposta working directory
WORKDIR /app

# Copia i file package.json e package-lock.json
COPY package*.json ./

# Installa le dipendenze
RUN npm install

# Copia tutto il resto dei file
COPY . .

# Imposta la variabile per OpenSSL legacy
ENV NODE_OPTIONS=--openssl-legacy-provider

# Costruisci l'app
RUN npm run build

# Stage 2: serve l'app con nginx
FROM nginx:alpine

# Copia la build nella cartella di nginx
COPY --from=build /app/build /usr/share/nginx/html

# Copia file di configurazione nginx custom (opzionale)
# COPY nginx.conf /etc/nginx/nginx.conf

# Espone la porta 80
EXPOSE 80

# Avvia nginx
CMD ["nginx", "-g", "daemon off;"]