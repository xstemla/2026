# 💚 MenteApp - Apoyo emocional con IA para adolescentes

## 📌 Antes de empezar
Este archivo es la **guía para humanos**. 
Antes de seguir, asegurate de tener:
- [ ] Una cuenta en **Replit** (gratis, con Google o GitHub)
- [ ] Una cuenta en **Hugging Face** (gratis, para la IA)

> 💡 Todo es gratuito y no necesita instalación en tu computadora.

> ⚠️ **ADVERTENCIA IMPORTANTE**: Esta app es una herramienta de acompañamiento, NO reemplaza la ayuda profesional. En caso de emergencia, llamá al 135 (línea de prevención del suicidio) o al 911.

---

## 🎯 Qué hace esta app
**MenteApp** es un espacio de apoyo emocional para adolescentes y jóvenes que:
- Detecta cuando el usuario no está bien mediante un **"modo urgente"** accesible con un toque
- Acompaña en tiempo real con un **chat guiado por IA** (empático y seguro)
- Permite **avisar a un contacto de confianza** (simulado) con un toque
- Ofrece una **animación de respiración guiada** para calmar la ansiedad
- Permite **registrar el estado de ánimo** diario y ver la evolución
- Incluye un **espacio seguro anónimo** (foro moderado)
- Siempre muestra **recursos de emergencia** (135, 911)
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
> ⚠️ **MenteApp NO necesita Supabase**. Los datos (estado de ánimo, contactos, posts) se guardan en el celular (localStorage).

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
- Completar el onboarding (nombre opcional, contacto de confianza)
- Activar **Modo urgente** y explorar las acciones
- Chatear con la IA sobre un sentimiento (ej. "me siento solo/a")
- Registrar estado de ánimo por varios días
- Publicar en el espacio seguro anónimo

### 6. Publicar la app (para generar el APK)
- En Replit, hacer clic en el botón **"Deploy"** (ícono de Vercel)
- Conectar con GitHub y autorizar Vercel
- Vercel te da una URL pública (ej: `https://mente-app.vercel.app`)

### 7. Generar el APK para instalar en el celular
- Entrar a [pwabuilder.com](https://pwabuilder.com/)
- Pegar la URL que te dio Vercel
- Click en **"Build"** → **"Android"**
- Descargar el archivo `.apk`

### 8. Compartir con los compañeros
- Enviar el `.apk` por WhatsApp o Google Drive
- Cada uno lo instala en su celular
- Recuerden que es una herramienta de acompañamiento, no un reemplazo profesional

---

## 📱 Cómo se usa en el día a día
| Momento | El usuario hace... | La app hace... |
|--|--|--|
| **No se siente bien** | Toca "Modo urgente" | Ofrece acciones: hablar, avisar a contacto, respirar, emergencia |
| **Quiere desahogarse** | Abre el chat con IA | Escucha sin juzgar y ofrece recursos |
| **Quiere registrar su día** | Selecciona emoji y escribe | Guarda el estado de ánimo y muestra evolución |
| **Necesita ayuda inmediata** | Toca "Llamar al 135" | Abre el teléfono con el número listo |
| **Quiere sentirse acompañado** | Entra al espacio seguro | Lee y publica anónimamente |

> 💚 La app actúa cuando más lo necesitan.

---

## 🤖 ¿Dónde usamos IA?
| Ubicación | Qué hace la IA |
|--|--|
| **Chat guiado** | Conversa con empatía, valida sentimientos, deriva a emergencia si detecta riesgo |
| **Moderación de foro** | Detecta contenido peligroso (autolesión, acoso) |

**Prompt que usa la IA internamente (chat - seguro):**
```javascript
const prompt = `
 Mensaje: "${mensaje}"
 Si hay riesgo de vida, respondé SOLO: "Llamá al 135".
 Si no, mostrá empatía y ofrecé recursos.
 Tono cálido, adolescente, máximo 100 palabras.
`;
``````
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
| **La IA da un consejo inapropiado** | Revisar el prompt de seguridad. Incluir siempre derivación a 135. |
| **El usuario está en crisis real** | La app NO reemplaza ayuda profesional. Mostrar siempre emergencia. |
| **Los datos no se guardan** | Verificar localStorage |
| **No se genera el APK** | Probar con otra URL o usar [bubblewrap.dev](https://bubblewrap.dev/) |


----------

## 🎯 Frase para la defensa

> _"Usando Replit y Hugging Face, construimos MenteApp: una app de apoyo emocional para adolescentes. Detecta crisis con un modo urgente, acompaña con IA segura, permite avisar a un contacto de confianza y ofrece recursos de emergencia. No reemplaza a un profesional, pero actúa cuando más se necesita."_

----------

## 👥 Autores

Proyecto estudiantil - [Nombre del curso/institución]

## 📄 Licencia

MIT
