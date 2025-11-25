FROM node:20-alpine AS builder

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm install

COPY . .

RUN npx @tanstack/router-cli generate

RUN npm run build


FROM nginx:alpine

# 📌 Ajout obligatoire pour charger ta config personnalisée
COPY nginx.conf /etc/nginx/conf.d/default.conf

# 📌 Copier le build React
COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 5173

CMD ["nginx", "-g", "daemon off;"]
