📚 BookScraper & SQL Insights

Web Scraping + Modelado Relacional + Análisis SQL

Este proyecto implementa un pipeline completo de datos (End-to-End) que:

Extrae información desde un sitio web real mediante Web Scraping

Limpia y transforma los datos

Los estructura en una base de datos relacional optimizada

El objetivo no es solo obtener datos, sino convertir información no estructurada en conocimiento consultable aplicando principios reales de ingeniería de datos y modelado.

🚀 Qué hace el sistema

El flujo del proyecto se compone de tres etapas:

1. Extracción de datos

Se realiza scraping sobre:

books.toscrape.com

Extrayendo:

Título

Categoría

Precio

Stock

Calificación

El sistema navega automáticamente por:

categorías

paginación

páginas individuales de cada libro

Incluye manejo de errores y reintentos para robustez.

2. Transformación

Los datos recolectados pasan por un proceso de limpieza:

Conversión de precios con Regex

Normalización de calificaciones (texto → valor numérico)

Estandarización de stock

Además:

Se simulan autores

Se generan relaciones complejas

Algunos libros poseen múltiples autores

Esto permite modelar escenarios reales y no solo datos planos.

3. Persistencia Relacional

Los datos se almacenan en una base SQLite estructurada bajo principios de normalización.

Tablas principales:

Libros

Autores

Categorias

Tabla puente:

Libro_Autor

Esta estructura implementa una relación:

Libros (N) ⟷ (M) Autores

🧩 Modelo de Datos

El diseño de la base sigue buenas prácticas de modelado relacional:

Categorias (1) ──── (N) Libros
Libros (N) ──── (M) Autores

Resuelto mediante:

Libro_Autor

El proyecto incluye un Diagrama UML del esquema de base de datos ubicado en:

imagenes/

Esto permite visualizar claramente:

entidades

relaciones

cardinalidades

⚙️ Optimización de Rendimiento

Se implementan índices SQL para mejorar tiempos de consulta.

Ejemplo:

Búsqueda de libros con calificación máxima:

Sin índice → 0.00525 s

Con índice → 0.00201 s

Resultado: reducción superior al 60% en tiempo de lectura.

🔍 Consultas SQL Destacadas

Many-to-Many Join

Obtención de libros por autor:

SELECT a.nombre AS autor, l.titulo AS libro, l.calificacion
FROM Libros l
JOIN Libro_Autor la ON l.id = la.id_libro
JOIN Autores a ON la.id_autor = a.id
ORDER BY a.nombre;

Análisis por Categoría

Promedio de calificación:

SELECT c.nombre AS categoria, AVG(l.calificacion) AS promedio
FROM Categorias c
JOIN Libros l ON c.id = l.id_categoria
GROUP BY c.nombre
ORDER BY promedio DESC;

🛠️ Tecnologías Utilizadas

Python 3.11+

Requests

BeautifulSoup4

SQLite3

JSON

SQL

🧠 Qué demuestra este proyecto

Más allá del scraping, este sistema muestra:

Pipeline de datos real

Limpieza y transformación

Modelado relacional

Implementación de M2M

Uso de índices

Consultas analíticas

Es decir:

pasar de web → a estructura → a análisis.

▶️ Ejecución

Clonar repositorio:

git clone https://github.com/Andylopez-3/Challenge-Web-Scraping-SQL.git


Instalar dependencias:

pip install requests beautifulsoup4


Ejecutar:

Abrir y correr:

Scrapiiing.ipynb

🎯 Enfoque Académico

El proyecto simula un escenario real de ingestión de datos donde:

los datos no nacen limpios
ni estructurados

pero terminan en una base lista para:

análisis

visualización

consultas complejas