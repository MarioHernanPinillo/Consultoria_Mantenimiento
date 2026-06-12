# Arquitectura y Diccionario de Datos Estructural (ISO 14224)

Este documento establece el plano de ingeniería de datos para las tablas base alojadas en Google Sheets. Su cumplimiento estricto previene la corrupción de datos relacionales en la aplicación móvil.

## 1. Jerarquía Taxonómica Aplicada
El modelo de datos absorbe los niveles sugeridos por la norma ISO 14224 para la gestión de datos de confiabilidad:
* **Nivel 3 (Sistemas de Planta):** Ubicaciones Técnicas / Áreas Operacionales.
* **Nivel 5 (Clase de Equipo):** Tipologías estandarizadas de activos.
* **Nivel 6 (Unidad de Equipo):** El activo individual con su placa/TAG.
* **Nivel 8 (Subsistema / Componente):** Elementos mantenibles con modos de falla propios.

---

## 2. Especificación Técnica de Tablas

### Tabla 1: T01_Ubicaciones_Tecnicas
Establece las fronteras físicas y operacionales de los activos.

* **ID_Ubicacion (Llave Primaria - PK):** * *Tipo:* Texto / Alfanumérico.
  * *Formato:* Máximo 10 caracteres, en mayúsculas, usando guiones como separadores.
  * *Ejemplo:* `PL-NEI-01` (Planta Neiva - Área 01).
* **Nombre_Ubicacion:**
  * *Tipo:* Texto.
  * *Restricción:* No se permiten celdas vacías (*Not Null*).
  * *Ejemplo:* `Estación de Bombeo Principal`.
* **Criticidad_Contexto:**
  * *Tipo:* Texto / Lista de validación.
  * *Valores permitidos:* `ALTA`, `MEDIA`, `BAJA`.

### Tabla 2: T02_Clase_Equipo
Catálogo maestro que estandariza las familias de activos para análisis estadísticos homogéneos.

* **ID_Clase (Llave Primaria - PK):**
  * *Tipo:* Texto.
  * *Formato:* Prefijo `EQ-` seguido de tres letras descriptivas.
  * *Ejemplo:* `EQ-TRA` (Transformadores), `EQ-MOT` (Motores Eléctricos).
* **Nombre_Clase:**
  * *Tipo:* Texto.
  * *Ejemplo:* `Transformador de Potencia`.

### Tabla 3: T03_Inventario_Activos
El registro maestro de activos individuales. Almacena la hoja de vida técnica.

* **ID_Activo (Llave Primaria - PK):**
  * *Tipo:* Texto.
  * *Restricción:* Alfanumérico único (TAG físico del equipo).
  * *Ejemplo:* `TRA-002`.
* **ID_Ubicacion (Llave Foránea - FK):**
  * *Tipo:* Texto.
  * *Restricción:* Debe existir previamente en `T01_Ubicaciones_Tecnicas`.
* **ID_Clase (Llave Foránea - FK):**
  * *Tipo:* Texto.
  * *Restricción:* Debe existir previamente en `T02_Clase_Equipo`.
* **Fecha_Instalacion:**
  * *Tipo:* Fecha (Date).
  * *Formato:* `AAAA-MM-DD`.
* **Estado_Operativo:**
  * *Tipo:* Texto / Lista de validación.
  * *Valores permitidos:* `OPERATIVO`, `EN_FALLA`, `RESERVA`, `BAJA`.

### Tabla 4: T04_Componentes_Mantenibles
Unidades de intercambio críticas asociadas a un activo específico.

* **ID_Componente (Llave Primaria - PK):**
  * *Tipo:* Texto / Correlativo único.
  * *Ejemplo:* `CMP-0081`.
* **ID_Activo (Llave Foránea - FK):**
  * *Tipo:* Texto.
  * *Restricción:* Vinculado directamente a `T03_Inventario_Activos`.
* **Nombre_Componente:**
  * *Tipo:* Texto.
  * *Ejemplo:* `Devanado Primario`, `Rodamiento Libre`, `Sello Mecánico`.
