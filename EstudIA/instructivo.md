# 📚 EstudIA - App con IA para apoyo escolar gratuito

## 📌 Antes de empezar
Este archivo es la **guía para humanos**. 
Antes de seguir, asegurate de tener:
- [ ] Una cuenta en **Replit** (gratis, con Google o GitHub)
- [ ] Una cuenta en **Hugging Face** (gratis, para la IA)
> 💡 Todo es gratuito y no necesita instalación en tu computadora.

---

## 🎯 Qué hace esta app

Ayuda a estudiantes de secundaria (13 a 18 años) a entender temas del colegio de manera gratuita. La app incluye:

- Videos educativos organizados por materia (currícula de Buenos Aires)
- Asistente IA que explica temas y responde preguntas
- Generación automática de ejercicios personalizados
- Seguimiento de progreso (videos vistos, puntaje)
- Función "seguir estudiando" (retoma último tema)

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
> ⚠️ **EstudIA NO necesita Supabase**. Los datos (progreso, puntaje, temas vistos) se guardan en el celular (localStorage).

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
- Seleccionar materia y tema (ej. Matemática → Fracciones)
- Ver un video educativo
- Preguntar al asistente: "¿cómo se resuelve una ecuación?"
- Pedir "dame ejercicios de fracciones"

### 6. Publicar la app (para generar el APK)
- En Replit, hacer clic en el botón **"Deploy"** (ícono de Vercel)
- Conectar con GitHub y autorizar Vercel
- Vercel te da una URL pública (ej: `https://estudia-ia.vercel.app`)

### 7. Generar el APK para instalar en el celular
- Entrar a [pwabuilder.com](https://pwabuilder.com/)
- Pegar la URL que te dio Vercel
- Click en **"Build"** → **"Android"**
- Descargar el archivo `.apk`

### 8. Compartir con los compañeros
- Enviar el `.apk` por WhatsApp o Google Drive
- Cada uno lo instala en su celular
- Empiezan a estudiar con ayuda de IA

---

## 📱 Cómo se usa en el día a día
| Momento | El usuario hace... | La app hace... |
|--|--|--|
| No entiende un tema | Elige materia y tema | Muestra videos explicativos |
| Termina un video | Nada (automático) | IA recomienda siguiente tema o ejercicios |
| Tiene una duda | Pregunta "¿cómo se resuelve una ecuación?" | IA explica paso a paso |
| Quiere practicar | Pide "dame ejercicios de fracciones" | IA genera 3 ejercicios con soluciones |
| Vuelve a la app | Abre la app | Retoma donde lo dejó (último tema visto) |
> 📖 El estudiante aprende a su ritmo, sin pagar.

---

## 🤖 ¿Dónde usamos IA?
| Ubicación | Qué hace la IA |
|--|--|
| **Asistente personal de estudio** | Responde preguntas específicas sobre temas escolares |
| **Recomendación de contenido** | Según lo que el usuario vio, sugiere el siguiente tema |
| **Generación de ejercicios** | Crea actividades personalizadas según tema y nivel |
| **Explicaciones alternativas** | Si el video no quedó claro, la IA explica con otras palabras |

**Prompt que usa la IA internamente (explicar tema):**

```javascript
const prompt = `
 Materia: ${materia}
 Tema: ${tema}
 Edad del usuario: ${edad}
 Explicá el tema de forma CLARA y SENCILLA.
 Usá ejemplos de la vida cotidiana de Argentina.
 Al final, hacé 2 preguntas cortas para que el usuario compruebe si entendió.
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
| **Los videos no se ven** | En la versión inicial son ejemplos de YouTube. Verificar conexión a internet |
| **El progreso se pierde** | Verificar que localStorage esté habilitado |
| **La IA da respuestas incorrectas** | El prompt está enfocado en temas escolares. Si ocurre, reportar para ajustar |
| **No se genera el APK** | Probar con otra URL o usar [bubblewrap.dev](https://bubblewrap.dev/) |

----------

## 🎯 Frase para la defensa

> _"Usando solo Replit desde el navegador, con IA gratuita de Hugging Face, construimos una app de apoyo escolar gratuito para estudiantes de secundaria. Videos por materia, asistente IA que responde dudas y genera ejercicios personalizados, y seguimiento del progreso. Todo gratis, pensado para la currícula de Buenos Aires."_

----------

## 👥 Autores

Proyecto estudiantil - [Nombre del curso/institución]

## 📄 Licencia

MIT
