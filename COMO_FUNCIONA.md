# Replit, APIs, Hugging Face y localStorage
## Quién corre, quién piensa, quién transporta y quién recuerda

> Entendé el rol de cada componente en tu proyecto de IA.

---

## 📌 Introducción

En tu proyecto de IA hay cuatro tecnologías que trabajan juntas:

- Replit
- Una API
- Hugging Face (con un modelo como Phi-3)
- localStorage o Supabase

Es normal confundirlas al principio. Todas participan en la app, varias están en internet, y todas reciben o envían información.

**Esta guía tiene un solo objetivo:** que entiendas el rol de cada una y nunca más las mezcles.

---

## 🍽️ La analogía del restaurante (guardala)

| Componente | Rol en el restaurante | Rol en el proyecto |
|------------|----------------------|-------------------|
| Replit | El local y la cocina | Donde **corre** la aplicación |
| API | El mozo | **Transporta** pedidos y respuestas |
| Hugging Face + Modelo | El chef | **Genera** respuestas con IA |
| localStorage / Supabase | La heladera | **Recuerda** / guarda información |
| Vos | El cliente | Usás la aplicación |

---

# 1. REPLIT — "El local"

## ¿Qué es?

Un entorno de desarrollo en la nube. Escribís código y ejecutás tu aplicación desde el navegador.

## ¿Qué hace?

- Ejecuta la aplicación
- Muestra la interfaz web (botones, textos, avatares)
- Guarda variables secretas (como el token de Hugging Face)
- Genera una URL pública para probar la app
- Conecta los distintos servicios (API, localStorage)

## ¿Qué NO hace?

- ❌ No genera respuestas de IA (eso es el modelo)
- ❌ No guarda automáticamente tus datos (eso es localStorage)
- ❌ No es una base de datos

## Importante

**Replit no es obligatorio.** También podrías usar Vercel, Netlify, un servidor propio o tu propia computadora. Lo importante es que **alguien ejecute la aplicación**.

### Frase para recordar

> **Replit es donde vive la app.**

---

# 2. API — "El mozo"

## ¿Qué es?

API significa *Application Programming Interface*.

En criollo: **un mecanismo que permite que dos sistemas se comuniquen**.

## ¿Qué hace?

- Lleva tu pedido desde la aplicación hasta el modelo
- Trae la respuesta desde el modelo hacia la aplicación
- Transporta datos entre sistemas

## Ejemplo concreto
App (Replit) → API → "Dividí la tarea 'Estudiar Matemática'"
↓
Hugging Face (Phi-3)
↓
API → App ← "Pasos: 1. Repasar ecuaciones, 2. Hacer ejercicios..."

text

## ¿Qué NO hace?

- ❌ **No piensa.** La API no entiende lo que transporta. Es como el mozo que lleva un plato sin saber la receta.
- ❌ No guarda datos
- ❌ No muestra pantallas

## En tu proyecto

La API es la que provee **Hugging Face** para comunicarse con sus modelos.

### Frase para recordar

> **La API transporta información. Sin ella, Replit y Hugging Face no se entenderían.**

---

# 3. HUGGING FACE Y LOS MODELOS — "El chef"

## ¿Qué es Hugging Face?

Una plataforma que aloja **miles de modelos** de inteligencia artificial.

## ¿Qué es Phi-3-mini?

**Un modelo específico** dentro de Hugging Face. Es el que usa AlanApp.

### Analogía

| Concepto | Analogía |
|-----------|-----------|
| Hugging Face | Una escuela de chefs |
| Phi-3-mini | Un chef de esa escuela |
| Llama | Otro chef |
| Mistral | Otro chef |

> **Hugging Face es el lugar. Phi-3 es uno de los modelos que viven ahí.**

## ¿Qué hace el modelo?

- Analiza el prompt (el texto que le mandás)
- Genera texto nuevo a partir de lo que aprendió
- Produce respuestas (pasos, mensajes, planes de estudio)

## ¿Qué NO hace?

- ❌ No muestra botones ni dibuja la interfaz
- ❌ No recuerda conversaciones por sí solo (cada llamado es independiente)
- ❌ No guarda tus datos

### Frase para recordar

> **El modelo piensa. Hugging Face es la biblioteca donde vive el modelo.**

---

# 4. LOCALSTORAGE Y SUPABASE — "La heladera"

## ¿Qué son?

### localStorage
Memoria persistente **dentro de tu navegador**. Solo vos tenés la tuya.

### Supabase
Base de datos en la nube. Se puede compartir entre varios usuarios.

## ¿Qué hacen?

- Guardan tus datos (nombre, materias, tareas, progreso)
- Conservan información entre sesiones
- Te permiten recuperar tu trabajo anterior al volver a abrir la app

