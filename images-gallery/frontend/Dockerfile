# Stage 1: build
FROM node:20-alpine AS build

WORKDIR /app

# Copia package.json e package-lock.json (o yarn.lock)
COPY package*.json ./

# Installa le dipendenze
RUN npm install

# Copia tutto il frontend
COPY . .

# Build della app
RUN npm run build

# Stage 2: serve con un web server leggero (nginx)
FROM nginx:alpine

# Copia la build nella cartella di nginx
COPY --from=build /app/build /usr/share/nginx/html

# Copia il file di configurazione nginx personalizzato (opzionale)
# COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 3000

# Avvia nginx
CMD ["nginx", "-g", "daemon off;"]