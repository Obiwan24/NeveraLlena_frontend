# Reglas de Arquitectura y Código - Gestor de Pádel (KMP)

## 1. Idioma y Nomenclatura (ESTRICTO)
- **Todo el código debe escribirse en ESPAÑOL**: nombres de clases, interfaces, métodos, variables, parámetros, paquetes y propiedades de estado.
- Única excepción: palabras reservadas de Kotlin y nombres propios de librerías (ej. `ViewModel`, `StateFlow`).

## 2. Stack Tecnológico Multiplataforma (`commonMain`)
- **UI:** Compose Multiplatform con Material 3.
- **Arquitectura:** Clean Architecture + MVI (Modelo-Vista-Intención).
- **Inyección de Dependencias:** Koin.
- **Red:** Ktor Client + Kotlinx Serialization.

## 3. Estructura de Paquetes (`commonMain/kotlin/com/gestapadel/app`)
- `dominio/modelos/`: Clases de datos puras (`Enfrentamiento`, `EstadisticaJugador`, `Convocatoria`).
- `dominio/repositorios/`: Interfaces (`RepositorioEnfrentamientos`, `RepositorioEstadisticas`).
- `dominio/casosuso/`: Un caso de uso por acción de negocio (`ProponerFechasJornadaUseCase`, `CerrarConvocatoriaUseCase`).
- `datos/`: Implementación con Ktor, DTOs (`EnfrentamientoDto`) y mappers (`aDominio()`).
- `presentacion/`: Pantallas Compose, `ViewModels` y contratos MVI (`EstadoUi`, `EventoUi`, `EfectoUi`).

## 4. Reglas de Dominio del Pádel
- Un `Enfrentamiento` consta siempre de 3 `PartidoPareja` (6 jugadores convocados por equipo).
- Un capitán local siempre propone 2 fechas (`PropuestaFecha`).
- Las estadísticas individuales calculan: `partidosApuntados`, `partidosJugados`, `partidosGanados`, `partidosPerdidos`, `setsGanados`, `setsPerdidos`, `juegosGanados`, `juegosPerdidos`.