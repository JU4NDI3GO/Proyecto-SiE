# Orquestación de Aplicaciones (Podman)

## Stack Tecnológico
- **Motor:** Podman (Rootless/Native Rocky Linux 10).
- **Broker:** Redis 7 (Imagen: `docker.io/library/redis:7-alpine`).
- **Aplicación:** Mayan EDMS (Imagen: `docker.io/mayanedms/mayanedms:latest`).

## Estado Actual e Incidencias
- Los contenedores están creados y en ejecución (`Up`).
- **Incidencia detectada:** Error de conectividad 111 (Connection Refused) entre Mayan y Redis.
- **Próximo paso:** Implementar una red virtual de Podman (`podman network create`) para resolver nombres de contenedores internamente.
