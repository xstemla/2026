# 💼 PrimerEmpleoApp - App con IA para jóvenes sin experiencia

## 📌 Antes de empezar

Este archivo es la **guía para humanos**. 
Antes de seguir, asegurate de tener:
- [ ] Una cuenta en **Replit** (gratis, con Google o GitHub)
- [ ] Una cuenta en **Hugging Face** (gratis, para la IA)

> 💡 Todo es gratuito y no necesita instalación en tu computadora.

---
## 🎯 Qué hace esta app
Conecta a jóvenes de 16 a 18 años (con autorización de sus padres) con oportunidades de primer empleo en Mar del Plata. La app incluye:
- Registro con perfil (nombre, edad, intereses)
- Muro con ofertas laborales locales
- Sistema de puntos e insignias por logros
- Asistente IA que ayuda a armar el CV paso a paso
- Recomendador de trabajos según tu perfil
- Consejos para entrevistas

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

> ⚠️ **PrimerEmpleoApp NO necesita Supabase**. Los perfiles, postulaciones y puntajes se guardan en el celular (localStorage).

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
- Registrarte con nombre, edad (16-18), intereses (ej. atención al cliente, ventas)
- Aceptar autorización de padres
- Explorar el muro de ofertas (datos mock)
- Aplicar a una oferta y ver cómo sumás puntos y desbloqueás insignias
- Usar el asistente IA para armar tu CV
- Pedir recomendaciones de trabajos a la IA

### 6. Publicar la app (para generar el APK)
- En Replit, hacer clic en el botón **"Deploy"** (ícono de Vercel)
- Conectar con GitHub y autorizar Vercel
- Vercel te da una URL pública (ej: `https://primer-empleo-app.vercel.app`)

### 7. Generar el APK para instalar en el celular
- Entrar a [pwabuilder.com](https://pwabuilder.com/)
- Pegar la URL que te dio Vercel
- Click en **"Build"** → **"Android"**
- Descargar el archivo `.apk`

### 8. Compartir con los compañeros
- Enviar el `.apk` por WhatsApp o Google Drive
- Cada uno lo instala en su celular
- Empiezan a buscar su primera experiencia laboral

---

## 📱 Cómo se usa en el día a día
| Momento | El usuario hace... | La app hace... |
|--|--|--|
| **Primera vez** | Se registra (nombre, edad, intereses) | Guarda el perfil |
| **Busca trabajo** | Navega el muro de oportunidades | Muestra ofertas filtradas por ciudad |
| **Aplica** | Toca "Aplicar" en una oferta | Registra la postulación y suma puntos |
| **Completa un trabajo** | (El empleador marca como completado)* | Suma puntos y muestra nueva insignia |
| **Quiere armar CV** | Toca "Asistente IA" | IA guía paso a paso |
| **No sabe qué trabajar** | Toca "Recomendarme" | IA sugiere ofertas según perfil |

> 💼 *En la versión MVP, se simula que al "aplicar" la oferta se completa automáticamente para pruebas. En una versión real, un empleador debería confirmar.

---

## 🤖 ¿Dónde usamos IA?
| Ubicación | Qué hace la IA |
|--|--|
| **Asistente para armar CV** | Guía al usuario paso a paso: "Decime tus habilidades...", "Ahora tu experiencia escolar..." |
| **Recomendación de trabajos** | Analiza perfil y sugiere ofertas compatibles |
| **Consejos para entrevistas** | Responde preguntas frecuentes, cómo vestirse, qué decir |
| **Feedback de perfil** | Sugiere mejorar el perfil para tener más chances |

**Prompt que usa la IA internamente (ejemplo para CV):**
```javascript
const prompt = `
 El usuario tiene:
 - Edad: ${edad}
 - Intereses: ${intereses}
 - Habilidades: ${habilidades}
 Ayudalo a armar su primer CV. Decile:
 1. Cómo presentarse
 2. Qué habilidades destacar
 3. Qué decir si no tiene experiencia previa
 Respondé en tono amigable y motivador.
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
| **El registro no permite menores de 16** | Validación incluida en el prompt |
| **No hay ofertas en mi ciudad** | Las ofertas son mock. En versión real, se pueden agregar manualmente |
| **La IA no recomienda bien** | Verificar que el perfil tenga intereses bien definidos |
| **Los puntos no se actualizan** | Revisar que localStorage se esté guardando correctamente |
| **No se genera el APK** | Probar con otra URL o usar [bubblewrap.dev](https://bubblewrap.dev/) |

----------

## 🎯 Frase para la defensa

> _"Usando solo Replit desde el navegador, con IA gratuita de Hugging Face, construimos una app que conecta a jóvenes de 16 a 18 años con su primer empleo. La IA ayuda a armar el CV, recomienda trabajos según el perfil y da consejos para entrevistas. Todo gratis, con sistema de puntos e insignias para motivarlos."_

----------

## 👥 Autores

Proyecto estudiantil - [Nombre del curso/institución]

## 📄 Licencia

MIT
