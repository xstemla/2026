# 🎓 OrientaApp - App con IA para orientación vocacional

## 📌 Antes de empezar
Este archivo es la **guía para humanos**. 
Antes de seguir, asegurate de tener:
- [ ] Una cuenta en **Replit** (gratis, con Google o GitHub)
- [ ] Una cuenta en **Hugging Face** (gratis, para la IA)

> 💡 Todo es gratuito y no necesita instalación en tu computadora.

---

## 🎯 Qué hace esta app
Ayuda a adolescentes que no saben qué estudiar mediante un test vocacional con IA. La app:
- Ofrece test corto (5 preguntas) o largo (15 preguntas)
- La IA analiza las respuestas y detecta tu perfil
- Recomienda las 3 carreras más adecuadas para vos
- Explica POR QUÉ cada carrera coincide con tu perfil
- Muestra un mapa con universidades cercanas que ofrecen esas carreras
- Permite guardar resultados y compartirlos por WhatsApp
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

> ⚠️ **OrientaApp NO necesita Supabase**. Los resultados del test se guardan en el celular (localStorage). El mapa usa Leaflet (OpenStreetMap), no requiere API key.

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
- Comenzar test corto (5 preguntas)
- Responder según tus gustos (ej. ayudar personas, materias favoritas, etc.)
- Al terminar, esperar que la IA analice y te muestre:
 - Perfil detectado (ej. "Social y empático")
 - Top 3 carreras con explicaciones
- Tocar "Ver en mapa" para ver universidades cercanas
- Guardar resultado y compartir por WhatsApp

### 6. Publicar la app (para generar el APK)
- En Replit, hacer clic en el botón **"Deploy"** (ícono de Vercel)
- Conectar con GitHub y autorizar Vercel
- Vercel te da una URL pública (ej: `https://orienta-app.vercel.app`)

### 7. Generar el APK para instalar en el celular
- Entrar a [pwabuilder.com](https://pwabuilder.com/)
- Pegar la URL que te dio Vercel
- Click en **"Build"** → **"Android"**
- Descargar el archivo `.apk`

### 8. Compartir con los compañeros
- Enviar el `.apk` por WhatsApp o Google Drive
- Cada uno lo instala en su celular
- Empiezan a descubrir qué pueden estudiar

---

## 📱 Cómo se usa en el día a día
| Momento | El usuario hace... | La app hace... |
|--|--|--|
| **Primera vez** | Abre la app y toca "Comenzar test" | Muestra opción de test corto o largo |
| **Responde preguntas** | Elige opciones sobre gustos e intereses | Guarda las respuestas y muestra progreso |
| **Termina el test** | Toca "Ver resultados" | IA analiza y recomienda carreras |
| **Quiere saber más** | Toca una carrera recomendada | Muestra explicación detallada |
| **Ve universidades** | Toca "Ver en mapa" | Mapa con universidades cercanas |
| **Comparte** | Toca "Compartir por WhatsApp" | Abre WhatsApp con sus resultados |

> 🎯 La app ayuda a los adolescentes a encontrar su camino.

---

## 🤖 ¿Dónde usamos IA?
| Ubicación | Qué hace la IA |
|--|--|
| **Análisis de respuestas** | Recibe las respuestas y determina el perfil del usuario |
| **Recomendación de carreras** | Sugiere carreras específicas según el perfil detectado |
| **Explicación personalizada** | Genera un texto que explica POR QUÉ cada carrera es buena para ese usuario |
| **Consejo motivador** | Agrega una frase para alentar al usuario |

**Prompt que usa la IA internamente (test corto):**
```javascript
const prompt = `
 El usuario respondió:
 P1 (actividad atractiva): ${respuesta1}
 P2 (materia favorita): ${respuesta2}
 P3 (descripción de amigos): ${respuesta3}
 P4 (entorno laboral): ${respuesta4}
 P5 (valor en trabajo): ${respuesta5}
 Respondé EXACTAMENTE en este formato:
 Perfil detectado: [2-3 palabras]
 Top 3 carreras: [carrera1, carrera2, carrera3]
 Explicación para carrera1: [texto corto]
 Explicación para carrera2: [texto corto]
 Explicación para carrera3: [texto corto]
 Consejo adicional: [frase motivadora]
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
| **Las recomendaciones son muy genéricas** | Asegurarse de que las preguntas sean específicas (el prompt ya incluye preguntas detalladas) |
| **El mapa no carga** | Verificar que Leaflet esté bien importado. No necesita API key. |
| **El test es muy largo** | El usuario puede elegir test corto (5 preguntas) |
| **La IA no responde** | Verificar que el token `VITE_HF_TOKEN` esté bien copiado. La app tiene fallback local. |
| **No se genera el APK** | Probar con otra URL o usar [bubblewrap.dev](https://bubblewrap.dev/) |

----------

## 🎯 Frase para la defensa

> _"Usando solo Replit desde el navegador, con IA gratuita de Hugging Face, construimos una app de orientación vocacional que ayuda a adolescentes a descubrir qué estudiar. La IA analiza sus gustos, recomienda carreras con explicaciones personalizadas y muestra universidades cercanas en un mapa. Todo gratis, desde el navegador, sin instalar nada."_

----------

## 👥 Autores

Proyecto estudiantil - [Nombre del curso/institución]

## 📄 Licencia
