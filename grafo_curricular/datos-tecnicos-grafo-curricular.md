# Cómo crear un grafo de relaciones curriculares con IA


La idea general es esta:

1. Crear una hoja con los contenidos del currículum.
2. Pedirle a la IA que genere las relaciones en una columna determinada, según los criterios que le des.
3. Pedirle a la IA que genere un **grafo de fuerzas interactivo** a partir de esos datos.

---

## 1. Preparar la hoja de cálculo

Crea una hoja de cálculo de Google con estas columnas:

```text
id | nombre | materia | curso | bloque | resumen | relacionados | tipo_relacion
```

### Qué significa cada columna

| Columna | Función |
|---|---|
| `id` | Código único de cada contenido. No debe repetirse ni tener espacios. |
| `nombre` | Nombre visible del contenido, saber básico, criterio o competencia. |
| `materia` | Materia a la que pertenece. Puede servir para colorear los nodos. |
| `curso` | Curso o año del currículum. |
| `bloque` | Bloque temático o apartado curricular. |
| `resumen` | Explicación breve del contenido. |
| `relacionados` | IDs de otros contenidos conectados. |
| `tipo_relacion` | Tipo de relación entre contenidos. |

Ejemplos de `id`:

```text
bio_1_ecosistemas
mat_2_estadistica
dig_1_hojas_calculo
```

Ejemplo de fila:

```csv
id,nombre,materia,curso,bloque,resumen,relacionados,tipo_relacion
mat_1_estadistica,Estadística básica,Matemáticas,1,Datos,Lectura e interpretación de datos,bio_1_datos;geo_1_graficas,aplicacion
```

---

## 2. Pedir a la IA que genere las relaciones

Una vez tengas los contenidos en la hoja, puedes pedirle a la IA que complete las columnas `relacionados` y `tipo_relacion`.

Lo importante es decirle **con qué criterios debe crear las relaciones**, porque eso definirá el grafo.

Por ejemplo, puedes pedirle que busque relaciones de este tipo:

| Tipo de relación | Significado |
|---|---|
| `prerrequisito` | Un contenido es necesario para comprender otro posterior. |
| `aplicacion` | Un contenido se usa para trabajar o aplicar otro. |
| `continuidad` | Un contenido continúa o amplía otro de otro curso. |
| `contenido_compartido` | Dos materias trabajan un contenido parecido. |
| `relacion_interdisciplinar` | Dos contenidos se pueden conectar en una actividad común. |
| `posible_relacion` | Relación sugerida por la IA, pendiente de revisión docente. |

### Prompt para generar las relaciones

Puedes usar un prompt parecido a este:

> Analiza los contenidos de esta hoja de cálculo y completa las columnas `relacionados` y `tipo_relacion`.
>
> En `relacionados`, escribe los `id` de los contenidos conectados, separados por punto y coma.
>
> En `tipo_relacion`, usa solo una de estas categorías:
>
> - `prerrequisito`
> - `aplicacion`
> - `continuidad`
> - `contenido_compartido`
> - `relacion_interdisciplinar`
> - `posible_relacion`
>
> Crea relaciones solo cuando haya una justificación curricular clara. Evita relaciones demasiado generales. Prioriza conexiones entre materias, entre cursos y entre contenidos que puedan ayudar a detectar continuidad, solapamientos o huecos.
>
> No inventes contenidos nuevos. Usa únicamente los `id` existentes en la hoja.
>
> Si dudas, usa `posible_relacion`.

Conviene revisar después las relaciones propuestas por la IA. La IA puede ayudar a detectar conexiones, pero el criterio docente es necesario para validar el resultado.

---

## 3. Pedir a la IA que genere el grafo

Cuando la hoja ya tenga los contenidos y las relaciones, puedes pedirle a la IA que cree el mapa.

Un **grafo de fuerzas interactivo en un lienzo Canvas** es este tipo de gráfico: simula partículas físicas que se atraen o se repelen. Los nodos relacionados tienden a acercarse y los poco conectados quedan más alejados.

En este caso:

- cada contenido será un **nodo**;
- cada relación será una **línea**;
- la materia puede definir el color del nodo;
- el tipo de relación puede definir el color, grosor o estilo de la línea.

---

## 4. Cómo se verá el tipo de relación

El tipo de relación se puede representar en el grafo mediante el estilo de las líneas.

Por ejemplo:

| Tipo de relación | Representación en el grafo |
|---|---|
| `prerrequisito` | línea azul |
| `aplicacion` | línea verde |
| `continuidad` | línea naranja |
| `contenido_compartido` | línea morada |
| `relacion_interdisciplinar` | línea gris |
| `posible_relacion` | línea discontinua |

También se puede pedir que al hacer clic sobre una línea aparezca una explicación de esa relación, aunque para eso sería mejor añadir una columna extra llamada `justificacion_relacion`.

---

## 5. Prompt para crear el grafo

Puedes usar un prompt como este:

> Crea una página web en un único archivo HTML, sin librerías externas, que genere un grafo de fuerzas interactivo en un lienzo Canvas a partir de los datos de esta hoja de cálculo o de este CSV.
>
> Condiciones:
>
> - Cada fila es un nodo.
> - La columna `id` identifica cada nodo.
> - La columna `nombre` se muestra como etiqueta o al pasar el ratón.
> - La columna `materia` define el color de los nodos.
> - La columna `relacionados` define las conexiones entre nodos. Los IDs están separados por punto y coma.
> - La columna `tipo_relacion` define el color o estilo de las líneas.
> - Debe haber una leyenda para las materias y otra para los tipos de relación.
> - Al hacer clic en un nodo, debe mostrarse un panel lateral con:
>   - nombre
>   - materia
>   - curso
>   - bloque
>   - resumen
>   - nodos relacionados
>   - tipo de relación
> - Debe permitir:
>   - zoom con la rueda del ratón;
>   - arrastrar nodos;
>   - mover el fondo;
>   - resaltar los vecinos del nodo seleccionado;
>   - buscar nodos por nombre;
>   - filtrar por materia y por curso.
>
> El resultado debe ser un único archivo HTML completo, listo para guardar y abrir en el navegador.

---

## 6. Recomendación práctica

No conviene pedir directamente:

```text
Hazme un knowledge graph.
```

Es mejor trabajar por fases:

1. Primero estructurar los datos en Google Sheets.
2. Después pedir a la IA que proponga las relaciones.
3. Revisar las relaciones manualmente.
4. Finalmente pedir el grafo interactivo.

Si usas una versión de ChatGPT con conexión a Drive, como ChatGPT Empresas con el plugin de Drive, la IA puede trabajar directamente sobre la hoja de cálculo. Si no, también se puede hacer exportando la hoja como CSV y pegando los datos en el chat.

---

## 7. Exportar desde Google Sheets

Si necesitas pasar los datos manualmente a la IA:

```text
Archivo → Descargar → Valores separados por comas (.csv)
```

Después abre el archivo CSV, copia el contenido y pégalo en el mensaje.
