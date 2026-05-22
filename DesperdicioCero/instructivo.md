# 🥗 DesperdicioCero - App con IA para evitar desperdicio de comida

## 📌 Antes de empezar
Este archivo es la **guía para humanos**. 
Antes de seguir, asegurate de tener:
- [ ] Una cuenta en **Replit** (gratis, con Google o GitHub)
- [ ] Una cuenta en **Hugging Face** (gratis, para la IA)
> 💡 Todo es gratuito y no necesita instalación en tu computadora.
>
 
---
## 🎯 Qué hace esta app
Ayuda a las personas a evitar desperdiciar comida y aprovechar residuos orgánicos. La app permite:
- Escanear productos (simulado con texto)
- Recibir recetas con alimentos próximos a vencer
- Ideas para compostaje y reutilización de residuos
- Foro comunitario con asistente IA
- Ranking de "comidas salvadas" y dinero ahorrado

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

> ⚠️ A diferencia de los otros proyectos, **DesperdicioCero NO necesita Supabase**. Los datos se guardan en el celular (localStorage).

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
- Escanear un producto (escribí "leche" o "tomates")
- Pedir recetas con ingredientes como "huevos, pan, leche"
- Preguntar "¿qué hago con cáscaras de banana?" en el foro

### 6. Publicar la app (para generar el APK)
- En Replit, hacer clic en el botón **"Deploy"** (ícono de Vercel)
- Conectar con GitHub y autorizar Vercel
- Vercel te da una URL pública (ej: `https://desperdicio-cero.vercel.app`)

### 7. Generar el APK para instalar en el celular
- Entrar a [pwabuilder.com](https://pwabuilder.com/)
- Pegar la URL que te dio Vercel
- Click en **"Build"** → **"Android"**
- Descargar el archivo `.apk`

### 8. Compartir con los compañeros
- Enviar el `.apk` por WhatsApp o Google Drive
- Cada uno lo instala en su celular
- Empiezan a evitar desperdicios y ahorrar dinero

---

## 📱 Cómo se usa en el día a día
| Momento | El usuario hace... | La app hace... |
|--|--|--|
| Compra un producto | Escribe el nombre del producto | La IA lo identifica y guarda |
| Producto próximo a vencer | Nada (automático) | Sugiere recetas para usarlo |
| Tiene ingredientes sueltos | Escribe "huevos, pan, leche" | IA recomienda recetas |
| Tiene restos orgánicos | Pregunta "¿qué hago con cáscaras?" | IA da ideas (compost, abono) |
| Quiere compartir un tip | Publica en el foro | Otros usuarios pueden verlo |
| Quiere competir | Ve su puntaje | Ranking de "comidas salvadas" |

> 🥑 La app ayuda a no tirar comida y ahorrar dinero.

---
## 🤖 ¿Dónde usamos IA?

| Ubicación | Qué hace la IA |
|--|--|
| **Identificación de productos** | Recibe nombre del producto y estima fecha de vencimiento |
| **Recetas inteligentes** | Según ingredientes disponibles, sugiere recetas |
| **Tips para residuos** | Responde preguntas sobre reutilización de residuos |
| **Asistente del foro** | Responde dudas de usuarios |

**Prompt que usa la IA internamente (ejemplo para recetas):**

```javascript
const prompt = `
 Ingredientes disponibles: ${ingredientes}
 Productos próximos a vencer: ${productos}
 Generá 2 recetas que usen estos ingredientes.
 Formato:
 Receta 1: [nombre] - [pasos cortos]
 Receta 2: [nombre] - [pasos cortos]
 Consejo: [texto corto]
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
| **Las recetas no son precisas** | Mejorar el prompt con más detalles de los ingredientes |
| **Los datos se pierden** | Verificar que localStorage esté habilitado en el navegador |
| **No se genera el APK** | Probar con otra URL o usar [bubblewrap.dev](https://bubblewrap.dev/) |


----------

## 🎯 Frase para la defensa

> _"Usando solo Replit desde el navegador, con IA gratuita de Hugging Face, construimos una app que ayuda a evitar el desperdicio de comida: identifica productos, sugiere recetas, da ideas para reutilizar residuos y tiene un foro comunitario con ranking. Todo gratis, sin necesidad de base de datos externa."_

----------

## 👥 Autores

Proyecto estudiantil - [Nombre del curso/institución]

## 📄 Licencia

MIT
