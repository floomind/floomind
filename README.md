<div align="center">

# 🧠 Floomind

### Agente de bienestar y eficiencia cognitiva con asistente de IA de voz

_Plataforma full-stack (backend + app móvil) con IA conversacional, integración de wearables, aprendizaje federado con privacidad y consentimiento verificable on-chain._

<br/>

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=for-the-badge&logo=dart&logoColor=white)

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)
![Celery](https://img.shields.io/badge/Celery-37814A?style=for-the-badge&logo=celery&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

![Claude](https://img.shields.io/badge/Claude_AI-D97757?style=for-the-badge&logo=anthropic&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white)
![Polygon](https://img.shields.io/badge/Polygon-7B3FE4?style=for-the-badge&logo=polygon&logoColor=white)

</div>

---

## 📋 Descripción

Floomind acompaña al usuario en su bienestar cognitivo: conversa por voz mediante un asistente de IA, integra datos de wearables, genera intervenciones personalizadas (meditación, biofeedback, sueño) y protege la privacidad del usuario mediante cifrado, aprendizaje federado y registro de consentimientos en blockchain.

---

## 📸 Capturas

<div align="center">

### Asistente de voz

<img src="docs/screenshots/01_mind_voz.jpeg" width="240" alt="Pantalla MIND por voz"/>&nbsp;&nbsp;
<img src="docs/screenshots/02_conversacion.jpeg" width="240" alt="Conversación con MIND"/>&nbsp;&nbsp;
<img src="docs/screenshots/03_calibrar_voz.jpeg" width="240" alt="Calibración de voz"/>

_Activación por voz «Hola Mind» · Conversación con el asistente MIND · Clonado de voz on-device_

<br/>

### Home e intervenciones

<img src="docs/screenshots/04_home.jpeg" width="240" alt="Home y acciones rápidas"/>&nbsp;&nbsp;
<img src="docs/screenshots/05_menu.jpeg" width="240" alt="Menú principal"/>&nbsp;&nbsp;
<img src="docs/screenshots/06_wearables.jpeg" width="240" alt="Integración de wearables"/>

_Acciones rápidas (respirar, meditar, biofeedback) · Menú «Tu Floomind» · Integración con wearables (Health Connect, Oura, Fitbit)_

<br/>

### Progreso y perfil

<img src="docs/screenshots/07_patrones.jpeg" width="240" alt="Patrones de pensamiento"/>&nbsp;&nbsp;
<img src="docs/screenshots/08_eficiencia.jpeg" width="240" alt="Métricas de eficiencia cognitiva"/>&nbsp;&nbsp;
<img src="docs/screenshots/09_perfil.jpeg" width="240" alt="Perfil y configuración"/>

_Perfil cognitivo: detección de sesgos (Beck / Kahneman) · Métricas de eficiencia cognitiva · Perfil y configuración de la MIND_

</div>

---

## ✨ Características principales

- 🎙️ **Asistente de IA de voz.** Conversación natural con síntesis de voz, detección de palabra de activación ("Hola Mind") **on-device** y transcripción de voz sin depender de la nube.
- 🧩 **Perfil cognitivo personalizado.** Motor de detección de sesgos y patrones de pensamiento (catastrofización, pensamiento dicotómico, lectura de mente, etc.) basado en marcos de Beck y Kahneman.
- 🗣️ **Voz propia (clonado on-device).** El usuario calibra su voz y las meditaciones suenan con su propia voz.
- ⌚ **Integración con wearables.** Sincronización con Health Connect / Apple Health, Oura Ring y Fitbit (HRV, sueño, actividad) vía OAuth.
- 🧘 **Intervenciones de bienestar.** Respiración, meditaciones en streaming, biofeedback de HRV en tiempo real y módulo de sueño.
- 📊 **Seguimiento de progreso.** Índice de Eficiencia Cognitiva (IEC), estado autonómico, deuda de sueño y tendencias.
- 🔒 **Privacidad por diseño.** Cifrado de datos personales, aprendizaje federado con *Secure Aggregation* y consentimientos registrados en blockchain (Polygon).
- 🔔 **Notificaciones inteligentes.** Push contextuales (FCM) según el momento y el estado del usuario.

---

## 🏗️ Arquitectura

Floomind se compone de dos proyectos:

### ⚙️ Backend — `Python 3.11 + FastAPI`

API modular por capas que orquesta datos, IA, tareas asíncronas y privacidad.

| Capa | Tecnología |
|---|---|
| API | FastAPI, Uvicorn, httpx |
| Bases de datos | PostgreSQL (SQLAlchemy async + Alembic), MongoDB (Motor), Redis, Qdrant (vectorial) |
| IA / NLP | Anthropic (Claude), OpenAI, Transformers, PyTorch, spaCy, scikit-learn |
| Tareas asíncronas | Celery + Flower |
| Aprendizaje federado | Flower (flwr) + Secure Aggregation (PyNaCl / X25519) |
| Blockchain | Web3 + eth-account (consentimientos en Polygon) |
| Seguridad | JWT, passlib/bcrypt, cryptography (AES) |
| Observabilidad / Test | Sentry, Loguru, pytest (81 tests) |

Módulos: **26 routers**, **69 servicios**, **12 tareas Celery**, aprendizaje federado (secure aggregation, PKI cross-device), auditoría, adapters de wearables y contratos Solidity. Documentación de diseño y auditoría de seguridad incluida (**31 documentos**).

> 📂 Detalle completo en [`floomind_ESTRUCTURA.md`](floomind_ESTRUCTURA.md).

### 📱 App — `Flutter (Dart)`

Aplicación móvil multiplataforma con arquitectura **feature-first**.

| Capa | Tecnología |
|---|---|
| Estado y navegación | Riverpod, go_router |
| UI | Google Fonts, flutter_animate, Rive, fl_chart |
| Red y almacenamiento | Dio, flutter_secure_storage, shared_preferences |
| Voz on-device | speech_to_text, sherpa_onnx (wake word), flutter_sound |
| Audio | just_audio, audio_service, audio_session |
| Wearables / salud | health (Health Connect / HealthKit), flutter_web_auth_2 |
| Push | Firebase Core + Messaging, flutter_local_notifications |

Estructura: **core** + **17 features** (onboarding, dashboard, MIND, voz, meditación, wearables, sueño, notificaciones, etc.) + **shared**.

> 📂 Detalle completo en [`floomind_app_ESTRUCTURA.md`](floomind_app_ESTRUCTURA.md).

---

## 🔗 Diagrama de alto nivel

```
┌──────────────┐        HTTPS/REST        ┌───────────────────────────┐
│  App Flutter │  ───────────────────────▶ │      Backend FastAPI      │
│  (móvil)     │ ◀───────────────────────  │                           │
│              │        Push (FCM)         │  ┌─────────────────────┐  │
│  Voz on-dev. │                           │  │ Routers → Services  │  │
│  Wearables   │                           │  └─────────────────────┘  │
└──────────────┘                           │   │        │       │     │
                                           │   ▼        ▼       ▼     │
                                    ┌──────────┐ ┌────────┐ ┌────────┐│
                                    │PostgreSQL│ │MongoDB │ │ Redis  ││
                                    └──────────┘ └────────┘ └────────┘│
                                           │  Qdrant (vectores)       │
                                           │  Celery (tareas async)   │
                                           │  IA: Claude / OpenAI      │
                                           │  Polygon (consentimiento) │
                                           └───────────────────────────┘
```

---

## 🔐 Seguridad y privacidad

- Datos personales cifrados (AES) y autenticación con JWT + bcrypt.
- Aprendizaje federado con *Secure Aggregation*: el modelo aprende sin exponer los datos crudos del usuario.
- Consentimientos registrados de forma verificable en blockchain.
- Las credenciales y claves **no se incluyen** en este repositorio (ver `.env.example`).

---

## 🚦 Estado del proyecto

Proyecto en desarrollo activo. El núcleo está operativo: registro y autenticación, perfil cognitivo, conversación por voz, sincronización de wearables e intervenciones. Roadmap y auditoría de seguridad documentados en `docs/`.

---

## 👤 Autor

**Agustín Formica** — Desarrollo full-stack (backend, app móvil e integración de IA).

[![Email](https://img.shields.io/badge/Email-agustin.formica@gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:agustin.formica@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-agustín--formica-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/agustín-formica)

<!-- Nota: este README es una VITRINA del proyecto. El código completo se mantiene privado; se comparte a pedido en procesos de entrevista. -->
