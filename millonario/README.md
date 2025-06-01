# Banco de preguntas en JSON – ¿Quién quiere ser millonario?

Este repositorio contiene archivos JSON con preguntas tipo test organizadas por temas y niveles de dificultad, diseñadas para ser utilizadas en el juego educativo *¿Quién quiere ser millonario?*, desarrollado por Juan José de Haro.

## 📄 Estructura del archivo JSON

Cada archivo contiene un único objeto con dos campos principales:

```json
{
  "tema": "Nombre del tema de las preguntas",
  "preguntas": [
    {
      "question": "Texto de la pregunta",
      "options": {
        "A": "Primera opción",
        "B": "Segunda opción",
        "C": "Tercera opción",
        "D": "Cuarta opción"
      },
      "correct": "A",
      "difficulty": "easy"
    }
  ]
}
```

### Niveles de dificultad

Cada conjunto debe contener al menos 60 preguntas repartidas equitativamente entre los siguientes niveles:

- `easy` (fácil)
- `medium` (media)
- `hard` (difícil)
- `very-hard` (muy difícil)
- `expert` (experto)

## 📥 Cómo usar estos archivos

Puedes enlazar directamente cualquiera de los archivos JSON desde tu versión del juego mediante la URL del archivo crudo. Por ejemplo, si tu archivo se llama `tema1.json`, puedes usar:

```
https://raw.githubusercontent.com/usuario/repositorio/main/tema1.json
```

Y añadirla a tu juego en la URL así:

```
https://tu-juego/index.html?json=https://raw.githubusercontent.com/usuario/repositorio/main/tema1.json
```

> También puedes subir tus propios archivos al repositorio siguiendo el mismo formato.

## 📂 Archivos disponibles

Cada archivo tiene un nombre descriptivo del tema, por ejemplo:

- `derivadas.json`
- `cinematica.json`
- `genetica.json`

## ✅ Validaciones

- Todas las preguntas deben tener exactamente 4 opciones.
- La opción correcta se indica con la clave `"correct"` y debe coincidir con una de las letras A, B, C o D.
- Cada pregunta debe tener asignado un valor válido en `"difficulty"`.

---

**Repositorio mantenido por** [Juan José de Haro](https://bilateria.org)  
**Laboratorio de aplicaciones educativas**: [https://labia.tiddlyhost.com](https://labia.tiddlyhost.com)  
**Licencia**: [Creative Commons BY-SA](https://creativecommons.org/licenses/by-sa/4.0/)

## Prompt para generar JSON de preguntas – ¿Quién quiere ser millonario?
Utiliza tu IA favorita para crear las preguntas con el prompt que hay a continuación.

````markdown
### Paso 1 – preguntar al usuario

Antes de generar nada, **pregunta al usuario el tema** sobre el que quiere las preguntas.  
Ejemplo:  
> ¿Sobre qué tema quieres que genere las preguntas tipo test? (Ejemplo: cinemática, derivadas, genética…)

### Paso 2 – generar el JSON cuando el usuario dé el tema

#### Estructura requerida

```json
{
  "tema": "Nombre del tema de las preguntas",
  "preguntas": [
    {
      "question": "Texto de la pregunta",
      "options": {
        "A": "Primera opción",
        "B": "Segunda opción",
        "C": "Tercera opción",
        "D": "Cuarta opción"
      },
      "correct": "A",
      "difficulty": "easy"
    }
  ]
}
```

#### Especificaciones obligatorias

1. **`tema`** refleja exactamente el tema indicado.
2. **`preguntas`** contiene **60 preguntas** en un único archivo:  
   - 12 `easy`  
   - 12 `medium`  
   - 12 `hard`  
   - 12 `very-hard`  
   - 12 `expert`
3. Para cada pregunta:  
   - `question`: enunciado claro y directo.  
   - `options`: cuatro claves `A`, `B`, `C`, `D` con respuestas distintas.  
   - `correct`: letra única (`A`, `B`, `C` o `D`) distribuida al azar y de forma equilibrada en todo el conjunto.  
   - `difficulty`: uno de los cinco niveles indicados.

#### Criterios por dificultad

- **easy**: definiciones o cálculos directos.  
- **medium**: interpretación o aplicación básica.  
- **hard**: relaciones técnicas o fórmulas con contexto.  
- **very-hard**: uso riguroso de fórmulas o propiedades menos habituales.  
- **expert**: formulaciones específicas, combinadas o contraejemplos.

#### Formato adicional

- Emplea **LaTeX** en `$…$` o `$$…$$` para fórmulas.  
- Usa unidades SI correctas (`$m/s^2$`, `$kg·m/s$`, `$N·m$`, etc.).  
- Varía los enunciados:  
  - ¿Cuál es…?  
  - ¿Qué se entiende por…?  
  - ¿Cómo se calcula…?  
  - ¿Cuál de las siguientes afirmaciones es falsa?

#### Validaciones obligatorias

- No repitas preguntas ni opciones textualmente.  
- Solo una opción correcta por pregunta.  
- Distribuye aleatoriamente la respuesta correcta entre A, B, C y D.  
- Entrega **todo el JSON en una sola respuesta**, sin fragmentar.  
- **No incluyas comentarios** dentro del JSON; cualquier texto que empiece con `//`, `#` o `/*` lo invalidaría.
````

Más información en README.ms del [proyecto](https://github.com/jjdeharo/millonario).
