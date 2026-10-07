# 🤝 Contratos compartidos

Estas son las "piezas de LEGO" donde se unen el trabajo de **Cielo (motor/datos)** y del **compañero (pantallas)**.
El compañero puede programar las pantallas usando estos modelos con datos falsos, aunque el motor todavía no exista.

Paquete: `com.audiocheck.app.domain.model`

```kotlin
enum class Ear { LEFT, RIGHT }

/** Estado de los audífonos (lo produce WiredAudioMonitor, lo pinta HeadphoneCheckScreen). */
sealed interface WiredAudioState {
    data object Disconnected : WiredAudioState
    data class Connected(val deviceName: String) : WiredAudioState
    data class Unsupported(val reason: String) : WiredAudioState   // Bluetooth, altavoz, etc.
    data object RouteInvalid : WiredAudioState
    data class Ready(val deviceName: String) : WiredAudioState
}

/** Estado de la prueba (lo produce HearingTestEngine, lo pinta HearingTestScreen). */
sealed interface TestState {
    data object Preparing : TestState
    data class Running(val ear: Ear, val progress: Float) : TestState // progress 0f..1f
    data class Paused(val reason: PauseReason) : TestState
    data class Finished(val sessionId: Long) : TestState
    data class Error(val message: String) : TestState
}

enum class PauseReason { HEADPHONES_DISCONNECTED, VOLUME_CHANGED, USER }

/** Punto del audiograma (lo produce Room, lo pinta AudiogramChart). */
data class AudiogramPoint(
    val ear: Ear,
    val frequencyHz: Int,
    val thresholdLevel: Int,   // nivel interno (Level 1, 2, 3...), NO dB HL
    val unit: LevelUnit = LevelUnit.INTERNAL_LEVEL,
)

enum class LevelUnit { INTERNAL_LEVEL, DB_HL }

/** Resumen de una prueba (lo produce Room, lo pinta HistoryScreen). */
data class TestSessionSummary(
    val id: Long,
    val createdAt: Long,       // epoch millis
    val completed: Boolean,
)
```

Frecuencias del MVP: `500, 1000, 2000, 4000, 8000` Hz (preparado para 250, 3000, 6000).

> Si alguno necesita cambiar un contrato: lo dice primero, lo cambia en un PR pequeño y el otro hace `git pull`.
