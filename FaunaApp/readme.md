Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.

## NOMBRE: FaunaApp

## FUNCIONALIDAD PRINCIPAL
Registrar avistajes de fauna (especie, ubicación, fecha, foto). Los datos se guardan en localStorage y se muestran en un listado ordenado del más reciente al más antiguo. Incluye IA opcional para sugerir categoría (ave/mamífero/reptil/insecto) según la especie.

---
## RESTRICCIONES (OBLIGATORIO RESPETAR)
- NO usar backend propio
- NO usar Firebase
- NO usar Redux, NO usar Zustand
- NO agregar autenticación real
- NO agregar funcionalidades fuera del MVP
- Mantener arquitectura simple
- Priorizar estabilidad sobre features

---

## ARQUITECTURA (DESACOPLADO)
- `useFauna`: toda la lógica de avistajes (CRUD + localStorage)
- `useHuggingFace`: lógica de IA para clasificar especies (opcional)
- Los componentes deben ser presentacionales (FormularioAvistaje, ListaAvistajes, TarjetaAvistaje)

---

## DEFINICIONES EXACTAS
- **AVISTAJE**: registro con especie (texto), ubicación (texto), fecha (YYYY-MM-DD), foto (opcional, base64)
- **CATEGORÍA IA**: Ave, Mamífero, Reptil, Insecto, Otro (sugerida por IA)

---
## LOGS OBLIGATORIOS (para debugging)
- 📝 Avistaje guardado: [especie]
- 🗑️ Avistaje eliminado: [id]
- 🧹 Todos los avistajes eliminados
- 🤖 Consultando IA para clasificar especie...
- 🤖 IA respondió: [categoría]
- ⚠️ Error de Hugging Face
- 💾 Datos cargados desde localStorage

---
## IMPLEMENTACIÓN POR FASES

### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Un solo componente App (sin routing complejo)

### FASE 2 - Formulario de avistaje
- Campos: Especie (texto, obligatorio), Ubicación (texto, obligatorio)
- Fecha: input type="date" con valor por defecto = hoy
- Foto: input type="file" accept="image/*" (opcional)
- Botón "Guardar avistaje"

### FASE 3 - Integración con Hugging Face IA (opcional)
- SDK: @huggingface/inference
- Modelo: microsoft/Phi-3-mini-4k-instruct
- Variable: VITE_HF_TOKEN
- Función: Al escribir la especie, sugerir categoría automáticamente
- La IA NO es obligatoria para guardar (fallback silencioso)

### FASE 4 - Guardar en localStorage
- Al enviar el formulario, crear objeto avistaje con:
 - id: Date.now()
 - especie, ubicacion, fecha, foto (base64 si existe)
- Guardar en localStorage con clave "avistajes"
- Actualizar lista

### FASE 5 - Listado de avistajes
- Mostrar todos los avistajes debajo del formulario
- Ordenar por fecha descendente (más reciente primero)
- Cada tarjeta muestra: especie, ubicación, fecha, miniatura de foto (si existe)
- Botón "Eliminar" por cada avistaje

### FASE 6 - Eliminar avistajes
- Botón "Eliminar" en cada tarjeta → borra ese avistaje
- Botón "Eliminar todos" → confirmación (alert o modal) → borra todo
- Actualizar localStorage y lista

### FASE 7 - Clasificación con IA (mejora)
- Cuando el usuario completa el campo "Especie", opcionalmente consultar a IA:
 - Prompt: "Clasificá esta especie en: Ave, Mamífero, Reptil, Insecto u Otro. Respondé SOLO la categoría."
 - Mostrar sugerencia debajo del campo (ej. "🦅 Categoría sugerida: Ave")
 - El usuario puede ignorar o aceptar (la categoría no se guarda obligatoriamente)

### FASE 8 - Validaciones y experiencia mobile
- Validar que especie y ubicación no estén vacíos
- Mostrar mensaje de éxito al guardar (toast o alert)
- Confirmación antes de "Eliminar todos"
- Diseño mobile-first

---
## LOCALSTORAGE (estructura de datos)
```json
{
 "avistajes": [
 {
 "id": 1715678901234,
 "especie": "Hornero",
 "ubicacion": "Parque Saavedra, La Plata",
 "fecha": "2025-05-20",
 "foto": "data:image/jpeg;base64,..."  // opcional
 },
 {
 "id": 1715678905678,
 "especie": "Lagartija Overa",
 "ubicacion": "Sierras de Tandil",
 "fecha": "2025-05-19",
 "foto": null
 }
 ]
}
```
----------

## HUGGING FACE IA (detalles específicos)

**Prompt para clasificar especie:**

```javascript
const prompt = `
 Especie de animal: ${especie}
 Clasificá en una de estas categorías: Ave, Mamífero, Reptil, Insecto, Otro.
 Respondé SOLO con el nombre de la categoría, nada más.
 Ejemplo de respuesta: "Ave"
`;
```
**Uso en la app:**

-   Mientras el usuario escribe la especie (debounce de 1 segundo)   
-   Si la IA responde, mostrar un badge debajo del campo: "🔍 Categoría sugerida: [categoría]"   
-   Si la IA falla o timeout, no mostrar nada (fallback silencioso)
    
----------

## MANEJO DE ERRORES (OBLIGATORIO)

### Hugging Face falla o timeout

-   No interrumpir el flujo principal  
-   Simplemente no mostrar sugerencia de categoría  
-   Registrar en consola/log: "⚠️ IA no disponible"
    

### Foto muy grande

-   Al leer el archivo, limitar tamaño (ej. redimensionar a max 500px)   
-   Si es muy pesada, mostrar mensaje "La foto se reducirá automáticamente"
    

### localStorage lleno o error

-   Mostrar mensaje "No se pudo guardar. Liberá espacio."   
-   Limitar cantidad de avistajes (mostrar advertencia al llegar a 50)
    

### Eliminar todos sin confirmación

-   Usar window.confirm("¿Eliminar todos los avistajes?") antes de borrar
    

----------

## MOBILE (OBLIGATORIO)

-   Evitar overflow horizontal    
-   Compatible con iPhone SE y Android Chrome   
-   Botones tamaño mínimo 44x44px   
-   Campos de formulario ocupan todo el ancho (w-full)  
-   Input type="date" funciona en celular (selector nativo) 
-   Fotos: input file con captura desde cámara (capture="environment")   
-   Tarjetas de avistajes fáciles de tocar
    

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
│   ├── FormularioAvistaje.tsx
│   ├── ListaAvistajes.tsx
│   ├── TarjetaAvistaje.tsx
│   └── SugerenciaIA.tsx
├── hooks/
│   ├── useFauna.ts
│   └── useHuggingFace.ts
├── lib/
│   └── localStorage.ts
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
-   Formulario guarda avistaje con especie, ubicación, fecha, foto (opcional)    
-   Los avistajes persisten en localStorage  
-   Listado ordenado por fecha descendente   
-   Botón "Eliminar" borra avistaje individual  
-   Botón "Eliminar todos" con confirmación borra todo  
-   La IA sugiere categoría (opcional, no bloqueante)   
-   Diseño mobile-first con colores naturaleza (verdes, marrones, celestes)   
-   Fallback elegante si Hugging Face no responde
    

