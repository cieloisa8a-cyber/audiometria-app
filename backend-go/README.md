# 🐹 backend-go

API REST en Go para AudioCheck (sesiones, resultados y perfiles de calibración).

**Responsable:** compañero · **Fase:** 6 del [Plan Maestro](../docs/PLAN_MAESTRO.md)

## Endpoints planeados
| Método | Ruta |
|---|---|
| GET | `/health` |
| POST | `/api/v1/sessions` |
| GET | `/api/v1/sessions` |
| GET | `/api/v1/sessions/{id}` |
| POST | `/api/v1/sessions/{id}/results` |
| GET | `/api/v1/calibration-profiles/{id}` |

## Primeros pasos
```bash
cd backend-go
go mod init github.com/cieloisa8a-cyber/audiometria-app/backend-go
```

> La app Android funciona sin este backend (estrategia Local First).
