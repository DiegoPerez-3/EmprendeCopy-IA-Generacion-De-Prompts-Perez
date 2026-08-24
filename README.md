# EmprendeCopy — Fast Prompting en Acción

**Curso:** 95920 – Inteligencia artificial: Generación de Prompts  
**Alumno:** Diego Javier Pérez  
**Entrega:** Preentrega 2 — Fast Prompting en Acción: Desentrañando la Magia

---

## Introducción

### Nombre del proyecto

**EmprendeCopy**

### Problema a abordar

Muchos pequeños negocios y emprendimientos usan redes sociales para promocionar productos, servicios y ofertas, pero no siempre tienen tiempo o conocimientos de copywriting y diseño para crear publicaciones de forma frecuente.

Armar una publicación no es solamente escribir un texto. También hay que pensar qué comunicar, qué tono usar, cómo adaptar el mensaje al público, qué llamada a la acción incluir y qué tipo de imagen puede acompañarlo.

La idea de EmprendeCopy es ayudar en ese proceso usando Inteligencia Artificial Generativa y técnicas de Prompt Engineering.

### Propuesta de solución

EmprendeCopy parte de algunos datos básicos del negocio:

- tipo de negocio;
- producto o servicio;
- promoción;
- público objetivo;
- plataforma;
- tono;
- objetivo.

Con esa información, el modelo genera:

- un título;
- un copy promocional;
- una llamada a la acción;
- cinco hashtags;
- un prompt visual en inglés para generar una imagen relacionada con la publicación.

En esta segunda entrega decidí probar distintas formas de prompting para ver cuál permite obtener resultados más consistentes.

Primero uso un prompt **zero-shot** como punto de partida y después pruebo una versión **few-shot** con ejemplos previos.

Además, aprovecho la prueba visual realizada en la primera entrega para mostrar cómo se puede revisar un resultado y mejorar el prompt cuando aparece algo que no se había pedido.

### Viabilidad del proyecto

El proyecto es técnicamente viable porque no necesita entrenar un modelo propio ni desarrollar una aplicación completa.

La POC utiliza:

- Python;
- Jupyter Notebook / Google Colab;
- Groq para las consultas de texto;
- una herramienta de generación de imágenes para la parte visual.

El trabajo principal está en diseñar, probar y ajustar los prompts.

También mantuve el alcance limitado a la generación de una publicación promocional, para que el proyecto siga siendo realizable dentro del tiempo del curso.

La API key de Groq no está escrita en la notebook ni en el repositorio. En Google Colab se guarda mediante **Secrets** con el nombre `GROQ_API_KEY`.

---

## Objetivos

### Objetivo general

Demostrar mediante una Jupyter Notebook cómo distintas técnicas de Fast Prompting pueden mejorar la generación de contenido promocional para pequeños negocios.

### Objetivos específicos

- Comparar una prueba zero-shot con una prueba few-shot.
- Ver si los ejemplos ayudan a mantener mejor el formato de salida.
- Generar un copy promocional a partir de datos simples.
- Generar un prompt visual complementario.
- Revisar una prueba de imagen real y proponer una mejora del prompt.
- Evitar consultas innecesarias a la API.
- Dejar una versión final que genere todo lo necesario con una sola consulta de texto.

---

## Metodología

Para la POC usé el mismo caso de ejemplo de la primera entrega: una peluquería femenina con una promoción de coloración.

La notebook sigue este orden:

1. Definir el caso de prueba.
2. Hacer una primera consulta zero-shot.
3. Repetir el mismo caso usando few-shot.
4. Comparar el formato de ambas respuestas con una escala de 0 a 10.
5. Revisar la imagen generada en la primera entrega.
6. Detectar un problema en el prompt visual y proponer una corrección.
7. Armar una versión final optimizada.
8. Comparar cantidad de consultas, tokens y costo aproximado.

La comparación se hace sobre el mismo caso para que el cambio de resultado dependa del prompt y no de usar datos diferentes.

---

## Herramientas y tecnologías

- **Python 3**
- **Jupyter Notebook / Google Colab**
- **Groq Python SDK**
- **Modelo:** `openai/gpt-oss-20b`
- **Zero-shot prompting**
- **Few-shot prompting**
- **Iteración de prompts**
- **Structured Outputs / JSON Schema**
- **Generación de imágenes de ChatGPT** para la prueba visual

### ¿Por qué elegí few-shot?

En EmprendeCopy no alcanza con que el modelo escriba algo creativo. También necesito que la respuesta mantenga una estructura bastante clara.

Por ejemplo:

- título;
- copy;
- CTA;
- hashtags.

Con few-shot puedo mostrarle ejemplos del formato que quiero antes de darle un caso nuevo.

La contra es que los ejemplos hacen que el prompt sea más largo y use más tokens, por eso también comparo ese costo con la mejora que aporta.

---

## Implementación

La implementación principal está en:

[`Preentrega2-DiegoPerez.ipynb`](Preentrega2-DiegoPerez.ipynb)

La notebook contiene:

- configuración segura de la API key;
- función reutilizable para consultar Groq;
- prueba zero-shot;
- prueba few-shot;
- comparación automática del formato;
- prueba visual de la primera entrega;
- propuesta de mejora del prompt de imagen;
- versión final con Structured Outputs;
- cálculo aproximado de tokens y costos;
- opción interactiva para probar otros negocios.

---

## Zero-shot y Few-shot

La primera prueba usa zero-shot.

El modelo recibe los datos de la promoción y la tarea, pero no recibe ejemplos previos.

