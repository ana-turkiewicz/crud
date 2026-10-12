# ETAPA 1 — build: instala o Node, as dependências e gera o dist/
FROM node:22-alpine AS build

WORKDIR /app

# Só os manifestos primeiro: o Docker reaproveita esta camada
# enquanto o package.json e o lock não mudarem.
COPY package.json package-lock.json ./
RUN npm ci

COPY . .
RUN npm run build

# ETAPA 2 — runtime: só o Apache e os arquivos prontos
FROM httpd:alpine

COPY --from=build /app/dist/ /usr/local/apache2/htdocs/
