# 💪 EntrenamientoApp - App con IA para aprender sobre entrenamiento y salud

## 📌 Antes de empezar

Este archivo es la **guía para humanos**. 
Antes de seguir, asegurate de tener:
- [ ] Una cuenta en **Replit** (gratis, con Google o GitHub)
- [ ] Una cuenta en **Hugging Face** (gratis, para la IA)
> 💡 Todo es gratuito y no necesita instalación en tu computadora.

---

## 🎯 Qué hace esta app
Ayuda a jóvenes y adolescentes a aprender sobre entrenamiento y salud de manera sencilla. La app incluye:

- Categorías por nivel (principiante, intermedio, avanzado)
- Videos y explicaciones de ejercicios
- Seguimiento de progreso (peso, entrenamientos, gráficos)
- Ranking con amigos y desafíos semanales
- Asistente IA que recomienda rutinas y responde preguntas

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

> ⚠️ **EntrenamientoApp NO necesita Supabase**. Los datos (progreso, nivel, entrenamientos) se guardan en el celular (localStorage).

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
- Explorar las categorías (principiante, intermedio, avanzado)
- Ver un video de ejercicio
- Anotar un entrenamiento (fecha, duración, peso)
- Preguntar al asistente IA: "¿cómo hago sentadillas?"

### 6. Publicar la app (para generar el APK)
- En Replit, hacer clic en el botón **"Deploy"** (ícono de Vercel)
- Conectar con GitHub y autorizar Vercel
- Vercel te da una URL pública (ej: `https://entrenamiento-app.vercel.app`)

### 7. Generar el APK para instalar en el celular
- Entrar a [pwabuilder.com](https://pwabuilder.com/)
- Pegar la URL que te dio Vercel
- Click en **"Build"** → **"Android"**
- Descargar el archivo `.apk`

### 8. Compartir con los compañeros
- Enviar el `.apk` por WhatsApp o Google Drive
- Cada uno lo instala en su celular
- Empiezan a entrenar y seguir su progreso

---

## 📱 Cómo se usa en el día a día

| Momento | El usuario hace... | La app hace... |
|--|--|--|
| Quiere empezar a entrenar | Elige categoría "principiantes" | Muestra videos y explicaciones |
| Anota su progreso | Ingresa peso, repeticiones, tiempo | Guarda datos y muestra gráfico |
| Compite con amigos | Mira el ranking | Muestra quién entrenó más días |
| Completa un desafío | Nada (automático) | IA felicita y sugiere próximo desafío |
| Tiene una duda | Pregunta "¿cómo hago sentadillas?" | IA responde y sugiere video |
| Comparte su logro | Toca "compartir" | Abre WhatsApp con mensaje |

> 💪 El usuario aprende, entrena y mejora su salud con ayuda de IA.

---
## 🤖 ¿Dónde usamos IA?

| Ubicación | Qué hace la IA |
|--|--|
| **Recomendación de rutinas** | Según nivel y objetivo, sugiere ejercicios |
| **Asistente de preguntas** | Responde dudas sobre técnica, lesiones, nutrición |
| **Motivación personalizada** | "¡Ya entrenaste 3 días seguidos!" |
| **Sugerencia de desafíos** | Propone metas según progreso |

**Prompt que usa la IA internamente (recomendar rutina):**

```javascript
const prompt = `
 Nivel: ${nivel} (principiante/intermedio/avanzado)
 Objetivo: ${objetivo} (ganar fuerza/bajar de peso/mejorar resistencia)
 Días por semana: ${dias}
 Respondé EXACTAMENTE en este formato:
 Rutina: [3-4 ejercicios con repeticiones]
 Técnica: [consejo corto]
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
| **La IA no responde** | Verificar que el token `VITE_HF_TOKEN` esté bien copiado |
| **Los videos no se ven** | En la versión inicial son ejemplos embebidos de YouTube. Verificar conexión a internet |
| **Los datos de progreso se pierden** | Verificar que localStorage esté habilitado en el navegador |
| **El gráfico no se muestra bien** | Asegurar que haya al menos 2 registros de peso/entrenamiento |
| **No se genera el APK** | Probar con otra URL o usar [bubblewrap.dev](https://bubblewrap.dev/) |

----------

## 🎯 Frase para la defensa

> _"Usando solo Replit desde el navegador, con IA gratuita de Hugging Face, construimos una app de entrenamiento para jóvenes: con videos educativos, seguimiento de progreso, funciones sociales y un asistente IA que recomienda rutinas, responde preguntas y motiva al usuario. Todo gratis, sin necesidad de base de datos externa."_

----------

## 👥 Autores

Proyecto estudiantil - [Nombre del curso/institución]

## 📄 Licencia

MIT
