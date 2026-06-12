# Manual de Configuración Lógica en AppSheet

Este documento técnico describe los parámetros de configuración, expresiones de datos y comportamiento de la interfaz de usuario requeridos para el despliegue de la aplicación de mantenimiento.

## 1. Integridad Relacional (Data References)
Para replicar de forma exacta la jerarquía de la norma ISO 14224 dentro de los formularios móviles, las columnas de llave foránea deben configurarse bajo el tipo de datos `Ref` de AppSheet:

1. **En la Tabla `T03_Inventario_Activos`:**
   * Modificar la columna `ID_Ubicacion` de *Text* a **Ref**. En la propiedad *Source Table*, seleccionar `T01_Ubicaciones_Tecnicas`. Activar el parámetro `IsPartOf`.
   * Modificar la columna `ID_Clase` de *Text* a **Ref**. En *Source Table*, seleccionar `T02_Clase_Equipo`.
2. **En la Tabla `T04_Componentes_Mantenibles`:**
   * Modificar la columna `ID_Activo` de *Text* a **Ref**. En *Source Table*, seleccionar `T03_Inventario_Activos`. Activar el parámetro `IsPartOf` (garantiza que si se elimina un activo, sus componentes asociados se remueven en cascada para evitar registros huérfanos).

---

## 2. Ingeniería de Columnas Virtuales (Fórmulas y Lógica)

### Expresión A: Concatenación del Label de Activos
Para evitar que el usuario en campo vea códigos planos, la columna virtual de visualización principal se configura mediante la siguiente expresión:
* **Nombre de la Columna Virtual:** `Activo_Label`
* **Tipo de Datos:** *Show / Text*
* **AppFormula:**
  ```excel
  CONCATENATE([ID_Activo], " - ", [ID_Clase].[Nombre_Clase], " [", [ID_Ubicacion].[Nombre_Ubicacion], "]")
IF(
  TOTALDAYS(TODAY() - [Fecha_Instalacion]) >= 180,
  "⚠️ REQUIERE INSPECCIÓN MAYOR",
  CONCATENATE("OK - ", TOTALDAYS(([Fecha_Instalacion] + 180) - TODAY()), " días restantes")
)
3. Guarda y cierra el archivo (`Ctrl + O`, **Enter**, `Ctrl + X`).

---

## Auditoría Final de la Jornada de Trabajo

Para cerrar con total rigor metodológico, registraremos y subiremos estas dos ingenierías definitivas a tu repositorio remoto en GitHub. Ejecuta la secuencia completa en tu consola Git Bash:

```bash
# 1. Añadir ambos archivos modificados al área de preparación
git add 01_datos_origen/diccionario_datos_iso14224.md 02_aplicacion_appsheet/arquitectura_appsheet.md

# 2. Verificar que están empaquetados para el registro
git status

# 3. Consolidar el commit con un mensaje estructurado de alto nivel
git commit -m "Ingenieria: Estructuracion definitiva del diccionario taxonómico ISO 14224 y manual logico de AppSheet"

# 4. Transferir los datos de forma segura al servidor remoto
git push origin main
