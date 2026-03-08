# Capa de Datos (PostgreSQL 15)

## Configuración de Instancia
Se configuró PostgreSQL para permitir conexiones desde la red de contenedores:
- **Archivo `postgresql.conf`:** `listen_addresses = '*'`
- **Archivo `pg_hba.conf`:** Se añadió regla `host all all 0.0.0.0/0 md5`.

## Bases de Datos Creadas
1. `mayan`: Usuario `mayan`, destinada al Gestor Documental.
2. `idempiere`: Usuario `idempiere`, destinada al ERP core.
