FROM nuuve.jfrog.io/nuuve-docker/keycloak:postgresql-1.0.0 as builder

ENV KC_METRICS_ENABLED=false
ENV KC_FEATURES=token-exchange
ENV KC_DB=postgres
ENV KC_HTTPS_PROTOCOLS=TLSv1.2,TLSv1.3


RUN /opt/keycloak/bin/kc.sh build

FROM nuuve.jfrog.io/nuuve-docker/keycloak:postgresql-1.0.0
#COPY --from=builder /opt/keycloak/lib/quarkus/ /opt/keycloak/lib/quarkus/
COPY --from=builder /opt/keycloak/ /opt/keycloak/
WORKDIR /opt/keycloak

# for demonstration purposes only, please make sure to use proper certificates in production instead
RUN keytool -genkeypair \
    -storepass password \
    -storetype PKCS12 \
    -keyalg RSA \
    -keysize 2048 \
    -dname "CN=server" \
    -alias server \
    -ext "SAN:c=DNS:localhost,IP:127.0.0.1" \
    -keystore conf/server.keystore

ENV KEYCLOAK_ADMIN=admin
ENV KEYCLOAK_ADMIN_PASSWORD=change_me
# change these values to point to a running postgres instance
ENV KC_DB_URL=""
ENV KC_DB_SCHEMA=""
ENV KC_DB_USERNAME=""
ENV KC_DB_PASSWORD=""
ENV KC_HOSTNAME=localhost:8443

ENTRYPOINT ["/opt/keycloak/bin/kc.sh", "start"]