## Diferencias clave

| Característica | localStorage | Supabase |
|----------------|--------------|----------|
| **Ubicación** | En tu navegador | En la nube |
| **Compartido** | No (solo vos) | Sí (varios usuarios) |
| **Necesita internet?** | No para leer/escribir | Sí |
| **Se borra solo?** | No (a menos que limpies datos) | No |
| **Cambia de dispositivo** | No viaja | Sí, está en la nube |

## Aclaración importante

localStorage **conserva la información aunque cierres la aplicación**.

Pero:
- Puede borrarse si limpiás los datos del navegador
- Puede perderse si cambiás de dispositivo

### Frase para recordar

> **localStorage recuerda. Supabase también, pero en la nube.**

---

# 🔄 El flujo completo (paso a paso)
```text
Vos
│ (escribís "Estudiar Matemática" y hacés clic)
▼
Replit
│ (arma el prompt: "Dividí esta tarea...")
▼
API de Hugging Face
│ (envía HTTP request + token)
▼
Hugging Face (modelo Phi-3-mini)
│ (el modelo piensa y genera la respuesta)
▼
API de Hugging Face
│ (devuelve la respuesta en formato JSON)
▼
Replit
│ (muestra los pasos en pantalla)
│ (guarda la tarea en localStorage)
▼
Vos (ves los pasos generados)
```


---

# 📊 Tabla definitiva

| Pregunta | Replit | API | Hugging Face / Modelo | localStorage |
|----------|--------|-----|----------------------|--------------|
| **¿Qué es?** | Entorno de ejecución | Canal de comunicación | IA generativa | Memoria persistente |
| **¿Qué hace?** | Corre la app | Transporta datos | Genera respuestas | Guarda datos |
| **¿Piensa?** | No | No | ✅ Sí | No |
| **¿Guarda información?** | No | No | No | ✅ Sí |
| **¿Muestra pantallas?** | ✅ Sí | No | No | No |
| **Necesita internet?** | Sí (para cargar) | Sí | Sí | No |

---

# 🎯 Frase para memorizar

> **Replit corre la app, la API transporta, Hugging Face piensa y localStorage recuerda.**


---

# ❌ Errores comunes (y por qué están mal)

| Frase que escuchaste | Corrección |
|----------------------|------------|
| "Hugging Face guarda mis datos" | ❌ No. HF solo procesa texto. Quien guarda es localStorage o Supabase. |
| "Replit piensa con IA" | ❌ No. Replit solo ejecuta el código. Quien piensa es el modelo. |
| "localStorage ejecuta código" | ❌ No. Solo guarda strings. |
| "La API genera respuestas" | ❌ No. La API solo transporta. Quien genera es el modelo. |
| "Phi-3 y Hugging Face son lo mismo" | ❌ No. HF es la plataforma, Phi-3 es un modelo dentro de ella. |

---

# 📚 Resumen rápido

| Concepto | Definición en una línea |
|----------|------------------------|
| **Replit** | IDE en la nube que ejecuta y aloja tu aplicación web. |
| **API** | Mecanismo de comunicación entre sistemas (el "mozo"). |
| **Hugging Face** | Plataforma que aloja miles de modelos de IA. |
| **Phi-3-mini** | Modelo de lenguaje específico que genera texto. |
| **localStorage** | Almacenamiento dentro del navegador, persiste entre sesiones. |
| **Supabase** | Backend y base de datos en la nube. |

---

# 🙋 Preguntas frecuentes

**¿Puedo cambiar Phi-3-mini por otro modelo?**
Sí. Podés usar Llama, Mistral, o cualquier otro alojado en Hugging Face.

**¿Puedo usar Vercel en lugar de Replit?**
Sí. También Netlify, Render, o tu propia computadora.

**¿Puedo usar Supabase en lugar de localStorage?**
Sí. La diferencia es que Supabase permite múltiples usuarios y acceso desde cualquier dispositivo.

**¿Puede funcionar la app sin la API?**
No. La API es el canal de comunicación. Sin ella, Replit no puede hablar con Hugging Face.

**¿Puede funcionar la app sin IA?**
Sí, pero perdería las funcionalidades inteligentes. Usaría solo los fallbacks locales.

**¿El token es para Replit o para Hugging Face?**
El token es para que **Hugging Face sepa quién está llamando a la API**. Replit solo lo guarda de forma segura.

---

# ✅ La única frase que tenés que recordar

> **Replit corre la app, la API transporta, Hugging Face piensa y localStorage recuerda.**

---

*¿Seguís con dudas? Volvé a leer la analogía del restaurante. Todo vuelve a esa imagen.*
