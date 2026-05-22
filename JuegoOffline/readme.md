Creá un juego mobile en React + TypeScript + Vite + Tailwind CSS (usando Canvas para el juego) que funcione SIN INTERNET (offline).
## NOMBRE: JuegoOffline
## FUNCIONALIDAD PRINCIPAL
Juego infinito estilo "runner" (inspirado en Subway Surfers) con una mecánica innovadora: en una esquina de la pantalla se reproduce la PARTIDA ANTERIOR del usuario en miniatura, permitiéndole ver DÓNDE falló la vez pasada y evitar el mismo error. Incluye IA que analiza la partida perdida y da consejos personalizados, además de sugerir desafíos cada 5 partidas.
---
## RESTRICCIONES (OBLIGATORIO RESPETAR)
- NO usar backend propio
- NO usar Firebase
- NO usar Redux, NO usar Zustand
- NO agregar autenticación real
- NO agregar funcionalidades fuera del MVP
- Mantener arquitectura simple
- Priorizar estabilidad sobre features
- **El juego debe funcionar OFFLINE (sin internet) - la IA solo se usa online, pero el juego base offline**
---
## ARQUITECTURA (DESACOPLADO)
- `useJuego`: toda la lógica del Canvas (personaje, obstáculos, colisiones, puntaje)
- `usePartidaAnterior`: lógica de guardar y reproducir la partida anterior
- `useHuggingFace`: lógica de IA para analizar errores y generar desafíos (solo online)
- `usePuntajes`: lógica de mejor puntaje y estadísticas (localStorage)
- Los componentes deben ser presentacionales
---
## DEFINICIONES EXACTAS
- **RUNNER**: personaje que corre automáticamente hacia la derecha
- **OBSTÁCULO**: elemento que aparece en el camino y causa game over al colisionar
- **PARTIDA ANTERIOR**: grabación simplificada de la última partida (posiciones de obstáculos o evento de muerte)
- **GAME OVER**: estado cuando el personaje colisiona con un obstáculo
---
## LOGS OBLIGATORIOS (para debugging)
- 🎮 Juego iniciado
- 💀 Game over - puntaje: [X], obstáculo: [tipo]
- 💾 Partida anterior guardada en localStorage
- 🤖 Consultando Hugging Face para analizar error...
- 🤖 IA respondió: [consejo]
- 🏆 Desafío generado por IA
- ⚠️ Error de Hugging Face (el juego sigue funcionando offline)
---
## IMPLEMENTACIÓN POR FASES
### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Crear componente Canvas (useRef, requestAnimationFrame)
- Juego base: personaje que corre, obstáculos que se mueven de derecha a izquierda
- Detección básica de colisiones
### FASE 2 - Mecánica principal (runner infinito)
- Personaje: cuadrado o sprite simple (puede saltar o agacharse)
- Obstáculos: generar aleatoriamente cada cierto tiempo
- Puntaje: aumenta con el tiempo o distancia
- Velocidad: aumenta gradualmente con el puntaje
### FASE 3 - Mecánica innovadora: partida anterior
- Guardar en localStorage la última partida:
 - Puntaje final
 - Posición X donde ocurrió el game over
 - Tipo de obstáculo que causó la muerte
- En la siguiente partida, mostrar en una esquina (ej. 150x100px) una REPLAY SIMPLIFICADA:
 - Reproducir la trayectoria del obstáculo que mató
 - Mostrar texto: "Aquí fallaste la última vez"
- Esto permite que el usuario vea su error mientras juega
### FASE 4 - Puntajes y estadísticas
- Mejor puntaje histórico (localStorage)
- Puntaje actual en tiempo real
- Contador de partidas jugadas
- Opción de reinicio rápido (botón "Reiniciar")
### FASE 5 - Integración con Hugging Face IA (solo online)
- SDK: @huggingface/inference
- Modelo: microsoft/Phi-3-mini-4k-instruct
- Variable: VITE_HF_TOKEN
- Función: Al perder, enviar datos a IA para consejo personalizado
- **El juego NO depende de la IA para funcionar** (si falla, solo no muestra consejo)
### FASE 6 - Análisis de errores con IA
- Al hacer game over, llamar a IA con:
 - Puntaje actual, mejor puntaje, tipo de obstáculo que causó muerte
- IA responde con consejo corto (máximo 15 palabras) y motivador
- Mostrar consejo en pantalla (ej. "Fallaste por el tren amarillo, saltá más temprano")
### FASE 7 - Desafíos personalizados por IA
- Contar partidas jugadas (localStorage)
- Cada 5 partidas, preguntar a IA: "Generá un desafío personalizado para este jugador"
- Desafío: objetivo medible (ej. "llegá a 800 puntos esquivando más obstáculos")
- Mostrar desafío actual en pantalla principal
### FASE 8 - Optimización y diseño
- Colores vibrantes (naranja, azul eléctrico, verde)
- Modo oscuro opcional (toggle en localStorage)
- Optimizado para celulares de gama baja:
 - Reducir número de obstáculos en pantalla
 - Simplificar detección de colisiones
 - Usar requestAnimationFrame eficiente
