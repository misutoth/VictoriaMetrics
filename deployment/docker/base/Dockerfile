# See https://medium.com/on-docker/use-multi-stage-builds-to-inject-ca-certs-ad1e8f01de1b
ARG certs_image
ARG root_image
FROM $certs_image as certs

#COPY Tesco_Root_CA.crt /usr/local/share/ca-certificates/certificate.crt
#RUN chmod 644 /usr/local/share/ca-certificates/certificate.crt && update-ca-certificates
COPY Tesco_Root_CA.crt /etc/ssl/certs/tesco-certificate.crt
RUN cat /etc/ssl/certs/tesco-certificate.crt >> /etc/ssl/certs/ca-certificates.crt

RUN apk update && apk upgrade && apk --update --no-cache add ca-certificates

FROM $root_image

COPY --from=certs /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY Tesco_Root_CA.crt /etc/ssl/certs/tesco-certificate.crt
RUN cat /etc/ssl/certs/tesco-certificate.crt >> /etc/ssl/certs/ca-certificates.crt
