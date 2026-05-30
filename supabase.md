# Supabase y los Tipos de Datos
## Por qué tus consultas van a volar (y cuándo no)

> Cuanto más entienda PostgreSQL tus datos, más eficiente podrá trabajar.

---

# 📌 Introducción

Cuando empezamos a usar Supabase solemos enfocarnos en:

- Crear tablas
- Guardar datos
- Hacer consultas

Pero hay una decisión que impacta directamente en el rendimiento de la aplicación:

**Elegir correctamente los tipos de datos.**

No es un detalle menor. Es parte del diseño de la base de datos.

---

# 🧠 La analogía de las cajas

Imaginá una habitación llena de cajas.

## Escenario 1: cajas sin etiquetas

Tenés miles de cajas mezcladas.

Algunas contienen:

- números
- fechas
- textos

Si alguien te pide:

> "Buscá todos los números mayores a 10"

tenés que abrir caja por caja para descubrir qué hay adentro.

Lleva tiempo.

---

## Escenario 2: cajas etiquetadas

Ahora cada caja tiene una etiqueta:

- 🔴 Números
- 🔵 Textos
- 🟢 Fechas

Cuando te piden números mayores a 10:

vas directamente a las cajas correctas.

Mucho más rápido.

---

# 📚 Lo que realmente pasa en Supabase

Supabase utiliza PostgreSQL.

Y PostgreSQL siempre sabe qué tipo tiene cada columna.

Por ejemplo:

```sql
CREATE TABLE tareas (
    id integer,
    titulo text,
    completada boolean,
    creada_en timestamp
);
```

PostgreSQL ya sabe:

- id → número
- titulo → texto
- completada → verdadero o falso
- creada_en → fecha y hora

No necesita adivinar.

---

# ⚠️ El problema real

Los problemas aparecen cuando elegimos mal los tipos.

Por ejemplo:

```sql
CREATE TABLE usuarios (
    edad text
);
```

Y guardamos:

```text
"18"
"25"
"42"
```

Aunque parecen números, PostgreSQL los ve como texto.

Entonces consultas como:

```sql
SELECT *
FROM usuarios
WHERE edad > '20';
```

pueden ser más lentas o requerir conversiones innecesarias.

---

# 🚀 Tipos correctos = más optimización

Cuando usamos el tipo correcto:

```sql
edad integer
```

PostgreSQL puede:

- comparar más rápido
- ordenar más rápido
- realizar cálculos más rápido
- aprovechar mejor los índices

---

# 📊 Comparación simple

| Situación | Resultado |
|------------|------------|
| Números guardados como integer | ✅ Optimizado |
| Números guardados como text | ⚠️ Menos eficiente |
| Fechas guardadas como timestamp | ✅ Optimizado |
| Fechas guardadas como texto | ⚠️ Menos eficiente |
| Verdadero/Falso como boolean | ✅ Optimizado |
| Verdadero/Falso como texto | ⚠️ Menos eficiente |

---

# ⭐ El verdadero héroe: los índices

Muchas personas creen que los tipos de datos son los responsables de toda la velocidad.

No exactamente.

Los tipos ayudan.

Los índices hacen magia.

---

## 📚 Analogía de la biblioteca

Imaginá una biblioteca.

### Los tipos de datos

Son las etiquetas de las estanterías:

- Historia
- Ciencia
- Literatura

Te ayudan a saber dónde buscar.

---

### Los índices

Son el catálogo de la biblioteca.

Te dicen exactamente:

- en qué estante está el libro
- en qué fila
- en qué posición

Sin catálogo:

- recorrés muchos libros

Con catálogo:

- vas directo al que necesitás

---

# 🔥 Ejemplo práctico

Supongamos una tabla con:

```text
100.000 tareas
```

Consulta:

```sql
SELECT *
FROM tareas
WHERE completada = true;
```

---

## Sin índice

PostgreSQL revisa fila por fila.

```text
100.000 registros
↓
100.000 revisiones
```

---

## Con índice

PostgreSQL salta directamente a los registros relevantes.

```text
100.000 registros
↓
solo los necesarios
```

La diferencia puede ser enorme.

En algunos casos:

- 10 veces más rápido
- 100 veces más rápido
- incluso 1000 veces más rápido

---

# 🔧 Ejemplo en AlanApp

Tabla:

```sql
CREATE TABLE tareas (
    id bigint,
    titulo text,
    completada boolean,
    creada_en timestamp
);
```

Consulta:

```sql
SELECT *
FROM tareas
WHERE completada = true
AND creada_en > '2026-01-01';
```

Con tipos correctos e índices:

- PostgreSQL entiende perfectamente los datos
- Puede usar estructuras optimizadas
- Encuentra los resultados rápidamente

---

# 📝 Impacto real en el rendimiento

| Factor | Impacto |
|----------|----------|
| Tipos correctos | ⭐⭐⭐ |
| Índices correctos | ⭐⭐⭐⭐⭐ |
| Consultas bien escritas | ⭐⭐⭐⭐ |
| Menos datos innecesarios | ⭐⭐⭐ |
| Diseño correcto de tablas | ⭐⭐⭐⭐ |

---

# ❌ Error común

Muchos principiantes creen:

> "Después cambio el tipo."

Técnicamente se puede.

Por ejemplo:

```sql
ALTER TABLE usuarios
ALTER COLUMN edad TYPE integer;
```

Pero cuando la tabla ya tiene miles de registros:

- puede llevar tiempo
- puede generar errores
- puede requerir migraciones

Por eso conviene diseñar bien desde el principio.

---

# 🎯 Regla para recordar

> Los tipos correctos le permiten a PostgreSQL entender tus datos.
>
> Los índices correctos le permiten encontrarlos rápido.

---

# 🧪 Ejercicio mental

Imaginá dos diccionarios.

## Diccionario A

Palabras mezcladas al azar.

## Diccionario B

Palabras ordenadas alfabéticamente.

¿En cuál encontrás una palabra más rápido?

En el segundo.

Los índices hacen exactamente eso.

---

# ✅ Conclusión

Definir correctamente los tipos de datos no es un detalle estético.

Es una decisión técnica que ayuda a PostgreSQL a:

- entender los datos
- compararlos correctamente
- ordenarlos eficientemente
- utilizar índices

Y cuando combinás tipos correctos con índices correctos, tus consultas realmente pueden volar.

---

# 📚 Resumen para examen

| Concepto | Definición |
|------------|------------|
| integer | Número entero |
| text | Texto |
| boolean | Verdadero/Falso |
| timestamp | Fecha y hora |
| Índice | Estructura que acelera búsquedas |
| PostgreSQL | Motor de base de datos usado por Supabase |

---

# Frase final

> Tipos correctos para entender los datos.
>
> Índices correctos para encontrarlos rápido.
