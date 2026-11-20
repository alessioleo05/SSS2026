FROM nginx:alpine

# Rimuovo la configurazione di default 
RUN rm -f /etc/nginx/conf.d/default.conf

# Copio il file di configurazione personalizzato per il reverse proxy
COPY nginx.conf /etc/nginx/nginx.conf

# Documenta la porta HTTP su cui ascolta Nginx
EXPOSE 80

# Avvio Nginx in primo piano 
CMD ["nginx", "-g", "daemon off;"]