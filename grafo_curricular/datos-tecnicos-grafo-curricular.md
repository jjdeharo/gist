# Cómo preparar los datos y pedir a la IA un grafo de relaciones curriculares

## 1. Preparar los datos en Google Sheets

Antes de pedir a la IA que genere el grafo, conviene organizar los contenidos en una hoja de cálculo de Google. La estructura mínima puede ser:

```text
id | nombre | materia | curso | bloque | resumen | relacionados | tipo_relacion
```

### Significado de cada columna

**id**  
Código único para cada elemento. No debe tener espacios.

Ejemplos:

```text
bio_1_ecosistemas
mat_2_estadistica
dig_1_hojas_calculo
```

**nombre**  
Nombre visible del contenido, saber básico, criterio o competencia.

**materia**  
Materia a la que pertenece. Puede usarse para colorear los nodos.

**curso**  
Curso o año del currículum. Permite ver progresiones.

**bloque**  
Bloque temático o ámbito dentro de la materia.

**resumen**  
Descripción breve del contenido.

**relacionados**  
IDs de otros elementos conectados, separados por punto y coma.

Ejemplo:

```text
mat_2_estadistica;dig_1_hojas_calculo
```

**tipo_relacion**  
Tipo de relación entre los contenidos. Puede servir para colorear o cambiar el estilo de las líneas.

Ejemplos:

```text
prerrequisito
aplicacion
continuidad
contenido_compartido
relacion_interdisciplinar
posible_relacion
```

---

## 2. Ejemplo de filas

```csv
id,nombre,materia,curso,bloque,resumen,relacionados,tipo_relacion
mat_1_estadistica,Estadística básica,Matemáticas,1,Datos,Lectura e interpretación de datos,bio_1_datos;geo_1_graficas,aplicacion
bio_1_datos,Datos experimentales,Biología,1,Investigación,Registro e interpretación de resultados,mat_1_estadistica;dig_1_hojas,aplicacion
dig_1_hojas,Hojas de cálculo,Digitalización,1,Tratamiento de datos,Organización y análisis de datos,bio_1_datos;mat_1_estadistica,contenido_compartido
geo_1_graficas,Gráficas climáticas,Geografía,1,Clima,Representación de datos ambientales,mat_1_estadistica,aplicacion
```

---

## 3. Exportar los datos

En Google Sheets:

```text
Archivo → Descargar → Valores separados por comas (.csv)
```

Después se copia el contenido del CSV y se pega en la IA.

---

## 4. Prompt para pedir el grafo

Puedes usar un prompt como este:

> Crea una página web en un único archivo HTML, sin librerías externas, que genere un grafo de fuerzas interactivo en un lienzo Canvas a partir del siguiente CSV.
>
> Condiciones:
>
> - Cada fila del CSV es un nodo.
> - La columna `id` identifica cada nodo.
> - La columna `nombre` se muestra como etiqueta o al pasar el ratón.
> - La columna `materia` define el color de los nodos.
> - La columna `relacionados` define las conexiones entre nodos. Los IDs están separados por punto y coma.
> - La columna `tipo_relacion` define el color o estilo de las líneas.
> - Debe haber una leyenda para las materias y otra para los tipos de relación.
> - Al hacer clic en un nodo, debe abrirse un panel lateral con:
>   - nombre
>   - materia
>   - curso
>   - bloque
>   - resumen
>   - nodos relacionados
>   - tipo de relación
> - Debe permitir:
>   - zoom con la rueda del ratón
>   - arrastrar nodos
>   - mover el fondo
>   - resaltar los vecinos del nodo seleccionado
>   - buscar nodos por nombre
>   - filtrar por materia y por curso
> - El resultado debe ser un solo archivo HTML completo, listo para guardar y abrir en el navegador.
>
> Datos CSV:
>
> ```csv
> [pegar aquí el CSV]
> ```

---

## 5. Cómo se verá el tipo de relación

El tipo de relación no aparece como un nodo, sino como una propiedad de la línea que une dos nodos.

Por ejemplo:

| Tipo de relación | Representación en el grafo |
|---|---|
| `prerrequisito` | línea azul |
| `aplicacion` | línea verde |
| `continuidad` | línea naranja |
| `contenido_compartido` | línea morada |
| `relacion_interdisciplinar` | línea gris |
| `posible_relacion` | línea discontinua |

También se puede pedir que al hacer clic en una línea se muestre una explicación de la relación, aunque eso requiere una estructura de datos algo más detallada.

---

## 6. Recomendación práctica

No conviene pedir directamente:

```text
Hazme un knowledge graph.
```

Es mejor darle a la IA:

1. Una tabla bien estructurada.
2. Una definición clara de qué es cada columna.
3. Una lista concreta de funciones que debe tener el mapa.
4. Un CSV pequeño de prueba antes de usar todo el currículum.

Lo normal es que no salga perfecto a la primera. Conviene trabajar por iteraciones:

1. Primero comprobar que lee bien el CSV.
2. Después comprobar que dibuja los nodos.
3. Luego revisar las conexiones.
4. Después añadir colores, estilos y leyendas.
5. Finalmente añadir filtros, buscador y panel lateral.
