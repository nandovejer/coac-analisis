# Gestor y Dashboard de Comparsas

Aplicación web **100% frontend** (HTML + CSS + JavaScript) para **registrar, importar, analizar y visualizar datos de comparsas** y sus **modalidades discursivas por fase del concurso**.

La herramienta permite trabajar tanto con **tablas simples** como con **Excels complejos con múltiples hojas**, como el estudio estadístico de modalidades discursivas del pasodoble.

No requiere backend ni instalación.

---

# Características principales

## 1. Gestor de datos interactivo

Permite introducir y editar datos manualmente desde un formulario.

Campos disponibles:

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

Las modalidades discursivas disponibles son:

- Lírico
- Narrativo
- Reflexivo
- Lírico / Narrativo
- Lírico / Reflexivo
- Narrativo / Reflexivo
- Lírico / Narrativo / Reflexivo

Los cambios se reflejan **automáticamente en la tabla**.

---

# Persistencia local

La aplicación guarda los datos automáticamente en:

```
localStorage
```

Esto permite que:

- los datos **no se pierdan al recargar la página**
- la herramienta funcione **sin servidor**
- cada usuario tenga su **propio dataset local**

---

# Importación de archivos

La aplicación permite importar:

- CSV
- XLSX
- XLS

## Excel simple

Funciona con tablas que contengan columnas como:

```
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

---

## Excel complejo (multihoja)

El sistema detecta automáticamente archivos como:

```
COMPARSAS 2022
COMPARSAS 2023
COMPARSAS 2024
COMPARSAS 2025
COMPARSAS 2026
```

El importador:

- detecta la **tabla real dentro de la hoja**
- ignora bloques de resumen
- ignora tablas estadísticas internas
- extrae el **año desde el nombre de la hoja**
- consolida todas las hojas en **una sola tabla**

También detecta encabezados irregulares.

Ejemplo:

```
G → Preliminar 1
```

---

# Tabla interactiva

La tabla permite:

- editar celdas directamente
- eliminar comparsas
- buscar comparsas
- filtrar por texto
- ordenar automáticamente

Cada cambio se guarda automáticamente.

---

# Exportación

Los datos pueden exportarse como:

```
CSV
```

Incluyendo:

```
Año
Comparsa
Fases del concurso
Modalidad discursiva
```

---

# Dashboard de análisis

La segunda pestaña muestra análisis automáticos.

## KPIs

- Número de comparsas
- Número total de registros de fase
- Comparsas que alcanzan la final
- Años detectados

---

## Gráficos incluidos

### Distribución discursiva

Frecuencia total de:

- Lírico
- Narrativo
- Reflexivo
- combinaciones mixtas

---

### Cobertura por fase

Número de comparsas que tienen datos en:

- Preliminar
- Cuartos
- Semifinal
- Final

---

### Avance máximo

Distribución de comparsas según la fase más alta alcanzada.

---

### Enfoque puro vs mixto

Comparación entre:

- enfoques puros
- enfoques mixtos

---

### Comparsas por año

Distribución del número de comparsas registradas por año.

---

# Insights automáticos

El sistema genera conclusiones automáticas como:

- modalidad más frecuente
- fase con mayor número de registros
- año con mayor número de comparsas
- predominio de enfoques puros o mixtos
- número de comparsas finalistas

---

# Tecnologías utilizadas

- HTML
- CSS
- JavaScript

Bibliotecas externas:

### Chart.js

Para generación de gráficos.

[https://www.chartjs.org/](https://www.chartjs.org/)

### SheetJS (XLSX)

Para leer archivos Excel.

[https://sheetjs.com/](https://sheetjs.com/)

---

# Estructura del proyecto

Ejemplo mínimo:

```
project/
│
├── comparsas_form_dashboard_import_multisheet.html
└── README.md
```

Todo el proyecto funciona dentro de **un único archivo HTML**.

---

# Uso

1. Abrir el archivo HTML en el navegador.
2. Importar un archivo Excel o CSV.
3. Revisar los datos en la tabla.
4. Editar o añadir nuevas comparsas.
5. Abrir la pestaña **Dashboard** para ver el análisis.
6. Exportar los datos si es necesario.

---

# Requisitos

- Navegador moderno
- conexión a internet (para cargar Chart.js y SheetJS desde CDN)

---

# Posibles mejoras futuras

- exportación directa a Excel
- filtros por año en el dashboard
- visualización de evolución temporal
- clustering de estilos discursivos
- exportación automática de informes
- modo comparativo entre años
- visualización de redes semánticas

---

# Licencia

Proyecto de uso libre para:

- investigación
- análisis cultural
- estudios del carnaval
- prototipado de herramientas de análisis discursivo
