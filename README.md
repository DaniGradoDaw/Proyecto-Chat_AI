<div align="center">

# Chat AI — Mensajería Segura con IA para Menores

> Aplicación móvil de mensajería para niños con moderación automática por inteligencia artificial y panel de control parental en tiempo real.

[![Angular](https://img.shields.io/badge/Angular-20-DD0031?style=for-the-badge&logo=angular&logoColor=white)](https://angular.dev)
[![Ionic](https://img.shields.io/badge/Ionic-8-3880FF?style=for-the-badge&logo=ionic&logoColor=white)](https://ionicframework.com)
[![Capacitor](https://img.shields.io/badge/Capacitor-8-119EFF?style=for-the-badge&logo=capacitor&logoColor=white)](https://capacitorjs.com)
[![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)](https://firebase.google.com)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-412991?style=for-the-badge&logo=openai&logoColor=white)](https://openai.com)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://typescriptlang.org)

**Disponible para iOS y Android**

</div>

---

## ¿Qué es Chat AI?

Chat AI es una **aplicación móvil** diseñada para que los niños puedan comunicarse entre sí de forma segura. Cada mensaje —texto, audio o imagen— pasa por un **pipeline de inteligencia artificial** antes de ser entregado, detectando automáticamente contenido inapropiado, acoso, información personal sensible o situaciones de riesgo.

Los padres y tutores disponen de un **panel de analíticas avanzado** con el historial de comportamiento de sus hijos, alertas en tiempo real y la posibilidad de revisar los mensajes que el sistema ha bloqueado o marcado para revisión.

---

## Funcionalidades principales

### Para los niños
- Chat en tiempo real: texto, mensajes de audio y fotos
- Chats privados y grupales
- Sistema de solicitud y gestión de amigos
- Avatares personalizados generados con IA (DiceBear + OpenAI)

### Para padres y tutores
- Dashboard de analíticas en tiempo real
- Notificaciones push de alertas (OneSignal)
- Revisión de mensajes bloqueados o en revisión
- Perfil de comportamiento por hijo y por chat
- Nivel de riesgo calculado automáticamente: bajo / medio / alto

### Motor de IA
- Moderación automática con **OpenAI omni-moderation**
- Clasificación de mensajes en categorías: normal, lenguaje ofensivo, acoso escolar, PII, riesgo de grooming, riesgo de autolesión
- Identificación de temas del chat: juegos, escuela, amistad, deportes, conflictos, familia...
- Análisis de rasgos del usuario: amable, empático, neutral, dominante, agresivo...
- Tres pipelines independientes para **texto, audio e imágenes**
- Puntuación de confianza en cada clasificación

---

## Stack tecnológico

| Capa | Tecnología |
|------|------------|
| Frontend / Mobile | Angular 20 + Ionic 8 + Capacitor 8 |
| Lenguaje | TypeScript 5.9 |
| Backend (Serverless) | Firebase Cloud Functions — Node.js 22 |
| Base de datos | Firebase Firestore (NoSQL, tiempo real) |
| Autenticación | Firebase Auth (email/contraseña + anónima) |
| Almacenamiento | Firebase Storage |
| IA y moderación | OpenAI API — GPT-4.1-mini · GPT-4o-mini · omni-moderation |
| Notificaciones push | OneSignal |
| Plataformas | iOS · Android · Web |
| Región cloud | europe-west1 (UE / GDPR) |

---

## Arquitectura

```
┌────────────────────────────────────────────────────────────┐
│                  App Móvil  (Angular + Ionic)               │
│     Vista hijo                     Vista tutor              │
│  Chat · Amigos · Avatares    Dashboard · Analíticas         │
└────────────────────┬───────────────────────────────────────┘
                     │  Firebase SDK (tiempo real)
┌────────────────────▼───────────────────────────────────────┐
│                  Firebase Firestore                         │
│   Usuarios · Hijos · Chats · Messages · Analytics          │
└────────────────────┬───────────────────────────────────────┘
                     │  Triggers automáticos
┌────────────────────▼───────────────────────────────────────┐
│             Cloud Functions  (Node.js 22)                   │
│  ┌───────────────┐  ┌───────────────┐  ┌───────────────┐   │
│  │  Pipeline     │  │  Pipeline     │  │  Pipeline     │   │
│  │   Texto       │  │   Audio       │  │   Imagen      │   │
│  └───────┬───────┘  └───────┬───────┘  └───────┬───────┘   │
└──────────┼──────────────────┼──────────────────┼───────────┘
           │                  │                  │
┌──────────▼──────────────────▼──────────────────▼───────────┐
│                        OpenAI API                           │
│       omni-moderation · GPT-4.1-mini · GPT-4o-mini         │
└─────────────────────────────────────────────────────────────┘
```

Cada mensaje se crea con estado `pending`. Las Cloud Functions lo procesan y cambian su estado a `approved`, `review` o `blocked`. Los clientes nunca pueden aprobar mensajes directamente: las reglas de Firestore lo impiden.

---

## Seguridad y privacidad

- Los niños usan autenticación anónima en Firebase con PIN de 4 dígitos; sus credenciales reales no se exponen en ningún cliente
- Los mensajes nunca llegan al destinatario sin pasar por el pipeline de IA
- Reglas de Firestore estrictas: ningún cliente puede modificar el estado de un mensaje
- Validación de tamaño y tipo en Cloud Storage: máx. 1 MB para imágenes, 20 MB para audio
- Todos los datos almacenados en servidores europeos (GDPR-friendly, región europe-west1)

---

## Taxonomía de moderación

| Tipo | Valores posibles |
|------|-----------------|
| Etiquetas de mensaje | `normal` · `profanity` · `bullying` · `pii_shared` · `grooming_risk` · `self_harm_risk` |
| Temas del chat | `games` · `school` · `friendship` · `family` · `sports` · `humor_memes` · `conflict` · `violence_theme` · `meetup_plans` · `daily_life` · `media_fandom` |
| Rasgos del usuario | `kind` · `empathetic` · `supportive` · `playful` · `neutral` · `dominant` · `aggressive` · `violent` |
| Nivel de riesgo | `low` · `medium` · `high` |

---

## Código fuente

> El código fuente de este proyecto es **privado** por contener configuraciones sensibles de servicios de terceros.
>
> Si estás interesado en el proyecto o en ver una demo, puedes contactarme en: **dani.grado.daw@gmail.com**

---

## Autores

**Daniel** — Desarrollo de Aplicaciones Web (DAW)
**Alfonso** — Desarrollo de Aplicaciones Web (DAW)
**Alejandro** — Programador Senior

[![GitHub](https://img.shields.io/badge/GitHub-DaniGradoDaw-181717?style=flat-square&logo=github)](https://github.com/DaniGradoDaw)
