# Guía: formato de columnas y tarjetas en SharePoint Lists

## 1. Crear la lista

1. En tu sitio: **+ New > List > From Excel**, y sube una tabla con encabezados en la fila 1.
2. Ajusta los tipos de columna:
   - Texto largo (resumen, recomendación): **Multiple lines of text**.
   - Fechas (vigencia, fecha de reporte): **Date and Time**, en formato **Date Only**.
   - Catálogos (tecnología, categoría, revisión, táctica): **Choice**, con los valores escritos exactamente igual en todas las filas.
3. Pulsa **Create**.

**Importante:** SharePoint asigna nombres internos (`field_1`, `field_2`, ...) en el orden en que importa las columnas. Consúltalos en la URL de **List settings > clic en la columna**, donde aparece `Field=field_N`. Si cambias de nombre o reordenas columnas después, los JSON dejan de funcionar.

## 2. Aplicar los chips de columna

Para cada columna: **Column settings > Format this column > Advanced mode**. Borra lo que haya, pega el JSON y pulsa **Save**.

| Columna | Archivo |
|---|---|
| Vigencia | `json/chip-vigencia.json` |
| Revisión | `json/chip-revision.json` |
| Tecnología | `json/chip-tecnologia.json` |
| Categoría | `json/chip-categoria.json` |
| Táctica MITRE | `json/chip-tactica.json` |

El chip de vigencia calcula el estado con la fecha de hoy (Vigente, Por vencer, Vencida, Sin vigencia), así que no necesitas columnas calculadas.

## 3. Vista de tarjetas (Gallery)

1. **+ Add view > Gallery**, con un nombre como "Esta semana".
2. **Edit current view > Columns**: marca todas las columnas que aparecen en la tarjeta.
3. **Format current view > Advanced mode**: pega `json/tarjetas-galeria.json` y guarda.
4. Para mostrar solo lo vigente, en **Edit current view > Filter** usa `Vigencia >= [Today]`.
5. Si la tarjeta sale en blanco, usa `json/tarjetas-galeria-basica.json` y revisa que los nombres `field_N` coincidan con tus columnas.

## 4. Publicar en la página del sitio

1. Abre la página del sitio, pulsa **Edit**.
2. Agrega una web part **List** y elige la vista de tarjetas.
3. Agrega botones para las demás vistas.
4. **Publish**.

## Solución de problemas

- **Tarjeta en blanco:** los nombres `field_N` no coinciden, o la vista no tiene activadas las columnas.
- **Chip sin color:** el valor no está en la lista de elección (revisa mayúsculas y acentos).
- **Fecha con un día de diferencia:** la columna quedó como Date and Time; cámbiala a Date Only.
- **Format current view no aparece:** es posible que el administrador haya restringido el formato personalizado.
