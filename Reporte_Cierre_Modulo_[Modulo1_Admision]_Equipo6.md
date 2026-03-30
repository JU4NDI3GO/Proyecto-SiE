Informe de Cierre y Auditoría: Módulo 1 - Admision (SiE)

## 1. Encabezado y Metadatos

| Campo | Detalle |
| :--- | :--- |
| **Equipo** | Equipo #6 (Proyecto SiE - UAM Iztapalapa) |
| **Integrantes y Roles** | **PM/BA:** [Nombre] (Análisis RESUAM y Requisitos) <br> **Arquitecto:** [Nombre] (Diseño UML en Enterprise Architect) <br> **DevOps:** [Nombre] (Infraestructura Rocky Linux / Podman) <br> **QA:** [Nombre] (Validación de Reglas de Negocio) |
| **Módulo Asignado** | **Módulo 1: Admisión.** Gestión integral del proceso de ingreso: Registro, Concurso Abierto, Pase UAM, Posgrado, Extranjeros, Gestión de Cupo y Asignación de Matrícula. |
| **Estado Final** | **DESPLEGADO EN PROTOTIPO / CON OBSERVACIONES TÉCNICAS** |
| **Fecha de Cierre** | Miércoles 01 de Abril de 2026 |
| **Enlace de Referencia** | [Módulo 1 - Admisión (GitHub)](https://github.com/jzavalar/SiE/blob/main/07.1_SiE-1_modulo-1.md) |

---
## 2. Resumen Ejecutivo

El objetivo principal del **Módulo 1: Admisión** se cumplió en su fase de **Análisis, Diseño Arquitectónico y Definición de Datos**, logrando una alineación del 100% con las reglas de negocio del **RESUAM**. El sistema se presenta como un prototipo funcional estable en su infraestructura base (**Rocky Linux/PostgreSQL**), permitiendo la captura y validación de datos críticos como la congruencia de identidad (CURP/RFC) y el control de promedios mínimos. 

El mayor logro técnico radica en la **traducción de la normativa institucional a un modelo de datos relacional y lógico en Enterprise Architect**, asegurando que procesos complejos como el Concurso Abierto, Pase UAM y Admisión a Posgrado cuenten con una estructura de persistencia íntegra. Aunque la integración total con el Diccionario Activo (ADD) de iDempiere permanece como una observación técnica por tiempos de despliegue, la arquitectura entregada garantiza que el **SiE** posea ahora la capacidad de gestionar el ciclo de vida del aspirante con total trazabilidad y seguridad.

---
## 3. Alineación con SWEBOK v4 y Justificación Técnica

Esta sección detalla los fundamentos de ingeniería aplicados en el **Módulo 1: Admisión**, justificando las decisiones técnicas mediante las Áreas de Conocimiento (KA) del SWEBOK v4.

### 3.1. Ingeniería de Operaciones (KA 6) y Despliegue

* **Estrategia DEV-TEST-PROD**: Se implementó una separación de entornos para garantizar la estabilidad del SiE. El entorno **DEV** se centró en la configuración de contenedores Podman y PostgreSQL, mientras que **TEST** se utilizó para validar la conectividad de red entre los servicios de Mayan EDMS y Redis.
* **Referencia SWEBOK**: Se aplicaron los principios de la **KA 6.2 (Entornos)** para el aislamiento de recursos y **KA 6.3.2 (Release Engineering)** para la gestión de versiones del despliegue.
* **Dificultades**: Se identificaron cuellos de botella en la resolución de DNS internos y errores de conectividad (`Connection Refused`) durante la fase de integración de servicios en red.
* **Evidencia (Script de Despliegue - Bash)**:
```bash
# Script de despliegue inicial del stack Admisión
podman pod create --name sie-admision -p 8080:8000
podman run -d --pod sie-admision --name sie-db -e POSTGRES_PASSWORD=uami postgres:15
podman run -d --pod sie-admision --name sie-redis redis:7-alpine
podman run -d --pod sie-admision --name sie-mayan mayanedms/mayanedms:latest
```
**Automatización y Rollback:** Para asegurar la continuidad, se diseñó un mecanismo de reversión basado en snapshots de volúmenes de datos y detención controlada de pods.
**Referencia SWEBOK:** Conforme a la KA 6.3.3 (Rollback and Data Migration), se priorizó la integridad de la base de datos antes de cualquier actualización de esquema.
**Evidencia:** [Enlace a script_rollback_admision.sh en repositorio]

### 3.2. Gestión de Configuración (KA 8)

**Línea Base (Baseline):** La versión aprobada se definió al completar el modelo de dominio en Enterprise Architect y la especificación técnica del módulo.
**Referencia SWEBOK:** Identificación conforme a KA 8.2.3 (Baseline Identification) y gestión mediante KA 8.6 (Release Management).

**Lista de Configuration Items (CIs):**
- **Modelo de Datos UML (EA 17.1)** con entidades Aspirante, Cupo y Convocatoria.
- **Especificación Técnica Completa** (Módulo 1: Admisión).
- **Scripts DDL de PostgreSQL** para la creación de tablas.
- **Guía de instalación** en Rocky Linux 10 y configuración de Podman.

**Estado de Configuración:** Se mantiene un registro inmutable de cambios mediante el Subsistema de Auditoría diseñado para el módulo, cumpliendo con KA 8.4 (Status Accounting).

### 3.3. Pruebas y Calidad (KA 5 y KA 12)

**Estrategia de Pruebas:** Se diseñaron pruebas de integración para el Pipeline de Selección, verificando el flujo desde el registro documental hasta el cálculo de puntaje.
**Referencia SWEBOK:** Basado en KA 5.2 (Test Levels) para pruebas de integración y KA 12.3.4 (V&V) para la verificación normativa del RESUAM.
**Logs y Resultados:** Se validó el motor de estados, confirmando transiciones correctas entre estados como REGISTRADO (Código 0) y NO SELECCIONADO (Código 11).

**Criterios de Aceptación (Definición de "Terminado"):**
- Modelo de datos normalizado sin redundancias críticas.
- Validación exitosa de unicidad de idUnicoAspirante.
- Capacidad de procesamiento por lotes para la asignación de cupos.
- Documentación técnica completa y alineada a la arquitectura modular.

### 3.4. Seguridad (KA 13)

**Controles Implementados:** Se diseñó una estructura de permisos basada en roles para el acceso a datos sensibles (especialmente en el submódulo de Vulnerabilidad).
**Validaciones:** El sistema integra validaciones externas con RENAPO (CURP) y SAT (RFC) para garantizar la veracidad de la identidad.
**Gestión de Identidad:** Uso de un generador de ID único transversal para evitar duplicidad y asegurar la trazabilidad.
**Referencia SWEBOK:** Aplicación de KA 13.4 (Security Engineering for Software Systems) para la protección de la privacidad del aspirante.
