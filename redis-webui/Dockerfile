FROM erikdubbelboer/phpredisadmin:latest

ENV ADMIN_USER eledock
ENV ADMIN_PASS eledock
ENV REDIS_1_HOST redis
ENV REDIS_1_PORT 6379

EXPOSE 8081
ENTRYPOINT [ "tini", "--", "php", "-S", "0.0.0.0:8081" ]