Después hago la misma prueba con few-shot, agregando dos ejemplos de publicaciones antes del caso nuevo.

La idea no es demostrar que zero-shot “funciona mal”, porque el modelo puede responder correctamente de las dos maneras.

Lo que quiero observar es si few-shot ayuda a mantener mejor el formato y el estilo esperado cuando la solución se reutiliza con distintos negocios.

---

## Escala de evaluación

A partir de la devolución de la primera entrega, incorporé una escala de **0 a 10** para medir la mejora entre las dos configuraciones de prompt con los mismos criterios.

Cada criterio vale 2 puntos:

| Criterio | Máximo | Zero-shot | Few-shot |
|---|---:|---:|---:|
| Respeta la estructura solicitada | 2 | 0 | 2 |
| Devuelve exactamente 5 hashtags | 2 | 0 | 2 |
| El copy tiene como máximo 80 palabras | 2 | 2 | 2 |
| Incluye una CTA clara y accionable | 2 | 2 | 2 |
| No agrega canales, condiciones o datos no proporcionados | 2 | 0 | 2 |
| **Total** | **10** | **4/10** | **10/10** |

El zero-shot genera un contenido válido, pero se aleja de algunas reglas: no usa la estructura indicada, devuelve 10 hashtags y agrega un enlace en la bio/DM que no estaba en los datos originales.

El few-shot respeta mejor las reglas del formato. Por eso, usando esta escala, pasa de **4/10 a 10/10**.

La escala no busca medir cuál texto es más creativo. La uso para comparar de forma más objetiva el cumplimiento de las reglas que necesito para el proyecto.

---

## Prueba texto-imagen e iteración

En la primera entrega generé una imagen para una peluquería a partir de este prompt:

> Professional advertising photograph of a modern women's hair salon, stylish woman with freshly colored glossy hair, elegant minimalist interior, medium close-up composition, warm soft lighting, sophisticated neutral color palette, realistic textures, clean premium aesthetic, empty space for promotional copy, square Instagram composition.

Para esa prueba usé la **herramienta de generación de imágenes de ChatGPT**. La generación visual la hice de forma manual: primero obtengo el prompt y después lo uso en la herramienta de imágenes.

Esto significa que la POC no hace una llamada automatizada adicional a una API de imágenes. Las consultas y costos que comparo corresponden a Groq.

El resultado cumplió bastante bien con la estética buscada, pero agregó el texto:

**“LUMIÈRE HAIR SALON”**

Eso no era lo que quería para la pieza final.

A partir de ese resultado, propuse reforzar el prompt con una instrucción más específica:

> Do not generate letters, words, typography, logos, signs, brand names or readable text anywhere in the image. Keep the left side completely clean and blank for copy to be added later during graphic design.

Este caso me sirvió para mostrar que el prompting también es un proceso de prueba, evaluación y ajuste.

---

## Optimización de consultas

Durante la notebook se hacen varias consultas porque necesito comparar técnicas:

- 1 consulta zero-shot;
- 1 consulta few-shot;
- 1 consulta para la versión final.

Esas tres llamadas forman parte de la demostración.

En un uso real no sería necesario hacer todas esas pruebas cada vez.

La versión final genera en una sola llamada:

- título;
- copy;
- CTA;
- cinco hashtags;
- prompt visual.

El flujo final queda:

**Datos del negocio → 1 consulta a Groq → contenido promocional + prompt visual**

De esta forma se reducen consultas innecesarias.

---

## Costos

La notebook usa los tokens informados por Groq para calcular un costo aproximado de cada prueba.

Para la estimación usé las tarifas consultadas el **23/08/2026** para `openai/gpt-oss-20b`:

- entrada: **USD 0,075 por 1 millón de tokens**;
- salida: **USD 0,30 por 1 millón de tokens**.

Estos valores son solo orientativos y pueden cambiar.

---

## Estructura del repositorio

```text
EmprendeCopy-IA-Generacion-De-Prompts-Perez/
├── README.md
├── Preentrega2-DiegoPerez.ipynb
├── requirements.txt
├── .gitignore
└── assets/
    ├── peluqueria-generada.png
    └── README.md
```

---

## Seguridad

La API key no se guarda en el código.

### En Google Colab

1. Abrir la sección **Secrets**.
2. Crear un secret llamado `GROQ_API_KEY`.
3. Pegar la API key.
4. Dar acceso a la notebook.

### En local

Se puede usar una variable de entorno llamada `GROQ_API_KEY`.

Nunca se debe subir una API key real a GitHub.

---

## Conclusiones

Después de hacer las pruebas, considero que las técnicas vistas en esta etapa mejoran la propuesta de EmprendeCopy.

Zero-shot sirve para obtener una primera respuesta sin ejemplos, mientras que few-shot permite marcar mejor el formato que quiero repetir. Con la escala que agregué, la comparación quedó en **4/10 para zero-shot y 10/10 para few-shot**.

La prueba visual también mostró que el primer resultado no siempre es definitivo y que revisar el resultado permite ajustar el prompt de forma más concreta.

Por último, la versión final deja el flujo simplificado a una sola consulta de texto por publicación, lo que hace que la solución sea más eficiente que repetir varias llamadas cada vez.

---

## Referencias técnicas

- Groq — GPT OSS 20B: https://console.groq.com/docs/model/openai/gpt-oss-20b
- Groq — Structured Outputs: https://console.groq.com/docs/structured-outputs
- Groq — Modelos disponibles: https://console.groq.com/docs/models

**Nota:** los precios mencionados fueron consultados el 23/08/2026 y pueden cambiar.
