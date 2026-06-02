# Alerta Vecinal

## ⚠️ Advertencia importante sobre Replit y Hugging Face

En Replit NO utilizar:

- `api-inference.huggingface.co`
- `@huggingface/inference`
- llamadas directas a `*.huggingface.co`

Motivo: suelen fallar por restricciones de red o permisos.

## ✅ Solución soportada

Usar Replit AI Integrations + OpenRouter.

Modelo recomendado:

```text
microsoft/phi-3-mini-128k-instruct
```

## Código de ejemplo funcional

```ts
import { AI } from '@replit/ai'

const ai = new AI()

const respuesta = await ai.chatCompletion({
  model: 'microsoft/phi-3-mini-128k-instruct',
  messages: [
    { role: 'user', content: 'Hola' }
  ]
})
```

---

# Tipos TypeScript

```ts
export interface Reporte {
  id: string
  foto: string
  lat: number
  lng: number
  direccion: string
  descripcion: string
  votos: number
  estado: 'pendiente' | 'visto' | 'resuelto'
  fecha: Date
  usuarioId: string
}

export interface Canje {
  comercio: string
  puntosGastados: number
  fecha: string
}
```

---

# Estructura de localStorage

```json
{
  "usuarioId": "vecino_demo",
  "nombre": "Vecino Marplatense",
  "puntos": 125,
  "reportes": [],
  "votosRealizados": [],
  "canjes": []
}
```

---

# Logs obligatorios

```text
📍 Nuevo reporte creado en [dirección]
🗳️ Voto registrado para reporte [id]
🤖 IA analizando duplicados...
🤖 IA detectó posible duplicado con reporte [id]
💾 Progreso guardado en localStorage
🏆 Usuario sumó [X] puntos. Total: [Y]
```

---

# Prompts IA

## Detectar duplicados

```text
¿Estos dos reportes describen el mismo bache?
Reporte 1: ...
Reporte 2: ...
Respondé solo SI o NO.
```

## Prioridades

```text
Estos son los reportes más votados...
¿Cuáles son las 3 direcciones prioritarias?
```

## Resumen semanal

```text
Generá un resumen corto para la Municipalidad.
```

---

# Manejo de errores

## IA falla

Mostrar:

```text
La IA no pudo agrupar reportes automáticamente
```

Fallback:

```text
Menos de 50 metros = mismo reporte
```

## Mapa falla

```text
No se pudo cargar el mapa
```

Mostrar listado de reportes.

## Fotos grandes

Comprimir a máximo 500 KB.

## LocalStorage lleno

Conservar últimos 50 reportes.

---

# Fases de implementación

## Fase 1
- React
- Vite
- TypeScript
- Tailwind
- Wouter

## Fase 2
- Mapa Leaflet

## Fase 3
- Nuevo reporte

## Fase 4
- Votación y ranking

## Fase 5
- IA duplicados

## Fase 6
- IA prioridades

## Fase 7
- Recompensas

## Fase 8
- Dashboard municipal

---

# Estructura de carpetas

```text
src/
├── pages/
├── components/
├── hooks/
├── lib/
├── services/
└── types/
```

---

# Criterios de aceptación

- Sin errores TypeScript
- IA funcionando mediante OpenRouter
- Reportes con foto y ubicación
- Votación sin doble voto
- Ranking actualizado
- Persistencia en localStorage
- Fallback si la IA falla
- Mobile First
- Sin errores CORS
- Sin errores Failed to fetch
