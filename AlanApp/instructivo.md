# 🧠 AlanApp - Asistente de estudio con IA

## 📌 Antes de empezar
Este archivo es la **guía para humanos**. 
Antes de seguir, asegurate de tener:
- [ ] Una cuenta en **Replit** (gratis, con Google o GitHub)
- [ ] Una cuenta en **Hugging Face** (gratis, para la IA)

> 💡 Todo es gratuito y no necesita instalación en tu computadora.

---

## 🎯 Qué hace esta app

Alan es un asistente de estudio con IA que:
- Divide tareas grandes en pasos pequeños y alcanzables
- Sugiere planes de estudio según tus materias
- Te da piezas de un rompecabezas como recompensa por cada paso completado
- Si no usás la app por varios días, Alan se preocupa y te envía mensajes personalizados
- Tiene un avatar amigable y colores cálidos

---

## 🛠️ Herramientas (todo desde el navegador)
| Herramienta | Link | Para qué |
| :--- | :--- | :--- |
| **Replit** | replit.com | Escribir y ejecutar el código |
| **Hugging Face** | huggingface.co | IA gratuita |
| **Vercel** | vercel.com | Publicar la app gratis |
| **PWABuilder** | pwabuilder.com | Convertir la app en APK |

✅ **No se instala nada en la computadora.**

---

## 🚀 Paso a paso

### 1. Crear las cuentas gratuitas (5 minutos)

**A. Hugging Face** (la IA)
- Entrar a [huggingface.co](https://huggingface.co)
- Registrarse con email
- Ir a **Settings** → **Access Tokens** → **New token** → copiar el token

**B. Replit** (el editor de código)
- Entrar a [replit.com](https://replit.com/)
- Registrarse con Google o GitHub

> ⚠️ **AlanApp NO necesita Supabase**. Los datos (tareas, progreso, rompecabezas) se guardan en el celular (localStorage).

### 2. Crear el proyecto en Replit
- Click en **"Create new Repl"** → **"Create with AI"**

### 3. Configurar los "Secretos" (Keys)
En Replit, ir a **Tools** → **Secrets** (🔒) y agregar:
| Secret | Valor |
|--|--|
| `VITE_HF_TOKEN` | El token que copiaste de Hugging Face |

### 4. Copiar el prompt
Abrir el archivo `readme.md` de este proyecto y **copiar TODO su contenido**.
En Replit, pegar el prompt en el chat del **"Replit Agent"** y esperar a que genere la app.

### 5. Ver la app funcionando
A la derecha de la pantalla aparece una vista previa. Probá:
- Completar el onboarding (nombre y materias)
- Crear una tarea: "estudiar para el examen de matemáticas"
- Ver cómo Alan la divide en pasos
- Completar un paso y recibir una pieza del rompecabezas
- (Opcional) Simular abandono esperando 3 días o cambiando la fecha en el código

### 6. Publicar la app (para generar el APK)
- En Replit, hacer clic en el botón **"Deploy"** (ícono de Vercel)
- Conectar con GitHub y autorizar Vercel
- Vercel te da una URL pública (ej: `https://alan-app.vercel.app`)

### 7. Generar el APK para instalar en el celular
- Entrar a [pwabuilder.com](https://pwabuilder.com/)
- Pegar la URL que te dio Vercel
- Click en **"Build"** → **"Android"**
- Descargar el archivo `.apk`

### 8. Compartir con los compañeros
- Enviar el `.apk` por WhatsApp o Google Drive
- Cada uno lo instala en su celular
- Empiezan a usar a Alan como asistente de estudio

---

## 📱 Cómo se usa en el día a día
| Momento | El usuario hace... | La app hace... |
|--|--|--|
| Primera vez | Abre la app, pone nombre y materias | Alan da la bienvenida |
| Tiene un examen | Escribe "estudiar 5 temas" | IA divide en pasos chicos |
| Completa un paso | Toca "Completar" | Suma progreso y da una pieza de rompecabezas |
| No abre la app por días | Nada (automático) | Alan muestra mensaje de preocupación |
| Completa todas las piezas | Junta las piezas | Se completa el rompecabezas y la recompensa |

> 🧩 Alan te ayuda a organizarte y te motiva a no abandonar.

---

## 🤖 ¿Dónde usamos IA?
| Ubicación | Qué hace la IA |
|--|--|
| **División de tareas** | Recibe "estudiar matemática" y lo divide en pasos lógicos |
| **Plan de estudio personalizado** | Sugiere horarios según materias y disponibilidad |
| **Mensajes de preocupación** | Genera mensajes únicos cuando el usuario abandona |
| **Detección de abandono** | Analiza tiempo sin actividad y decide qué mensaje enviar |

**Prompt que usa la IA internamente (dividir tarea):**
```javascript
const prompt = `
 Tarea del usuario: ${tarea}
 Sus materias: ${materias}
 Dividí esta tarea en 3 a 5 pasos pequeños.
 Estimá el tiempo total en minutos.
 Agregá un mensaje motivador.
 Formato:
 Pasos: [paso 1, paso 2, ...]
 Tiempo: [X] minutos
 Motivación: [frase corta]
`;
```
----------

## 💰 Costos

| Servicio | Costo |
|--|--|
| Replit | $0 |
| Hugging Face | $0 |
| Vercel | $0 |
| PWABuilder | $0 |
| **TOTAL** | **$0** |

----------

## ❓ Problemas comunes

| Problema | Solución |
|--|--|
| **Alan no responde** | Verificar que el token `VITE_HF_TOKEN` esté bien copiado |
| **Las piezas del rompecabezas no se guardan** | Revisar que localStorage esté habilitado |
| **Los mensajes de preocupación no aparecen** | Verificar que pasaron 3 días desde la última actividad. Podés probar cambiando la fecha en el código |
| **La app se ve mal en celular** | El prompt ya pide diseño responsive. Si algo falla, ajustar Tailwind |
| **No se genera el APK** | Probar con otra URL o usar [bubblewrap.dev](https://bubblewrap.dev/) |


----------

## 🎯 Frase para la defensa

> _"Usando solo Replit desde el navegador, con IA gratuita de Hugging Face, construimos a Alan, un asistente de estudio que divide tareas grandes en pasos chicos, da recompensas con un sistema de rompecabezas, y se preocupa por el usuario si abandona la app. Todo gratis, pensado para motivar a estudiantes."_

----------

## 👥 Autores

Proyecto estudiantil - [Nombre del curso/institución]

## 📄 Licencia

MIT



