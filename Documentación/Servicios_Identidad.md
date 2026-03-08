# Gestión de Identidad (FreeIPA)

## Detalles del Dominio
- **Hostname:** `ipa.uami.local`
- **Dominio:** `uami.local`
- **Realm:** `UAMI.LOCAL`

## Notas de Instalación
La instalación se realizó en modo **Standalone** para evitar conflictos con la red local:
- Se omitieron los DNS Forwarders (`--no-forwarders`).
- Se desactivó la configuración de zonas inversas IPv6 (`--no-reverse`).

## Comandos de Verificación
- `sudo ipactl status`: Verifica que los 7 servicios de IPA estén RUNNING.
- `kinit admin`: Valida la obtención de tickets Kerberos.
