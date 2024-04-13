from debian:bookworm
run apt-get update && apt-get install -y nginx ssl-cert
copy nginx.conf /etc/nginx/nginx.conf
copy default /etc/nginx/sites-enabled/default
run rm /var/log/nginx/access.log; ln -s /dev/stdout /var/log/nginx/access.log
run rm /var/log/nginx/error.log; ln -s /dev/stderr /var/log/nginx/error.log
cmd ["sh", "-euc", "nginx -t && nginx -g 'daemon off;'"]
