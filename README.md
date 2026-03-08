# Gestor y Dashboard de Comparsas

Aplicación web **100% frontend** para **registrar, importar, editar, filtrar y analizar comparsas** y sus **modalidades discursivas por fase del concurso**, con una capa de **consulta asistida por IA local de Chrome** sobre el subconjunto de datos filtrado.

> No requiere backend ni instalación. Todo funciona desde un único `index.html`.

---

## Qué hace esta herramienta

Este proyecto está pensado para trabajar con datasets culturales o de investigación sobre comparsas de forma visual, rápida y local.

Permite:

- cargar datos desde **CSV**, **XLSX** y **XLS**
- registrar comparsas manualmente desde un formulario
- editar las fases directamente desde la tabla
- guardar cambios automáticamente en `localStorage`
- explorar métricas y gráficos en un dashboard
- aplicar filtros analíticos que afectan tanto a los gráficos como a la IA
- hacer preguntas en lenguaje natural usando la **IA integrada de Chrome**, limitada al dataset filtrado actual

---

## Características principales

### 1) Gestión manual de datos

La pestaña **Datos** incluye un formulario para crear o actualizar registros con estos campos:

- Año
- Comparsa
- Preliminar 1
- Preliminar 2
- Cuartos 1
- Cuartos 2
- Semifinal 1
- Semifinal 2
- Final 1
- Final 2

Además:

- valida que el nombre de la comparsa sea obligatorio
- evita duplicados de **comparsa + año**
- permite limpiar el formulario
- permite vaciar toda la tabla y el almacenamiento local

---

### 2) Tabla editable y búsqueda rápida

La tabla principal permite:

- buscar por **comparsa** o **año**
- editar cada fase directamente desde selectores inline
- abrir una fila en modo edición
- eliminar registros individuales
- visualizar el total de filas y cuántas comparsas tienen final

---

### 3) Persistencia automática en local

La aplicación guarda los cambios automáticamente en `localStorage`, por lo que:

- los datos no se pierden al recargar la página
- no hace falta montar servidor ni base de datos
- cada usuario mantiene su propio dataset local en el navegador

---

### 4) Importación flexible de archivos

#### Formatos admitidos

- `CSV`
- `XLSX`
- `XLS`

#### Importación simple

Admite tablas con encabezados estándar, por ejemplo:

```text
Año
COMPARSAS
Preliminar 1
Preliminar 2
Cuartos 1
Cuartos 2
Semifinal 1
Semifinal 2
Final 1
Final 2
```

#### Importación multihoja

También soporta libros de Excel con hojas por año, por ejemplo:

```text
COMPARSAS 2022
COMPARSAS 2023
COMPARSAS 2024
COMPARSAS 2025
COMPARSAS 2026
```

El importador:

- detecta la tabla útil dentro de hojas complejas
- intenta extraer el año desde el nombre de la hoja
- ignora filas de resumen o bloques estadísticos no relevantes
- consolida todas las hojas en una sola tabla final
- normaliza encabezados irregulares

Ejemplo de alias detectado:

```text
G -> Preliminar 1
```

> **Importante:** al importar un archivo, el dataset actual se reemplaza por el contenido importado.

---

### 5) Normalización de modalidades discursivas

La app normaliza varias formas de entrada para unificar las modalidades y permitir análisis coherentes.

Modalidades disponibles:

- `Lírico`
- `Narrativo`
- `Reflexivo`
- `Lírico / Narrativo`
- `Lírico / Reflexivo`
- `Narrativo / Reflexivo`
- `Lírico / Narrativo / Reflexivo`

También interpreta alias cortos o variantes en mayúsculas, por ejemplo:

- `L` → `Lírico`
- `N` → `Narrativo`
- `R` → `Reflexivo`
- `L/N` → `Lírico / Narrativo`

---

## Dashboard analítico

La pestaña **Dashboard** trabaja siempre sobre el **subconjunto filtrado actual**.

### KPIs incluidos

- Comparsas filtradas
- Registros de fase
- Comparsas con final
- Años detectados
- Estado de filtro activo

### Filtros disponibles

- **Año**
- **Fase máxima** alcanzada
- **Modalidad presente**
- **Tipo de enfoque**: puro o mixto
- **Comparsa contiene**

### Gráficos incluidos

