# 📊 Proyecto: Preparación y Modelado de Datos de Ventas (ETL)

## 👤 Autor
* **Estudiante:** Paula Florencia Cordero Lapalma
* **Curso:** Data Analytics / Power BI (Coderhouse)

---

## 📂 Estructura del Repositorio y Archivos Entregados
Este repositorio contiene todos los elementos técnicos solicitados por la consigna del proyecto:
* `README.md`: Documentación técnica detallada del proceso ETL y modelado.
* Carpeta de evidencias y capturas del proceso en Power Query y Power BI.
* Archivo fuente procesado y estructurado para el análisis.

---

## ⚙️ Instrucciones de Ejecución y Verificación
Para verificar el funcionamiento y la correcta aplicación de los criterios de la rúbrica, siga estos pasos:
1. **Clonar o descargar** este repositorio en su equipo local.
2. Abrir **Power BI Desktop**.
3. Cargar el archivo de datos correspondiente (`Ventas_export_legacy.xlsx`) o revisar las consultas conectadas.
4. Ingresar al **Editor de Power Query** para visualizar la secuencia de pasos aplicados (Promoción de encabezados, tipado de datos, eliminación de nulos y duplicados).
5. Dirigirse a la vista de **Modelo** en Power BI para comprobar el esquema en estrella y la relación de uno a varios (`1 a *`) establecida a través de la clave foránea `id_cliente`.

---

## 🛠️ 1. Extracción y Transformación de Datos en Power Query

El archivo fuente presentaba desafíos típicos de sistemas heredados: filas vacías, duplicados, inconsistencias de mayúsculas en categorías, fechas como texto y datos de clientes mezclados con transacciones. 

### Secuencia de Pasos Aplicados:
1. **Promoción de Encabezados:** Se elevó la primera fila para establecer los nombres correctos de los campos.
2. **Eliminación de Filas Vacías:** Se descartaron las filas iniciales/finales completamente vacías.
3. **Renombrado de Columnas:** Estandarización de nombres técnicos (`COD_OP`, `COD_CLI`, etc.) a formato **`snake_case`** en español (`id_operacion`, `id_cliente`, etc.).
4. **Corrección de Tipos de Datos:** 
   * Asignación de tipo **Fecha** a las columnas temporales (`fecha_venta`, `fecha_alta_cliente`).
   * Configuración de identificadores y números de contacto (`id_operacion`, `id_cliente`, `telefono_cliente`) como **Texto**.
   * Ajuste de montos y cantidades a formatos numéricos.
5. **Limpieza de Duplicados y Nulos:** Eliminación de filas duplicadas basándose en la clave única de la operación y gestión de nulos.
6. **Estandarización de Textos:** Unificación de mayúsculas/minúsculas en el campo `canal_venta`.

> 📸 **Evidencia del panel de "Pasos Aplicados" en Power Query:**
<img width="1910" height="832" alt="Captura de pantalla 2026-10-15 162532" src="https://github.com/user-attachments/assets/f4698e87-c1f4-4829-bb8e-27fda73e5c98" />

---

## 🗂️ 2. Normalización y Modelado Dimensional (Esquema en Estrella)

Para cumplir con las mejores prácticas de modelado de datos y evitar redundancias:
* **Dimensión Clientes (`dim_clientes`):** Se duplicó la consulta original, filtrando únicamente los atributos del cliente y aplicando eliminación de duplicados sobre `id_cliente`.
* **Tabla de Hechos (`hechos_ventas`):** Se conservó el detalle transaccional eliminando columnas personales redundantes y manteniendo `id_cliente` como **clave foránea**.

### Relación en Power BI:
Ambas tablas se conectaron mediante una relación de **uno a varios (`1 a *`)** utilizando `id_cliente` como puente.

> 📸 **Evidencia del Modelo Relacional:**
<img width="966" height="582" alt="Captura de pantalla 2026-10-15 162552" src="https://github.com/user-attachments/assets/1111da4d-55d1-4509-bd3b-4cf7a9793ba9" />


---

## ✅ Criterios de Aceptación Cumplidos
* El archivo se cargó exitosamente en Power BI Desktop sin errores.
* Se eliminaron por completo las filas vacías y duplicadas.
* El modelo en esquema de estrella optimiza el rendimiento del motor **VertiPaq**.


