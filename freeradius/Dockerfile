# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
# copied from https://github.com/goofball222/freeradius/blob/main/stable/Dockerfile
    set -x \
    && delgroup ping \
    && addgroup -g $PGID radius \
    && adduser -D -G radius -u $PUID radius \
    && chown -R root:radius /etc/raddb/*.conf /etc/raddb/mods-config/files \
    && apk add -q --no-cache \
        bash freeradius freeradius-radclient tzdata \
#   Alpine FreeRadius unused mods Kitchen Sink list, for future reference 2018-08-19.
#       freeradius-checkrad freeradius-doc freeradius-eap freeradius-krb5 freeradius-ldap \
#       freeradius-lib freeradius-mssql freeradius-mysql freeradius-pam freeradius-perl \
#       freeradius-postgresql freeradius-python freeradius-redis freeradius-rest freeradius-sql \
#       freeradius-sqlite freeradius-unixodbc \
    && rm -rf /tmp/* /var/cache/apk/* \
    && curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

# Copy root filesystem
COPY rootfs /
