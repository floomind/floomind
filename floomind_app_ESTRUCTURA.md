# Floomind — App (Frontend) · Estructura del proyecto

Aplicación móvil multiplataforma del agente de bienestar y eficiencia cognitiva Floomind. Construida en **Flutter (Dart)** con arquitectura **feature-first**, asistente de voz on-device y sincronización con wearables.

## Stack principal

- **Framework:** Flutter (Dart)
- **Estado y navegación:** Riverpod, go_router
- **UI:** Google Fonts, flutter_animate, Rive (animaciones), fl_chart (gráficos)
- **Red y almacenamiento:** Dio (HTTP), flutter_secure_storage, shared_preferences
- **Push notifications:** Firebase Core + Firebase Messaging (FCM), flutter_local_notifications
- **Voz on-device:** speech_to_text (STT nativo), sherpa_onnx (wake word "Hola Mind", offline), flutter_sound (grabación)
- **Audio:** just_audio, audio_service, audio_session (reproductor de meditaciones en streaming)
- **Wearables / salud:** health (Android Health Connect + iOS HealthKit), flutter_web_auth_2 (OAuth)
- **Utilidades:** image_picker, intl, uuid, logger, connectivity_plus, permission_handler

## Estructura de carpetas

```
floomind_app/
├── lib/                        # Código de la app (Dart)
│   ├── main.dart               # Punto de entrada
│   ├── core/                   # Configuración transversal                    (7 archivos)
│   │   ├── constants/          #   Constantes y configuración de entorno
│   │   ├── router/             #   Rutas de navegación (go_router)
│   │   ├── services/           #   Cliente API (Dio), almacenamiento seguro
│   │   └── theme/              #   Tema visual y estilos
│   │
│   ├── features/               # Módulos por funcionalidad                   (56 archivos)
│   │   ├── splash/             #   Pantalla de inicio
│   │   ├── onboarding/         #   Registro, selfie, consentimiento
│   │   ├── home/               #   Pantalla principal
│   │   ├── dashboard/          #   Métricas y gráficos (HRV, sueño, tendencias)
│   │   ├── mind/               #   Avatar MIND
│   │   ├── mind_audio/         #   Voz de la MIND (síntesis + reproducción)
│   │   ├── mind_ambient/       #   Modo ambiente + escucha por voz
│   │   ├── mind_conversation/  #   Conversación con el asistente de IA
│   │   ├── voice_calibration/  #   Calibración de voz + wake word
│   │   ├── meditation/         #   Reproductor de meditaciones (streaming)
│   │   ├── interventions/      #   Intervenciones recomendadas
│   │   ├── sleep/              #   Módulo de sueño
│   │   ├── wearables/          #   Conexión con wearables
│   │   ├── devices/            #   Gestión de dispositivos
│   │   ├── notifications/      #   Notificaciones push (FCM)
│   │   ├── profile/            #   Perfil del usuario
│   │   └── curriculum/         #   Contenido / recorrido del usuario
│   │
│   └── shared/                 # Reutilizable entre features                  (4 archivos)
│       ├── widgets/            #   Componentes UI comunes
│       └── animations/         #   Animaciones compartidas
│
├── assets/                     # Recursos
│   ├── audio/                  #   Sonidos y audios
│   ├── images/                 #   Imágenes
│   ├── rive/                   #   Animaciones Rive
│   └── sherpa_kws/             #   Modelo de wake word on-device
│
├── android/                    # Proyecto nativo Android
├── ios/                        # Proyecto nativo iOS
├── linux/  ·  macos/           # Targets de escritorio
│
├── pubspec.yaml                # Dependencias y configuración del proyecto
├── analysis_options.yaml       # Reglas de análisis estático (linter)
├── .gitignore
└── README.md                   # Portada del proyecto
```

## Archivos que NO se publican (excluir del repositorio)

Por seguridad e higiene del repo, estos no deben subirse:

- `android/app/google-services.json` — **configuración de Firebase con claves** (excluir sí o sí)
- `ios/Runner/GoogleService-Info.plist` — **configuración de Firebase con claves** (excluir sí o sí)
- `.bak.*` — copias de respaldo de trabajo
- `build/`, `.dart_tool/`, `.idea/`, `.flutter-plugins-dependencies` — artefactos generados por Flutter/IDE
- Scripts sueltos de mantenimiento (`*.py`, `*.ps1`) que quedaron en la raíz y no forman parte de la app

> Nota Flutter: el `.gitignore` por defecto **no** excluye los archivos de Firebase. Hay que agregarlos manualmente al `.gitignore` para que no se publiquen.
