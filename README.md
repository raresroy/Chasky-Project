# Chasky – Plataforma de Protección Dinámica (DPSS)
**Detección y Mitigación en Tiempo Real de Phishing y Spam en Correos Electrónicos**

Proyecto académico desarrollado en la Universidad Nacional de Ingeniería (UNI) como parte de la carrera de Ingeniería de Ciberseguridad.

---

## Descripción general

**Chasky** es una **Plataforma de Protección Dinámica (DPSS)** diseñada para detectar phishing y spam en tiempo real en cuentas de Gmail, utilizando **modelos Transformer (DistilBERT)** desplegados sobre infraestructura cloud de bajo costo.

A diferencia de filtros tradicionales basados en reglas o ingeniería manual de características, Chasky emplea **Deep Learning sobre texto crudo**, permitiendo adaptarse a tácticas de ataque modernas y reducir falsos negativos.

El sistema se despliega en una **instancia gratuita de Google Cloud Platform**, opera dentro de un **contenedor Docker** y expone un **dashboard web seguro** mediante **ngrok**.

---

## Enfoque en Seguridad de la Información

El proyecto fue diseñado alineándose conceptualmente con marcos y estándares internacionales de seguridad:

- **NIST Cybersecurity Framework (CSF)**  
  - Identify: identificación de amenazas por análisis de correo
  - Protect: autenticación segura OAuth 2.0
  - Detect: clasificación automática de phishing/spam
  - Respond: alertas inmediatas al usuario
  - Recover: registros y estadísticas para análisis posterior

- **ISO/IEC 27001**  
  - Gestión de riesgos
  - Control de accesos (OAuth 2.0)
  - Protección de información sensible
  - Principios de confidencialidad y mínimo privilegio

- **CIS Critical Security Controls (referencial)**  
  - Monitoreo continuo
  - Protección de cuentas
  - Registro de eventos y actividad

---

## Arquitectura del sistema (resumen)

- **Frontend + Backend:** Flask (dashboard web)
- **Autenticación:** OAuth 2.0 (Gmail API)
- **Motor de análisis:** DistilBERT (cargado una sola vez en memoria)
- **Persistencia:** Archivos JSON locales
- **Infraestructura:**  
  - Google Cloud Platform (instancia e2-micro – always free)
  - Docker
  - Exposición pública mediante túnel HTTPS con ngrok

Arquitectura diseñada siguiendo principios de:
- separación de responsabilidades
- modularidad
- bajo consumo de recursos
- sostenibilidad operativa

---

## Funcionalidades principales

- Autenticación segura con Google (OAuth 2.0)
- Monitoreo continuo de correos entrantes
- Clasificación automática:
  - Legítimo
  - Spam
  - Phishing
- Envío de alertas automáticas por correo
- Dashboard web con:
  - estadísticas en tiempo real
  - historial de correos analizados
  - niveles de riesgo y confianza

---

## Video demostrativo

**Demo funcional del sistema:**  
https://www.youtube.com/watch?v=6v7Bef2CckY

El video muestra:
- autenticación OAuth
- análisis automático de correos
- generación de alertas
- visualización del dashboard

---

## Documentación

Este repositorio incluye documentación técnica y funcional del proyecto:

- Memoria descriptiva completa
- Manual de usuario
- Arquitectura del sistema
- Análisis de riesgos
- Mapeo conceptual a estándares de seguridad

📁 Ver carpeta `/docs`.

---

## Estado del proyecto

- Proyecto **académico funcional**
- Desarrollado y sustentado en la **Universidad Nacional de Ingeniería (UNI)**
- En proceso de mejora y expansión
- Código productivo no expuesto completamente por razones de seguridad

Se incluyen fragmentos representativos y documentación técnica para fines de evaluación.

---

## 👨‍💻 Autores

- Espinoza Soncco, Emerson Aldair  
- Minaya Diaz, Jose Miguel  
- Palacios Yarleque, Jerson Andres  
- Villegas Noblecilla, Luis Javier  

Ingeniería de Ciberseguridad – Universidad Nacional de Ingeniería  
Lima, Perú – 2025