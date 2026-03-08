# Sistema de Información Escolar (SiE) - Proyecto UAMI

Este repositorio contiene la configuración y despliegue de la infraestructura para una Fábrica de Software basada en **Rocky Linux 10**, ejecutada desde una unidad externa de 320GB.

## 1. Arquitectura del Sistema
* **Servidor:** Rocky Linux 10 (IP: 192.168.100.80).
* **Cliente de Administración:** Windows 10 vía SSH/PKI.
* **Gestión de Identidad:** FreeIPA (Kerberos + LDAP + DNS).
* **Persistencia:** PostgreSQL 15 (Bases de datos: `mayan`, `idempiere`).
* **Contenedores:** Podman (Mayan EDMS + Redis).

## 2. Avances Técnicos
* **Acceso Seguro:** Implementación de túneles SSH con llaves RSA de 4096 bits.
* **Servidor de Identidad:** Despliegue de FreeIPA en modo Standalone con resolución DNS interna.
* **Capa de Datos:** Configuración de PostgreSQL con acceso remoto habilitado mediante `pg_hba.conf` y `listen_addresses`.
* **Orquestación:** Despliegue inicial de microservicios con Podman.

## 3. Desafíos y Mitigaciones
* **Error NXDOMAIN:** Resuelto mediante el ajuste de `resolv.conf` y re-instalación de FreeIPA sin forwarders externos.
* **Conflicto de Puertos (8080/8443):** Mitigado mediante limpieza de procesos huérfanos de Dogtag PKI.
* **Conectividad de Contenedores:** Identificado conflicto de firewall en el loopback de la IP física; solución pendiente mediante red interna de Podman.
