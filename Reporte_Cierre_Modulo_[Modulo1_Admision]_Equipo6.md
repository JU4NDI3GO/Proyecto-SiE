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

La ejecución del **Módulo 1: Admisión** se fundamentó en los estándares internacionales de ingeniería de software, asegurando que el diseño no solo sea funcional, sino técnica y legalmente sólido.

### 3.1 Requisitos de Software (Software Requirements KA)
El equipo realizó una fase exhaustiva de elicitación y análisis basada en el **RESUAM**. 
* [cite_start]**Justificación:** Se transformaron reglas de negocio ambiguas en requerimientos técnicos precisos, como la validación de identidad (RENAPO/SAT) y los criterios de evaluación para posgrado[cite: 153, 219, 220]. 
* [cite_start]**Logro:** Definición de un **ID único transversal** que garantiza la integridad del dato durante todo el ciclo de vida del aspirante[cite: 186, 215].

### 3.2 Diseño de Software (Software Design KA)
[cite_start]Se adoptó un enfoque de **Arquitectura Modular** y configuración basada en metadatos[cite: 169, 171].
* [cite_start]**Justificación:** Siguiendo los principios de **alta cohesión y bajo acoplamiento**, se diseñó un "Motor de Convocatorias" y un "Pipeline de Selección" independientes[cite: 176, 179, 221]. 
* [cite_start]**Modelado:** El uso de **UML 2.5** permitió definir entidades complejas como `Cupo`, `Vulnerabilidad` y `ResultadoAdmision`, asegurando que la estructura de datos soporte la lógica de asignación eficiente[cite: 12, 50, 69, 155].

### 3.3 Calidad de Software (Software Quality KA)
[cite_start]La calidad se integró desde el diseño mediante una **Máquina de Estados** robusta[cite: 232].
* [cite_start]**Justificación:** Al definir estados inmutables (ej. REGISTRADO, ADMITIDO, MATRICULADO), se garantiza la trazabilidad y se eliminan estados inválidos en el proceso de inscripción[cite: 84, 94, 96, 234]. 
* [cite_start]**Atributos:** El diseño prioriza la **seguridad** (protección de datos sensibles de vulnerabilidad) y el **rendimiento** para soportar cargas concurrentes durante periodos pico[cite: 50, 139, 247, 250].

### 3.4 Gestión de la Configuración y Procesos (SCM & Process KA)
[cite_start]Se estableció un flujo de trabajo basado en el ciclo de vida del sistema, desde la configuración de la convocatoria hasta la auditoría final[cite: 266].
* [cite_start]**Justificación:** La inclusión de un **Subsistema de Auditoría** inmutable responde a la necesidad de cumplimiento legal y transparencia institucional[cite: 181, 240, 242, 273].
* [cite_start]**Evolución:** El uso de **APIs REST** y un diseño orientado a eventos permite que el sistema sea escalable y se integre con otros módulos como Becas o Finanzas[cite: 255, 258, 275, 276].
