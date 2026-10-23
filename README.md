<div align="center">

# 🚦 Pulso Vial · Siniestralidad vial de Cartagena

**Observatorio y centro de gestión de siniestros viales** — mapa de calor, ruta segura, reportes ciudadanos por QR y WhatsApp, despacho de incidentes y predicción de riesgo.

[![Demo](https://img.shields.io/badge/Ver%20demo-accidentalidad--cartagena.vercel.app-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://accidentalidad-cartagena.vercel.app)
[![Portafolio](https://img.shields.io/badge/Detalle%20en%20el%20portafolio-E34F26?style=for-the-badge&logo=astro&logoColor=white)](https://luis-mercado-portfolio.vercel.app/proyectos/pulso-vial)
![Estado](https://img.shields.io/badge/Estado-En%20producci%C3%B3n-2EA44F?style=for-the-badge)

<img src="docs/portada.jpg" alt="Portada de Pulso Vial" width="100%" />

</div>

> 🔒 **Repositorio de presentación.** El código fuente es privado. Aquí encontrarás la descripción, la arquitectura y capturas del sistema. Si quieres conocer el código para un proceso de selección, [escríbeme](mailto:luisda3329@hotmail.com).
>
> Iniciativa independiente: no representa a ninguna entidad oficial.

---

## 📌 Qué es

Plataforma full-stack para gestionar la siniestralidad vial de Cartagena de punta a punta:

- **La ciudadanía** consulta el mapa de calor, compara rutas según su riesgo y reporta siniestros sin crear cuenta (web, código QR del paradero o WhatsApp) con un código de seguimiento.
- **El equipo de operación** recibe esos reportes en una bandeja, abre incidentes, despacha la unidad más cercana y mide el tiempo de llegada.
- **El equipo de análisis** detecta puntos negros, compara años y predice dónde y cuándo es más probable el próximo siniestro.

Es la reescritura completa de una versión anterior (React + FastAPI) como una sola aplicación Next.js, migrando el histórico sin tocar las tablas originales.

## ✨ Funcionalidades

- 🧭 **Ruta segura:** compara alternativas de Mapbox/OSRM y puntúa cada tramo de 100 m según los siniestros cercanos, su gravedad y la hora del viaje.
- 📲 **Reportes ciudadanos** por web, QR de paradero y WhatsApp (webhook con firma verificada), con seguimiento público y detección de duplicados.
- 🚑 **Gestión de incidentes** de la apertura al cierre: unidad más cercana, cronómetro contra el tiempo máximo de llegada y panel de turno en vivo para la sala de control.
- 📍 **Puntos negros** con DBSCAN e índice EPDO; **predicción de riesgo** con un modelo de Poisson explicable, validado con PAI (3,8 veces mejor que el azar).
- 🗓️ **Filtro de tiempo común** en todos los módulos (hoy, 7/30/90 días, años, «hace un año», rangos exactos), compartible por URL.
- 📥 Importación CSV/Excel, exportación, datos abiertos y lectura automática de noticias.
- 🤖 **Asistente IA** con herramientas sobre la base de datos (AI SDK) y modo de respaldo por reglas.
- 🔐 Roles (administración, supervisión, operación, análisis), auditoría y **WCAG 2.2 AA** verificado con axe.

## 🖼️ Capturas

| | |
|---|---|
| <img src="docs/02-consola.jpg" alt="Consola" /> <br/> **Consola:** indicadores del periodo, mapa de calor e incidentes en curso | <img src="docs/03-turno.jpg" alt="Panel de turno" /> <br/> **Panel de turno** en vivo para la sala de control |
| <img src="docs/05-ruta-segura.jpg" alt="Ruta segura" /> <br/> **Ruta segura** con tramos coloreados por riesgo | <img src="docs/04-mapa-calor.jpg" alt="Mapa de calor" /> <br/> **Mapa de calor** con capas de puntos negros, cámaras e incidentes |
| <img src="docs/07-reportes.jpg" alt="Reportes ciudadanos" /> <br/> **Bandeja de reportes** con detección de duplicados | <img src="docs/06-prediccion.jpg" alt="Predicción" /> <br/> **Predicción de riesgo** por hora y zona |
| <img src="docs/08-puntos-negros.jpg" alt="Puntos negros" /> <br/> **Puntos negros** detectados con DBSCAN | <img src="docs/01-portada.jpg" alt="Portada pública" /> <br/> **Portada pública** con las cifras del año |

## 🏗️ Arquitectura

```mermaid
flowchart LR
    subgraph Ciudadania["Ciudadanía (sin cuenta)"]
        W[Web / Mapa de calor]
        QR[QR de paradero]
        WA[WhatsApp]
    end
    subgraph App["Next.js 16 · App Router"]
        P[Portal público]
        C[Consola del equipo<br/>roles y auditoría]
        SA[Server Actions + API]
        IA[Asistente IA<br/>AI SDK + reglas]
        AN[Análisis<br/>DBSCAN · EPDO · Poisson]
    end
    DB[(PostgreSQL · Neon<br/>Drizzle ORM)]
    MAP[Mapbox / OSRM<br/>OpenStreetMap]

    W --> P
    QR --> P
    WA -- webhook firmado --> SA
    P --> SA
    C --> SA
    SA --> DB
    AN --> DB
    IA --> DB
    P --> MAP
    C --> MAP
```

## 🛠️ Stack

![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Drizzle](https://img.shields.io/badge/Drizzle-C5F74F?style=for-the-badge&logo=drizzle&logoColor=black)
![Neon](https://img.shields.io/badge/Neon-00E599?style=for-the-badge&logo=neon&logoColor=black)
![Leaflet](https://img.shields.io/badge/Leaflet-199900?style=for-the-badge&logo=leaflet&logoColor=white)
![Mapbox](https://img.shields.io/badge/Mapbox-000000?style=for-the-badge&logo=mapbox&logoColor=white)
![WhatsApp API](https://img.shields.io/badge/WhatsApp%20API-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)

---

<div align="center">

Hecho por **[Luis Mercado](https://github.com/luismercado29)** · Diseño y desarrollo full-stack · 2026

© 2026 Luis Mercado. Todos los derechos reservados.

</div>