---
## LOCALSTORAGE (estructura de datos)
```json
{
 "mejorPuntaje": 2500,
 "partidasJugadas": 34,
 "ultimaPartida": {
 "puntaje": 1200,
 "obstaculoMuerte": "tren",
 "posicionX_muerte": 350,
 "timestamp": 1715678901234
 },
 "desafioActual": "Superá los 1000 puntos",
 "desafiosCompletados": ["superar 500 puntos", "esquivar 10 obstáculos seguidos"],
 "configuracion": {
 "modoOscuro": false
 }
}
```
----------

## JUEGO (requisitos técnicos - Canvas)

-   **Tamaño Canvas**: ancho 100%, alto 400px-500px (responsive)
-   **Personaje**: 30x30px, salta con tap/clic o espacio
-   **Obstáculos**: 20x30px, generación aleatoria cada 1.5s (intervalo disminuye con velocidad)
-   **Colisiones**: AABB collision detection (cajas)
-   **FPS**: 60 usando requestAnimationFrame
-   **Partida anterior replay**: Canvas secundario de 120x80px en esquina superior derecha, reproduce animación del último obstáculo que mató
    

----------

## HUGGING FACE IA (detalles específicos)

**Prompt para análisis de error (game over):**

```javascript
const prompt = `
 El jugador perdió con puntaje: ${puntaje} (récord: ${mejorPuntaje}).
 El obstáculo que lo mató fue: ${obstaculo}.
 DALE UN CONSEJO CORTO (máximo 15 palabras) y MOTIVADOR.
 Respondé SOLO el consejo, sin explicación adicional.
`;
```
**Prompt para generar desafío personalizado:**

```javascript
const prompt = `
 El jugador ha completado ${partidasJugadas} partidas.
 Su mejor puntaje es ${mejorPuntaje}.
 Generá un desafío corto y específico para mejorar (ej. "llegá a 800 puntos").
 Respondé SOLO el desafío, una frase corta.
`;
```

**Uso de IA no bloqueante:**

-   Si la IA falla o timeout, mostrar consejo genérico (ej. "¡Intentá de nuevo, prestá atención a los obstáculos amarillos!")    
-   Los desafíos se guardan localmente si la IA no responde
    
----------

## MANEJO DE ERRORES (OBLIGATORIO)

### Hugging Face falla o timeout

-   Mostrar consejo genérico predefinido
-   Desafío por defecto: "Superá tu récord actual"
-   El juego sigue funcionando perfectamente offline
    

### Canvas lento o frame drops

-   Reducir cantidad de obstáculos si detecta baja performance
-   Simplificar colisiones (bounding box simple)
    
### localStorage lleno o error

-   No guardar la partida actual, solo mantener en memoria
-   Mostrar advertencia no intrusiva
    
### Game over inesperado

-   Asegurar que la colisión sea precisa (hitbox del personaje)

----------

## MOBILE (OBLIGATORIO)

-   El juego debe ser jugable con TAP (tocar pantalla para saltar)
-   Evitar overflow horizontal
-   Compatible con iPhone SE y Android Chrome
-   Botón de reinicio de al menos 44x44px
-   Canvas táctil (eventos touchstart)
-   Modo oscuro visible en condiciones de poca luz
    
----------

## VARIABLES DE ENTORNO (Secrets en Replit)

```text
VITE_HF_TOKEN = token_huggingface
```

----------

## ESTRUCTURA DE ARCHIVOS

```text
src/
├── App.tsx
├── components/
│   ├── CanvasJuego.tsx
│   ├── ReplayPartidaAnterior.tsx
│   ├── Puntaje.tsx
│   ├── ConsejoIA.tsx
│   ├── DesafioIA.tsx
│   └── BotonesControl.tsx
├── hooks/
│   ├── useJuego.ts
│   ├── usePartidaAnterior.ts
│   ├── useHuggingFace.ts
│   └── usePuntajes.ts
├── lib/
│   └── localStorage.ts
├── utils/
│   ├── colisiones.ts
│   └── generadorObstaculos.ts
└── types/
 └── index.ts
```

----------

## DEPENDENCIAS

```text
react, react-dom, typescript, vite, tailwindcss
@huggingface/inference
lucide-react
```
----------

## CRITERIOS DE ACEPTACIÓN

-   Sin errores TypeScript
-   Juego funciona offline (sin conexión, la IA no es necesaria)
-   Mecánica runner: personaje corre, obstáculos aparecen, colisiones detectan game over
-   Puntaje en tiempo real y mejor puntaje histórico guardado
-   Partida anterior se guarda y se reproduce en miniatura en la siguiente partida
-   Al perder, IA da consejo personalizado (si hay conexión)
-   Cada 5 partidas, IA genera desafío personalizado
-   Modo oscuro opcional funciona
-   Diseño responsive, jugable con tap en celular
-   Fallback elegante si Hugging Face no responde
