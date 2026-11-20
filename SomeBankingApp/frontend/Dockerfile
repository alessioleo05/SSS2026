# --- STAGE 1: Build dell'applicazione Angular ---
FROM node:20-alpine AS build

RUN apk add --no-cache git

WORKDIR /app

RUN git clone https://github.com/mmenapace/SomeBankingApp.git .

WORKDIR /app/frontend

RUN npm install

# Sostituisce l'URL del backend con /api in tutti i sorgenti
RUN node -e "const fs=require('fs'),path=require('path');let n=0;(function w(d){for(const e of fs.readdirSync(d,{withFileTypes:true})){const p=path.join(d,e.name);if(e.isDirectory()){w(p);continue}if(!/\.(ts|js|html)$/.test(e.name))continue;const s=fs.readFileSync(p,'utf8');const t=s.replace(/https?:\/\/(127\.0\.0\.1|localhost):8000/g,'/api');if(t!==s){fs.writeFileSync(p,t);console.log('patched',p);n++}}})('src');console.log('files patched:',n);if(!n)process.exit(1)"

RUN npm run build -- --configuration production

# La build fallisce se nel bundle resta ancora l'URL vecchio
RUN ! grep -rE "127\.0\.0\.1:8000|localhost:8000" dist/

# --- STAGE 2: Servire l'app con Nginx ---
FROM nginx:alpine

COPY --from=build /app/frontend/dist/SomeBankingFrontend/browser /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]