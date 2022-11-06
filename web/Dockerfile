FROM nginx:alpine
#FROM nginx:stable


COPY nginx.conf /etc/nginx/nginx.conf


ARG CERTBOT_EMAIL=wendellxj@hotmail.com
ARG DOMAIN_LIST=tecws.com.br,api.tecws.com,www.tecws.com.br



RUN   apt-get update 
RUN   apt-get install -y cron certbot python-certbot-nginx bash wget \
      #&& certbot certonly --standalone --agree-tos -m wendellxj@hotmail.com -n -d tecws.com.br,api.tecws.com,www.tecws.com.br \
      && certbot certonly --standalone --agree-tos -m ${CERTBOT_EMAIL} -n -d ${DOMAIN_LIST} \
      && rm -rf /var/lib/apt/lists/* \
      && echo "PATH=$PATH" > /etc/cron.d/certbot-renew  \      
      && echo "@monthly certbot renew --nginx >> /var/log/cron.log 2>&1" >>/etc/cron.d/certbot-renew \
      && crontab /etc/cron.d/certbot-renew



VOLUME /etc/letsencrypt


CMD [ "sh", "-c", "cron && nginx -g 'daemon off;'" ]