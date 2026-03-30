# Arquitectura de Red y Acceso

## Topología de Hardware
- **Servidor (Host):** Disco Externo 320GB con Rocky Linux 10.
- **Cliente:** Laptop con Windows 10 (Terminal/PowerShell).

## Configuración de Acceso SSH
Se implementó seguridad mediante llaves asimétricas (PKI):
1. **Generación:** RSA 4096 bits en el cliente.
2. **Autorización:** Llave pública alojada en `~/.ssh/authorized_keys` del servidor.
3. **Resultado:** Acceso remoto seguro sin intercambio de contraseñas.

## Puertos Habilitados (Firewalld)
| Servicio | Puerto | Protocolo |
| :--- | :--- | :--- |
| SSH | 22 | TCP |
| PostgreSQL | 5432 | TCP |
| Redis | 6379 | TCP |
| Mayan EDMS | 8000 | TCP |
