# Arquitectura de Datos: Estructura Taxonómica (ISO 14224)

Este documento define el esquema relacional de las tablas base en Google Sheets que alimentarán la aplicación de AppSheet, garantizando la integridad de datos desde el nivel de planta hasta el componente.

## 1. Tabla: T01_Ubicaciones_Tecnicas (Nivel 3/4 ISO 14224)
Registra las áreas físicas o procesos lógicos de la planta. Es la tabla padre de la jerarquía.

| Campo | Tipo de Datos | Llave (Key) | Regla de Validación / Origen |
| :--- | :--- | :--- | :--- |
| `ID_Ubicacion` | Texto (Alfanumérico) | **Llave Primaria** | Código único (Ej: `PL-NEI-01`) |
| `Nombre_Ubicacion` | Texto | | Nombre descriptivo (Ej: Planta Inyección) |
| `Criticidad_Planta` | Texto | | Alta / Media / Baja |

## 2. Tabla: T02_Clase_Equipo (Nivel 5 ISO 14224)
Define los tipos genéricos de equipos industriales presentes en la organización.

| Campo | Tipo de Datos | Llave (Key) | Regla de Validación / Origen |
| :--- | :--- | :--- | :--- |
| `ID_Clase` | Texto | **Llave Primaria** | Código de clase (Ej: `EQ-TRA`, `EQ-MOT`) |
| `Nombre_Clase` | Texto | | Transformadores, Motores, Bombas, etc. |

## 3. Tabla: T03_Inventario_Activos (Nivel 6/7 ISO 14224)
El maestro de activos. Contiene la ficha técnica e historial de cada equipo individual.

| Campo | Tipo de Datos | Llave (Key) | Regla de Validación / Origen |
| :--- | :--- | :--- | :--- |
| `ID_Activo` | Texto | **Llave Primaria** | Tag físico del equipo (Ej: `TRA-002`) |
| `ID_Ubicacion` | Texto | *Llave Foránea* | Relación con `T01_Ubicaciones_Tecnicas` |
| `ID_Clase` | Texto | *Llave Foránea* | Relación con `T02_Clase_Equipo` |
| `Marca` | Texto | | Proveedor/Fabricante |
| `Modelo` | Texto | | Especificación del fabricante |
| `Fecha_Instalacion`| Date | | Formato `DD/MM/AAAA` |
| `Estado_Operativo` | Texto | | Operativo / En Falla / En Reserva / Baja |

## 4. Tabla: T04_Componentes (Nivel 8 ISO 14224)
Sub-elementos críticos asociados a un activo que poseen modos de falla propios (unidades de intercambio).

| Campo | Tipo de Datos | Llave (Key) | Regla de Validación / Origen |
| :--- | :--- | :--- | :--- |
| `ID_Componente` | Texto | **Llave Primaria** | Código correlativo único |
| `ID_Activo` | Texto | *Llave Foránea* | Relación con `T03_Inventario_Activos` |
| `Nombre_Componente`| Texto | | Rodamiento, Devanado, Sello Mecánico, etc. |
