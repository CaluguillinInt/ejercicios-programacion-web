---
sidebar_label: 'Métodos de Arreglos'
sidebar_position: 5
---

# Métodos de Arreglos

## Contexto del ejercicio

Un sistema académico necesita procesar las notas de un grupo de estudiantes: mostrarlas con formato de texto, filtrar a los aprobados, calcular la suma total y obtener el promedio del grupo.

```typescript
const notas = [6, 8, 4, 10, 7, 3, 9];
```

## Código completo

```typescript
@Get('calificaciones')
calificaciones() {
  const notas = [6, 8, 4, 10, 7, 3, 9];

  const notasTexto = notas.map(nota => `Calificación: ${nota}`);

  const aprobados = notas.filter(nota => nota >= 7);

  const suma = notas.reduce((acumulador, nota) => acumulador + nota, 0);

  const promedio = parseFloat(
    (notas.reduce((acumulador, nota) => acumulador + nota, 0) / notas.length).toFixed(2)
  );

  return {
    notasOriginales: notas,
    map: notasTexto,
    filter: aprobados,
    reduce: suma,
    promedio,
  };
}
```

## Resultado

```json
{
  "notasOriginales": [6, 8, 4, 10, 7, 3, 9],
  "map": [
    "Calificación: 6",
    "Calificación: 8",
    "Calificación: 4",
    "Calificación: 10",
    "Calificación: 7",
    "Calificación: 3",
    "Calificación: 9"
  ],
  "filter": [8, 10, 7, 9],
  "reduce": 47,
  "promedio": 6.71
}
```

---

## map() — Transformar cada elemento

### Código

```typescript
const notasTexto = notas.map(nota => `Calificación: ${nota}`);
```

### Explicación

`map()` recorre **todos** los elementos del arreglo y transforma cada uno en un nuevo valor. El arreglo resultante siempre tiene la **misma cantidad de elementos** que el original.

```
[6, 8, 4, 10, 7, 3, 9]
         ↓ map()
[
  "Calificación: 6",
  "Calificación: 8",
  "Calificación: 4",
  "Calificación: 10",
  "Calificación: 7",
  "Calificación: 3",
  "Calificación: 9"
]
```

| Elemento | Descripción |
|----------|-------------|
| `nota` | Cada elemento del arreglo en la iteración actual |
| `` `Calificación: ${nota}` `` | Nuevo valor que reemplaza al original |

### Resultado

```json
[
  "Calificación: 6",
  "Calificación: 8",
  "Calificación: 4",
  "Calificación: 10",
  "Calificación: 7",
  "Calificación: 3",
  "Calificación: 9"
]
```

---

## filter() — Seleccionar elementos

### Código

```typescript
const aprobados = notas.filter(nota => nota >= 7);
```

### Explicación

`filter()` recorre el arreglo y conserva **únicamente los elementos que cumplen la condición**. El arreglo resultante puede tener menos elementos que el original.

```
[6, 8, 4, 10, 7, 3, 9]
         ↓ filter(nota >= 7)
[8, 10, 7, 9]
```

| Nota | ¿Cumple `>= 7`? | ¿Se incluye? |
|------|-----------------|--------------|
| 6 | ❌ | No |
| 8 | ✅ | Sí |
| 4 | ❌ | No |
| 10 | ✅ | Sí |
| 7 | ✅ | Sí |
| 3 | ❌ | No |
| 9 | ✅ | Sí |

### Resultado

```json
[8, 10, 7, 9]
```

---

## reduce() — Acumular en un solo valor

### Código

```typescript
const suma = notas.reduce((acumulador, nota) => acumulador + nota, 0);
```

### Explicación

`reduce()` recorre el arreglo y va **acumulando** un resultado, reduciéndolo todo a **un único valor**. Recibe dos argumentos: la función acumuladora y el valor inicial (`0` en este caso).

```
[6, 8, 4, 10, 7, 3, 9]  →  valor inicial: 0
         ↓ reduce()
0 + 6  = 6
6 + 8  = 14
14 + 4 = 18
18 + 10= 28
28 + 7 = 35
35 + 3 = 38
38 + 9 = 47
```

| Elemento | Descripción |
|----------|-------------|
| `acumulador` | Guarda el resultado parcial de cada iteración |
| `nota` | El elemento actual del arreglo |
| `0` | Valor inicial del acumulador |

### Resultado

```json
47
```

### Promedio con reduce()

Usando el mismo `reduce()` para sumar, luego dividiendo entre la cantidad de elementos:

```typescript
const promedio = parseFloat(
  (notas.reduce((acumulador, nota) => acumulador + nota, 0) / notas.length).toFixed(2)
);
```

```
47 / 7 = 6.714...  →  6.71
```

### Resultado

```json
6.71
```

---

## ¿Qué demuestra este ejercicio?

| Método | Regla práctica | Resultado |
|--------|---------------|-----------|
| ✅ `map()` | **Transformar** → mismo tamaño, nuevo valor por elemento | Arreglo de igual longitud |
| ✅ `filter()` | **Seleccionar** → solo los que cumplen la condición | Arreglo igual o más corto |
| ✅ `reduce()` | **Acumular** → todos los elementos en un único valor | Un solo valor |