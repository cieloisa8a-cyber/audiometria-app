# 🎧 AudioCheck

Aplicación Android de **tamizaje auditivo orientativo** (audiometría de tonos puros con audífonos cableados).

> ⚠️ **AudioCheck NO es un dispositivo médico ni una herramienta diagnóstica.**
> Sus resultados son orientativos y no reemplazan una evaluación audiológica profesional.

---

## 📁 Estructura del repositorio (monorepo)

```text
audiometria-app/
├── mobile-android/     📱 App nativa: Kotlin + Jetpack Compose + Room + Hilt
├── backend-go/         🐹 API REST en Go (sesiones, resultados, sincronización)
├── analysis-python/    🐍 Servicio de análisis en Python (FastAPI): reportes y estadísticas
├── docs/               📚 Plan Maestro, reparto de tareas y documentación técnica
├── .gitignore
└── README.md
```

| Carpeta | Responsable principal | Tecnología |
|---|---|---|
| `mobile-android/` (motor, datos) | Cielo | Kotlin, AudioTrack, Room |
| `mobile-android/` (pantallas) | Compañero | Jetpack Compose, Material 3 |
| `backend-go/` | Compañero | Go |
| `analysis-python/` | Compañero | Python, FastAPI |
| `docs/` | Ambos | Markdown |

---

## 📚 Documentos clave

- [Plan Maestro](docs/PLAN_MAESTRO.md): fases del proyecto.
- [Reparto de tareas](docs/TAREAS_EQUIPO.md): quién hace qué, y flujo de Git.
- [Contratos compartidos](docs/CONTRATOS.md): modelos e interfaces que conectan el trabajo de los dos.

---

## 🚀 Cómo empezar

```bash
git clone https://github.com/cieloisa8a-cyber/audiometria-app.git
cd audiometria-app
```

- **App Android:** Android Studio → `File > Open` → carpeta `mobile-android`.
- **Backend Go:** ver [backend-go/README.md](backend-go/README.md).
- **Análisis Python:** ver [analysis-python/README.md](analysis-python/README.md).

---

## 👥 Integrantes

- Cielo (`@cieloisa8a-cyber`)
- _(nombre del compañero)_