- **Distribución discursiva**
- **Cobertura por fase**
- **Avance máximo por comparsa**
- **Tipo de enfoque**
- **Comparsas por año**

### Hallazgos automáticos

El dashboard genera conclusiones dinámicas como:

- modalidad más frecuente
- fase con más registros informados
- año con más comparsas dentro del filtro
- número de comparsas finalistas
- predominio de enfoques puros o mixtos
- comparsa con más fases informadas

---

## IA local de Chrome

La aplicación incorpora una sección para hacer preguntas sobre los datos mediante la **IA integrada de Chrome**.

### Cómo funciona

La consulta:

1. toma el **dataset filtrado actual**
2. lo convierte a JSON
3. se lo pasa al modelo local del navegador
4. obliga a responder con un JSON estructurado

La IA tiene instrucciones explícitas para:

- usar **solo** los datos recibidos
- no inventar información
- indicar si la pregunta no se entiende
- indicar si no hay base suficiente en el dataset
- devolver evidencia textual breve cuando sí puede responder

### Estados de respuesta previstos

La interfaz contempla varios estados de compatibilidad del modelo local:

- `available`
- `downloading`
- `downloadable`
- `unavailable`
- error de comprobación o de consulta

### Tipos de respuesta de la IA

La respuesta estructurada puede devolver:

- `ok`
- `no_entendido`
- `sin_datos`

### Casos de uso

Ejemplos de preguntas:

- `¿Qué modalidad aparece más en 2026?`
- `¿Cuántas comparsas llegaron a la final?`
- `¿Qué comparsa tiene más fases informadas?`

> **Nota:** esta funcionalidad depende de un navegador Chrome compatible con la API de modelo local. Si el modelo no está disponible, se está descargando o el entorno no lo soporta, la app lo indicará en pantalla.

---

## Tecnologías usadas

- **HTML5**
- **CSS3**
- **JavaScript vanilla**
- **Chart.js** para visualización de gráficos
- **SheetJS / XLSX** para lectura de archivos Excel

Dependencias cargadas por CDN:

```html
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdn.jsdelivr.net/npm/xlsx/dist/xlsx.full.min.js"></script>
```

---

## Estructura del proyecto

```text
.
├── index.html
└── README.md
```

Todo el proyecto vive dentro de un único archivo HTML, lo que facilita:

- compartirlo
- ejecutarlo localmente
- adaptarlo como prototipo
- desplegarlo como página estática

---

## Cómo usarlo

1. Abre `index.html` en tu navegador.
2. Añade registros manualmente o importa un archivo `CSV`, `XLSX` o `XLS`.
3. Revisa y corrige los datos desde la tabla.
4. Usa la pestaña **Dashboard** para analizar el dataset.
5. Aplica filtros para acotar el análisis.
6. Haz preguntas en la sección de IA local de Chrome.
7. Exporta el resultado a CSV si lo necesitas.

---

## Requisitos

### Para la app base

- navegador moderno
- conexión a internet para cargar las librerías desde CDN

### Para la IA local

- una versión de Chrome compatible con la API de modelo local usada por la app
- disponibilidad del modelo en el navegador
- un contexto donde `LanguageModel` esté expuesto

---

## Limitaciones actuales

- No hay backend ni sincronización entre dispositivos.
- Los datos se guardan solo en el navegador actual.
- La importación reemplaza el dataset cargado anteriormente.
- La exportación disponible es solo a **CSV**.
- La función de IA depende de compatibilidad real del navegador y del modelo local.
- En datasets muy grandes, la consulta a la IA puede verse limitada por el tamaño del prompt enviado al modelo.

---

## Ideas de mejora

- exportación a Excel
- importación incremental en lugar de sobrescritura
- comparación entre años
- informes descargables
- guardado de vistas filtradas
- métricas más avanzadas por modalidad y fase
- optimización de consultas IA para datasets grandes

---

## Público objetivo

Este proyecto puede ser útil para:

- investigación cultural
- análisis del carnaval
- proyectos docentes
- prototipos de humanidades digitales
- exploración local de datasets sin backend

---

## Créditos

Este proyecto fue desarrollado con la colaboración de:

Nando Muñoz & Javier Velázquez

---

## Licencia

Proyecto de uso libre para investigación, análisis cultural, estudios del carnaval y prototipado.

Si lo reutilizas o adaptas, es recomendable mantener una referencia al proyecto original o documentar claramente tus cambios.
