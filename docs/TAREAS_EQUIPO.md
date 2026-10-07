# 👥 Reparto de tareas — AudioCheck

Dos personas, dos frentes, **cero pisarse**.

| | 🪟 Cielo (Windows) | 🍎 Compañero (Mac) |
|---|---|---|
| **Rol** | "Motor y Datos" | "Pantallas y Servidor" |
| **Carpetas que toca** | `mobile-android/.../core/`, `data/`, `domain/` | `mobile-android/.../ui/`, `backend-go/`, `analysis-python/` |
| **Fases** | F2 (2A y 2B), F3, F5 | F4, F6 |
| **Compartido** | F7 (tests, docs, integración) | F7 (tests, docs, integración) |

> [!IMPORTANT]
> Las clases que conectan el trabajo de los dos están definidas en [CONTRATOS.md](CONTRATOS.md).
> **Nadie cambia un contrato sin avisarle al otro.**

---

## 📅 Orden de arranque (para que nadie se quede esperando)

### Paso 1 — Cielo: Fase 2A (configuración base de Android)
Cambia `build.gradle.kts`, el package y agrega Compose/Hilt/Room.
➡️ **Mientras tanto el compañero NO toca `mobile-android/`** (evita conflictos en Gradle).

### Paso 1 — Compañero (al mismo tiempo): Fase 6 (backend)
Arranca con `backend-go/` y `analysis-python/`, que no dependen de Android.

### Paso 2 — Cuando Cielo hace merge de 2A en `main`
- Compañero: `git pull` y empieza **Fase 4** (pantallas) usando datos falsos.
- Cielo: sigue con **Fase 2B** (motor de audio) y **Fase 3** (Room).

### Paso 3 — Integración
Las pantallas del compañero se conectan al motor y Room de Cielo a través de los contratos.

---

## ✅ Checklist Cielo — "Motor y Datos"
- [ ] **2A** Renombrar app → AudioCheck, package `com.audiocheck.app`, minSdk 26
- [ ] **2A** Dependencias Compose, Hilt, Room, DataStore, Navigation
- [ ] **2A** Crear modelos de [CONTRATOS.md](CONTRATOS.md) en `domain/model/`
- [ ] **2B** `WiredAudioMonitor` + `AudioRouteValidator`
- [ ] **2B** `ToneEngine` + `AndroidToneEngine` (PCM, L/R, fade)
- [ ] **2B** `CalibrationProfile` + `DemoCalibrationProfile`
- [ ] **2B** `HearingTestEngine` + `DemoThresholdStrategy`
- [ ] **2B** `FakeToneEngine` + `FakeWiredAudioMonitor` (solo debug)
- [ ] **F3** Room: entidades, DAOs, repositorios, use cases
- [ ] **F5** `AudiogramExporter` + `FileProvider` + compartir

## ✅ Checklist Compañero — "Pantallas y Servidor"
- [ ] **F6** `backend-go/`: `go mod init`, `GET /health`, endpoints de sesiones
- [ ] **F6** `analysis-python/`: FastAPI, endpoint de análisis orientativo, pytest
- [ ] **F4** Tema Material 3 (colores, tipografía, dark mode)
- [ ] **F4** Navegación Compose
- [ ] **F4** Splash, Home, HeadphoneCheck, Instructions
- [ ] **F4** HearingTest (botón "LO ESCUCHO"), Results, History, Settings
- [ ] **F4** `AudiogramChart` con Canvas (O derecho / X izquierdo)
- [ ] **F4** Textos en `strings.xml`

---

## 🌿 Flujo de Git (cópialo tal cual)

**Antes de empezar a trabajar cada día:**
```bash
git checkout main
git pull origin main
git checkout -b feature/nombre-de-la-tarea
```

**Mientras trabajas (cada avance):**
```bash
git add .
git commit -m "Descripción corta de lo que hiciste"
git push origin feature/nombre-de-la-tarea
```

**Cuando terminas la tarea:**
1. En GitHub → botón **Compare & pull request** → **Create pull request**.
2. El otro lo revisa y le da **Merge**.
3. Los dos: `git checkout main` y `git pull origin main`.

### Nombres de ramas sugeridos
| Cielo | Compañero |
|---|---|
| `feature/android-base-setup` | `feature/backend-go` |
| `feature/audio-engine` | `feature/analysis-python` |
| `feature/headphone-monitor` | `feature/ui-theme-navigation` |
| `feature/room-database` | `feature/ui-screens` |
| `feature/export-share` | `feature/audiogram-chart` |

> [!WARNING]
> Nunca trabajen directo en `main`. Nunca usen `git push --force`.
