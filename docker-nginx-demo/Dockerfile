# Immagine di partenza ultraleggera Nginx
FROM nginx:alpine

# Copia i file HTML locali nella cartella predefinita servita da Nginx
COPY index.html /usr/share/nginx/html/index.html

# Espone la porta 80 (valore di documentazione)
EXPOSE 80

# Comando di avvio predefinito per Nginx in foreground
CMD ["nginx", "-g", "daemon off;"]