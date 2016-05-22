FROM dockercloud/haproxy:1.4
MAINTAINER Jaynarol <Jaynarol@gmail.com>


# Load ClondFlare IP List
RUN apk add --update curl \
	&& { curl https://www.cloudflare.com/ips-v4 | head -20 && curl https://www.cloudflare.com/ips-v6 | head -20; } > /home/cf-ip \
	&& rm -rf /var/cache/apk/* \
	&& apk del curl


# Fix Real IP for Apache
ENV EXTRA_FRONTEND_SETTINGS_80 acl FROM_CLOUDFLARE src -f /home/cf-ip, http-request set-header X-Real-Ip %[src] if ! FROM_CLOUDFLARE, http-request set-header X-Real-Ip %[req.hdr(CF-Connecting-IP)] if FROM_CLOUDFLARE
ENV EXTRA_FRONTEND_SETTINGS_443 acl FROM_CLOUDFLARE src -f /home/cf-ip, http-request set-header X-Real-Ip %[src] if ! FROM_CLOUDFLARE, http-request set-header X-Real-Ip %[req.hdr(CF-Connecting-IP)] if FROM_CLOUDFLARE