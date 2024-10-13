FROM alpine:3.20

# Install dnsmasq
RUN apk --no-cache add dnsmasq=2.90-r3

EXPOSE 53

# Start dnsmasq, write log items to container console
ENTRYPOINT ["dnsmasq", "-k"]