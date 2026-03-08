# Módulo 1: Administración - Análisis y Modelado UML

Este documento detalla el análisis del Módulo de Administración para el Sistema de Información Empresarial (SiE), modelado siguiendo los estándares de Enterprise Architect.

## 1. Alcance del Módulo
El Módulo de Administración es el eje central del sistema, encargado de la gestión de la identidad, la configuración global y el control de acceso.

### Funcionalidades Clave:
* **Gestión de Usuarios:** Registro, modificación y baja de cuentas.
* **Control de Acceso (RBAC):** Definición de roles y asignación de privilegios.
* **Configuración del Sistema:** Parámetros globales y variables de entorno.
* **Auditoría y Logs:** Registro de actividades críticas para trazabilidad.

## 2. Diagramas UML (Enterprise Architect)

### A. Diagrama de Casos de Uso
Define las interacciones entre los actores (Administrador, Usuario, Sistema Externo) y las funcionalidades del módulo.
* **Actor Principal:** Administrador del Sistema.
* **Casos de Uso Críticos:** `Gestionar Usuarios`, `Configurar Roles`, `Consultar Logs de Auditoría`.

### B. Diagrama de Clases
Estructura de datos y lógica del negocio.
* **Clases Principales:** `Usuario`, `Rol`, `Permiso`, `Sesión`, `LogAuditoria`.
* **Relaciones:** Un `Usuario` posee uno o varios `Roles`, los cuales contienen múltiples `Permisos` (Relación M:N).

### C. Diagrama de Componentes
Muestra cómo el módulo de Administración se comunica con el resto del SiE.
* **Interfaces:** API de Autenticación, Servicio de Directorio (FreeIPA Integration).

## 3. Matriz de Trazabilidad de Requisitos
| ID | Requisito | Caso de Uso Relacionado | Prioridad |
| :--- | :--- | :--- | :--- |
| R-1.1 | Autenticación centralizada | Login / Validar Credenciales | Alta |
| R-1.2 | Gestión de perfiles | Administrar Perfil de Usuario | Media |
| R-1.3 | Control de sesiones | Monitorear Sesiones Activas | Alta |

## 4. Alineación con Infraestructura (Rocky Linux 10)
El modelado UML del Módulo 1 se implementará utilizando los servicios ya configurados:
- **Backend de Identidad:** Integración con los esquemas LDAP de FreeIPA.
- **Persistencia:** Tablas de administración alojadas en la base de datos `postgresql`.
