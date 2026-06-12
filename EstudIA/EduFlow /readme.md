
  tareas: Tarea[];
  actividadesExtras: ActividadExtra[];
  puntajeTotal: number;
  retoSemanal: {
    semanaInicio: string; // fecha del lunes
    tareasCompletadas: number;
    bonusReclamado: boolean;
  };
}
🧮 SISTEMA DE PUNTOS Y RETOS
Reglas:
Acción	Puntos
Completar tarea antes del vencimiento	+15
Completar tarea el mismo día del vencimiento	+10
Completar tarea después del vencimiento	+5
Reto semanal (5+ tareas completadas en la semana)	+30 bonus
Cálculo de "semana":
La semana va de lunes a domingo

Se reinicia automáticamente cada lunes

📱 PANTALLAS OBLIGATORIAS
1. Dashboard (Home)
text
┌─────────────────────────────┐
│ 🎓 EduFlow        🏆 245 pts │
├─────────────────────────────┤
│ ⚠️ TAREAS DE HOY (2)         │
│ □ Matemática - Ejercicios    │
│ □ Historia - Leer capítulo   │
├─────────────────────────────┤
│ 🔥 RETO SEMANAL: 4/5 tareas  │
│ ████████░░ 80%               │
├─────────────────────────────┤
│ 📅 PRÓXIMA VENCE:            │
│ Ciencias - Trabajo (mañana)  │
├─────────────────────────────┤
│ [+ Nueva tarea]              │
│ [📋 Ver todas] [🏅 Logros]   │
└─────────────────────────────┘
2. Lista de Tareas
Filtros: Todas | Por materia | Vencidas | Completadas

Cada tarea muestra: checkbox, nombre, materia, días que faltan, prioridad con color

Botón eliminar (ícono basura)

3. Agregar Tarea
Campo: Nombre (input text)

Selector de materia (Matemática, Lengua, Ciencias, Historia, Inglés, Otra)

Date picker: <input type="date">

Selector de prioridad (Alta/Media/Baja)

Botón Guardar

4. Actividades Extras
Listado de actividades fijas (fútbol, inglés, gimnasio)

Agregar nueva: nombre, día (selector lunes a sábado), horario

Estas NO suman puntos pero aparecen en el dashboard como "ocupado"

5. Ranking/Logros local
Mostrar puntaje total

Insignias simples:

🎯 "Primer paso" (1 tarea completada)

⚡ "Racha de 3 días"

🔥 "Racha de 7 días"

💯 "100 puntos"

🏆 "Reto semanal cumplido"

🧩 COMPONENTES PRESENTACIONALES
tsx
// Ejemplo de estructura que SÍ funciona en Replit
const TarjetaTarea = ({ tarea, onCompletar, onEliminar }) => {
  const diasRestantes = calcularDiasRestantes(tarea.fechaVencimiento);
  
  return (
    <div className="bg-white rounded-lg p-4 shadow mb-2">
      <div className="flex items-center gap-3">
        <input 
          type="checkbox" 
          checked={tarea.completada}
          onChange={() => onCompletar(tarea.id)}
          className="w-5 h-5"
        />
        <div className="flex-1">
          <h3 className="font-semibold">{tarea.nombre}</h3>
          <p className="text-sm text-gray-600">{tarea.materia}</p>
        </div>
        <span className={`text-sm ${
          diasRestantes < 0 ? 'text-red-500' : 
          diasRestantes === 0 ? 'text-orange-500' : 'text-green-600'
        }`}>
          {diasRestantes < 0 ? 'Vencida' : 
           diasRestantes === 0 ? 'Hoy' : 
           `Faltan ${diasRestantes} días`}
        </span>
        <button onClick={() => onEliminar(tarea.id)} className="text-red-500">
          🗑️
        </button>
      </div>
    </div>
  );
};
📁 ESTRUCTURA DE ARCHIVOS (Replit compatible)
text
src/
├── App.tsx
├── main.tsx
├── index.css
├── pages/
│   ├── Home.tsx
│   ├── TareasLista.tsx
│   ├── AgregarTarea.tsx
│   ├── ActividadesExtras.tsx
│   └── Logros.tsx
├── components/
│   ├── TarjetaTarea.tsx
│   ├── Filtros.tsx
│   ├── ProgresoSemanal.tsx
│   └── BannerRecordatorio.tsx
├── hooks/
│   ├── useTareas.ts
│   ├── useActividades.ts
│   └── usePuntaje.ts
├── lib/
│   └── localStorage.ts
└── types/
    └── index.ts
🔧 FUNCIONES UTILITARIAS OBLIGATORIAS
typescript
// lib/fechas.ts
export const getDiasRestantes = (fechaVencimiento: string): number => {
  const hoy = new Date();
  hoy.setHours(0, 0, 0, 0);
  const vencimiento = new Date(fechaVencimiento);
  vencimiento.setHours(0, 0, 0, 0);
  const diff = vencimiento.getTime() - hoy.getTime();
  return Math.ceil(diff / (1000 * 60 * 60 * 24));
};

export const getSemanaActual = (): string => {
  const hoy = new Date();
  const dia = hoy.getDay();
  const lunes = new Date(hoy);
  lunes.setDate(hoy.getDate() - (dia === 0 ? 6 : dia - 1));
  return lunes.toISOString().split('T')[0];
};

export const esMismoDia = (fecha1: string, fecha2: string): boolean => {
  return fecha1 === fecha2;
};
✅ MANEJO DE ERRORES EN REPLIT
Problema	Solución
localStorage lleno	Limitar a 100 tareas máximo, mostrar alerta
Fecha inválida	Validar antes de guardar, usar new Date(fecha).toString() !== 'Invalid Date'
Estado perdido al recargar	Cargar desde localStorage en cada useEffect de inicio
CSS rotó en mobile	Usar Tailwind con container mx-auto px-4
🎨 REQUISITOS VISUALES (mobile-first)
Colores amigables: fondo gris claro (bg-gray-100), tarjetas blancas

Prioridades visuales:

Alta: borde rojo o texto rojo

Media: borde naranja

Baja: borde verde

Botones: mínimo 44x44px, con padding generoso

Títulos: claros y grandes (text-xl o text-2xl)

📋 CRITERIOS DE ACEPTACIÓN PARA REPLIT
No hay errores TypeScript en consola

npm run dev funciona sin errores

Al recargar la página, las tareas persisten

Se puede marcar una tarea como completada y suma puntos

El reto semanal se actualiza automáticamente

Las fechas se muestran correctamente (formato legible)

No hay any en TypeScript

Interfaz responsive (probado en vista móvil del inspector)

🚀 COMANDOS INICIALES PARA REPLIT
bash
# Crear proyecto (si empezás de cero)
npm create vite@latest eduflow -- --template react-ts
cd eduflow
npm install
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
npm install lucide-react  # opcional, íconos bonitos

# Tailwind config - Sobrescribir tailwind.config.js:
# content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"]

# Correr
npm run dev
💡 TIPS ESPECÍFICOS PARA REPLIT
El preview de Replit muestra la app en un iframe → las notificaciones del navegador no funcionan bien por eso usamos banner interno

Los logs se ven en la pestaña "Shell" o "Console" de Replit

Para debuggear agregar console.log en cada acción importante

Si Replit se pone lento, hacer Ctrl+Shift+R (recargar duro)

