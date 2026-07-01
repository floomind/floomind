# Floomind — Backend · Estructura del proyecto

Backend de una plataforma de bienestar con asistente de IA de voz, aprendizaje federado y consentimiento on-chain. Construido en **Python 3.11 + FastAPI**, con arquitectura modular por capas.

## Stack principal

- **API:** FastAPI, Uvicorn, httpx
- **Bases de datos:** PostgreSQL (SQLAlchemy async + Alembic), MongoDB (Motor), Redis, Qdrant (vectorial)
- **IA / NLP:** Anthropic (Claude), OpenAI, Transformers, PyTorch, spaCy, scikit-learn
- **Tareas asíncronas:** Celery + Flower
- **Aprendizaje federado:** Flower (flwr) + Secure Aggregation (PyNaCl / X25519)
- **Blockchain:** Web3 + eth-account (contratos de consentimiento en Polygon)
- **Seguridad:** JWT (python-jose), passlib/bcrypt, cryptography
- **Almacenamiento / audio:** boto3 (S3/R2), Pillow, pydub (ffmpeg)
- **Observabilidad:** Sentry, Loguru
- **Testing:** pytest, pytest-asyncio, pytest-cov (81 tests)

## Estructura de carpetas

```
floomind-backend/
├── app/                        # Código de la aplicación
│   ├── main.py                 # Punto de entrada de la API (FastAPI)
│   ├── config.py               # Configuración (lee variables de entorno)
│   ├── core/                   # Núcleo: seguridad, Celery, settings          (6 módulos)
│   ├── database/               # Conexiones a PostgreSQL y MongoDB             (5 módulos)
│   ├── models/                 # Modelos de datos (ORM)
│   ├── schemas/                # Schemas Pydantic (validación de entrada/salida)
│   ├── routers/                # Endpoints de la API REST                      (26 routers)
│   ├── services/               # Lógica de negocio                            (69 servicios)
│   ├── tasks/                  # Tareas asíncronas Celery                     (12 tareas)
│   ├── adapters/               # Integraciones externas (Fitbit, Oura, health SDKs)  (10)
│   ├── middleware/             # Middlewares HTTP (seguridad, contexto)
│   ├── audit/                  # Auditoría y trazabilidad de eventos           (4 módulos)
│   ├── federated/              # Aprendizaje federado + Secure Aggregation    (25 módulos)
│   │   ├── aggregation/        #   Estrategias de agregación de modelos
│   │   ├── secagg/             #   Secure Aggregation (criptografía)
│   │   └── cross_device/       #   PKI, protocolo y transporte entre dispositivos
│   └── utils/                  # Utilidades varias
│
├── contracts/                  # Smart contracts (Solidity) — consentimiento on-chain
│   ├── ConsentRegistry.sol
│   └── FloomindConsent.sol
│
├── tests/                      # Suite de tests (pytest)                       (81 tests)
├── docs/                       # Documentación de diseño y auditoría          (31 documentos)
│   ├── design/                 #   RFCs y diseño de algoritmos
│   ├── handoff/                #   Documentos de traspaso entre sprints
│   ├── security_audit/         #   Modelo de amenazas, inventario cripto, alcance de auditoría
│   └── roadmap_q3_2026/        #   Roadmap y métricas
│
├── Dockerfile                  # Imagen de la aplicación
├── docker-compose.yml          # Orquestación local (API + bases + workers)
├── requirements.txt            # Dependencias Python
├── pytest.ini                  # Configuración de tests
├── .env.example                # Plantilla de variables de entorno (SIN valores reales)
├── .gitignore                  # Archivos excluidos del repositorio
└── README.md                   # Portada del proyecto
```

## Archivos que NO se publican (protegidos por `.gitignore`)

Por seguridad, estos nunca se suben al repositorio:

- `.env` y `.env.*` — credenciales y tokens reales (Claude, OpenAI, MongoDB, Redis, S3/R2, etc.)
- `secrets/` — claves y material criptográfico
- `.venv/`, `venv/`, `__pycache__/` — entorno e intermedios de Python
- `.bak.*` — copias de respaldo de trabajo
- `*.mp3`, `*.wav` — audios de diagnóstico
- `*.log`, `.pytest_cache/`, `.coverage` — logs y artefactos de test

> Se publica únicamente `.env.example` como plantilla, con los **nombres** de las variables pero **sin sus valores**.
