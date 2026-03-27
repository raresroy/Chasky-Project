# Chasky — Plataforma de Detección de Phishing en Gmail

> Detección y mitigación en tiempo real de phishing y spam en correos electrónicos usando DistilBERT (Transformers) sobre infraestructura GCP de bajo costo.

Proyecto académico desarrollado en la **Universidad Nacional de Ingeniería (UNI)** — Ingeniería de Ciberseguridad · Lima, Perú · 2025

---

## ¿Qué es Chasky?

**Chasky** es una plataforma web de protección dinámica (DPSS – *Dynamic Phishing Shield System*) que monitorea automáticamente una cuenta de Gmail, analiza cada correo entrante con inteligencia artificial y alerta al usuario en tiempo real cuando detecta un mensaje peligroso.

A diferencia de los filtros tradicionales basados en reglas fijas, Chasky usa **DistilBERT**, un modelo de lenguaje pre-entrenado de la familia Transformer, que opera directamente sobre el texto del correo sin necesidad de ingeniería manual de características. Esto le permite adaptarse mejor a tácticas de ataque modernas.

El sistema corre en una **VM gratuita de Google Cloud Platform**, dentro de un contenedor Docker, y es accesible desde cualquier dispositivo a través de un túnel HTTPS seguro con ngrok.

---

## Demo en video

▶️ **[Ver demostración funcional en YouTube](https://www.youtube.com/watch?v=6v7Bef2CckY)**

El video muestra la autenticación OAuth, el análisis automático de correos, la generación de alertas y la visualización del dashboard en tiempo real.

---

## Funcionalidades

- **Autenticación segura con Google** — OAuth 2.0, sin almacenar contraseñas
- **Monitoreo continuo 24/7** — no necesitas mantener el navegador abierto
- **Clasificación automática** de cada correo en tres categorías:
  - ✅ Legítimo
  - ⚠️ Spam
  - 🚨 Phishing
- **Alertas automáticas por correo** cuando se detecta phishing con más del 90 % de confianza (llegan en menos de 10 segundos)
- **Dashboard web en tiempo real** con:
  - Métricas de detección (amenazas, spam, correos seguros)
  - Gráfico de clasificación general
  - Tendencia de ataques en el tiempo
  - Flujo de análisis en vivo con nivel de riesgo (1/5 a 5/5) y confianza del modelo

---

## Arquitectura

El sistema sigue el modelo arquitectónico **4+1** y se organiza en los siguientes módulos:

```
┌──────────────────────────────────────────────────────────┐
│               Google Cloud Platform (GCP)                 │
│                                                          │
│   ┌──────────────────────────────────────────────────┐   │
│   │              Docker: App Chasky / Flask           │   │
│   │                                                  │   │
│   │   ┌────────────┐    ┌──────────────────────┐    │   │
│   │   │  OAuth 2.0  │    │  DistilBERT (local)  │    │   │
│   │   │   Manager   │    │  EmailAnalyzer        │    │   │
│   │   └────────────┘    └──────────────────────┘    │   │
│   │                                                  │   │
│   │   ┌────────────────┐   ┌───────────────────┐    │   │
│   │   │  Gmail Monitor  │   │  Notificaciones   │    │   │
│   │   │  (background)  │   │  (alertas correo) │    │   │
│   │   └────────────────┘   └───────────────────┘    │   │
│   │                                                  │   │
│   │   ┌───────────────────────────────────────────┐  │   │
│   │   │  Dashboard Flask + HTML (JSON polling)    │  │   │
│   │   └───────────────────────────────────────────┘  │   │
│   └──────────────────────────────────────────────────┘   │
│                         ▲                                │
└─────────────────────────│────────────────────────────────┘
                          │ HTTPS (ngrok tunnel)
                          │
                    ┌─────┴──────┐
                    │  Usuario   │
                    │  (browser) │
                    └────────────┘
```

| Capa | Tecnología |
|------|-----------|
| Backend / Frontend | Python 3.10+ · Flask · HTML/JS |
| Modelo IA | DistilBERT (Hugging Face Transformers) |
| Autenticación | OAuth 2.0 — Gmail API |
| Persistencia | Archivos JSON locales (`analisis.json`, `resumen.json`) |
| Infraestructura | GCP e2-micro (always free) · Docker · ngrok |

---

## Cómo funciona

1. El usuario accede a la web y hace clic en **"Iniciar sesión con Google"**
2. Autoriza el acceso mediante OAuth 2.0 (Chasky solo solicita permisos de lectura y envío de alertas)
3. Un hilo en segundo plano consulta la bandeja de Gmail cada 8–10 segundos
4. Cada correo nuevo es procesado por DistilBERT: extracción de asunto + cuerpo → clasificación
5. El resultado se guarda en JSON y se muestra en el dashboard (se actualiza automáticamente cada 8 segundos)
6. Si se detecta phishing con confianza > 90 %, se envía una alerta de seguridad al correo del usuario

> Chasky **nunca guarda tu contraseña** y puedes revocar el acceso en cualquier momento desde tu cuenta de Google.

---

## Niveles de riesgo

| Nivel | Etiqueta | Significado | ¿Genera alerta? |
|-------|----------|-------------|-----------------|
| 1/5 | Muy Seguro | Correo 100 % legítimo (universidad, contacto conocido) | No |
| 2/5 | Bajo Riesgo | Promociones, newsletters | No |
| 3/5 | Moderado | Cadenas, ofertas dudosas | No |
| 4/5 | Alto Riesgo | Posible phishing, enlaces sospechosos | Sí |
| 5/5 | Crítico | Phishing casi seguro ("Tu cuenta será bloqueada") | Sí (urgente) |

---

## Requisitos para ejecutar

- Python 3.10+
- Docker
- Credenciales OAuth 2.0 configuradas en Google Cloud Console (Gmail API habilitada)
- Cuenta ngrok (para exposición pública)
- Mínimo 2 GB de RAM

> El proyecto puede desplegarse gratuitamente en la instancia **e2-micro always-free** de GCP. El costo operativo estimado es inferior a **1 USD/mes**.

---

## Documentación del repositorio

```
/docs
├── Memoria_Descriptiva_Chasky.pdf    # Arquitectura y requerimientos completos
├── Manual_Usuario_Chasky.pdf         # Guía de uso paso a paso
├── Arquitectura_Chasky.pdf           # Diagramas arquitectónicos (modelo 4+1)
└── Presentacion_Chasky.pdf           # Presentación del proyecto
```

---

## Estado del proyecto

- ✅ Proyecto académico funcional, desarrollado y sustentado en la UNI
- 🔄 En proceso de mejora y expansión
- 🔒 El código productivo completo no está expuesto públicamente por razones de seguridad

El repositorio incluye fragmentos representativos, documentación técnica completa y el manual de usuario para fines de evaluación y referencia.

---

## 👨‍💻 Autores

| Nombre | Correo |
|--------|--------|
| Espinoza Soncco, Emerson Aldair | emerson.espinoza@uni.pe |
| Minaya Diaz, Jose Miguel | miguel.minaya.d@uni.pe |
| Palacios Yarleque, Jerson Andres | jerson.palacios.y@uni.pe |
| Villegas Noblecilla, Luis Javier | luis.villegas.n@uni.pe |

**Ingeniería de Ciberseguridad — Universidad Nacional de Ingeniería**
Lima, Perú · 2025