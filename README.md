# 📊 Proyecto: Preparación y Modelado de Datos de Ventas (ETL)

## 👤 Autor
* **Nombre:** Paula Florencia Cordero Lapalma

---

## 🎯 Propósito del Ejercicio
Este proyecto simula el rol de un analista de datos junior enfrentándose a un reporte de ventas desorganizado proveniente de un sistema *legacy*. El objetivo principal fue aplicar un proceso completo de **ETL (Extracción, Transformación y Carga)** en Power Query y estructurar un modelo relacional eficiente en Power BI Desktop, garantizando la calidad, integridad y optimización de los datos para la futura construcción de visualizaciones y reportería analítica.

---

## 🛠️ 1. Extracción y Transformación de Datos en Power Query

El archivo fuente `Ventas_export_legacy.xlsx` presentaba desafíos típicos de sistemas heredados: filas vacías, duplicados, inconsistencias de mayúsculas en categorías, fechas como texto y datos de clientes mezclados con los detalles de transacciones. 

### Secuencia de Pasos Aplicados:
1. **Promoción de Encabezados:** Se elevó la primera fila para establecer los nombres correctos de los campos mediante la opción de promoción de datos.
2. **Eliminación de Filas Vacías:** Se descartaron las filas iniciales/finales completamente vacías que no aportaban valor analítico.
3. **Renombrado de Columnas:** Se estandarizaron todos los nombres técnicos originales (`COD_OP`, `COD_CLI`, etc.) a formato **`snake_case`** y en español (`id_operacion`, `id_cliente`, `nombre_cliente`, etc.) para asegurar una lectura intuitiva para los usuarios del negocio.
4. **Corrección de Tipos de Datos:** 
   * Se asignó tipo **Fecha** a las columnas temporales (`fecha_venta`, `fecha_alta_cliente`) para permitir filtros y cálculos de inteligencia de tiempo en DAX.
   * Se configuraron los identificadores y números de contacto (`id_operacion`, `id_cliente`, `telefono_cliente`) como **Texto** para proteger los ceros iniciales y evitar conversiones numéricas no deseadas.
   * Se ajustaron los montos y cantidades a formatos numéricos decimales y enteros.
5. **Limpieza de Duplicados y Nulos:** Se eliminaron las filas duplicadas basándose en la clave única de la operación y se gestionaron los valores nulos para evitar sesgos en las métricas.
6. **Estandarización de Textos:** Se unificaron las variantes de mayúsculas/minúsculas en el campo de canal de ventas (`canal_venta`) para evitar la fragmentación de categorías en los gráficos.

<img width="1910" height="832" alt="Captura de pantalla 2026-10-15 162532" src="https://github.com/user-attachments/assets/4ca0579f-2cb2-41c3-a37d-af7f1dadbb89" />


---

## 🗂️ 2. Normalización y Modelado Dimensional (Esquema en Estrella)

Para cumplir con las mejores prácticas de modelado de datos y evitar la redundancia (anomalías de actualización), se separó la información transaccional de la información de los clientes mediante el siguiente diseño:

* **Dimensión Clientes (`dim_clientes`):** Se duplicó la consulta original, filtrando únicamente los atributos correspondientes al cliente y aplicando la eliminación de duplicados sobre el campo `id_cliente` para garantizar una dimensión única donde cada cliente aparece una sola vez.
* **Tabla de Hechos (`hechos_ventas`):** Se conservó el detalle transaccional de las operaciones eliminando las columnas de datos personales redundantes, manteniendo únicamente la columna `id_cliente` como **clave foránea**.

### Relación en Power BI:
Ambas tablas se conectaron en la vista de modelo de Power BI Desktop mediante una relación de **uno a varios (`1 a *`)** utilizando `id_cliente` como puente, asegurando que los filtros fluyan correctamente desde la dimensión hacia los hechos.

> 📸 **Captura del Modelo Relacional:**

<img width="966" height="582" alt="Captura de pantalla 2026-10-15 162552" src="https://github.com/user-attachments/assets/87587fee-7362-421f-85a9-e3819e67f91b" />

---

## ✅ Conclusión y Criterios de Aceptación
* El archivo se cargó exitosamente en Power BI Desktop sin errores de conversión.
* Se eliminaron por completo las filas vacías y duplicadas.
* El modelo resultante en esquema de estrella optimiza el rendimiento del motor **VertiPaq** y deja los datos listos para el desarrollo de medidas DAX avanzadas y tableros de control ejecutivos.
