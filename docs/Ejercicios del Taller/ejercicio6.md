---
sidebar_label: 'Funciones'
sidebar_position: 6
---

# Funciones

## Contexto del ejercicio

Un sistema de utilidades matemáticas necesita demostrar distintos tipos de funciones en TypeScript: una función estándar que suma dos números, una función con parámetros REST que acepta cualquier cantidad de valores, y una función sobrecargada que adapta su comportamiento según los argumentos recibidos.

## Código completo

```typescript
// Función estándar
function sumar(a: number, b: number): number {
  return a + b;
}

// Función con parámetros REST
function sumarVarios(...numeros: number[]): number {
  return numeros.reduce((acumulado, n) => acumulado + n, 0);
}

// Firmas de sobrecarga
function saludar(nombre: string): string;
function saludar(nombre: string, edad: number): string;

// Implementación de la sobrecarga
function saludar(nombre: string, edad?: number): string {
  if (edad !== undefined) {
    return `Hola ${nombre}, tienes ${edad} años`;
  }
  return `Hola ${nombre}`;
}

@Get('funciones')
funciones() {
  return {
    funcionEstandar: sumar(5, 3),
    funcionRest: sumarVarios(10, 20, 30, 40),
    sobrecarga1: saludar('Pedro'),
    sobrecarga2: saludar('Pedro', 22),
  };
}
```

## Resultado

```json
{
  "funcionEstandar": 8,
  "funcionRest": 100,
  "sobrecarga1": "Hola Pedro",
  "sobrecarga2": "Hola Pedro, tienes 22 años"
}
```

---

## Función Estándar

### Código

```typescript
function sumar(a: number, b: number): number {
  return a + b;
}
```

### Uso

```typescript
sumar(5, 3);
```

### Explicación

Es la forma más básica de declarar una función en TypeScript. Recibe dos parámetros tipados como `number` y devuelve su suma. El tipo de retorno `: number` al final de la firma le indica a TypeScript qué tipo de valor debe regresar la función.

| Elemento | Descripción |
|----------|-------------|
| `a: number` | Primer parámetro tipado |
| `b: number` | Segundo parámetro tipado |
| `: number` | Tipo de retorno declarado |
| `return a + b` | Valor que devuelve la función |

### Resultado

```
8
```

---

## Función con Parámetros REST

### Código

```typescript
function sumarVarios(...numeros: number[]): number {
  return numeros.reduce((acumulado, n) => acumulado + n, 0);
}
```

### Uso

```typescript
sumarVarios(10, 20, 30, 40);
```

### Explicación

El operador `...` (REST) permite que la función acepte cualquier cantidad de argumentos. Todos los valores que se pasen se agrupan automáticamente en un array llamado `numeros`.

```typescript
sumarVarios(10, 20, 30, 40);
// numeros = [10, 20, 30, 40]
```

Luego, `.reduce()` recorre ese array acumulando la suma de todos sus elementos, comenzando desde `0`.

| Elemento | Descripción |
|----------|-------------|
| `...numeros` | Agrupa todos los argumentos en un array |
| `number[]` | El array solo acepta valores numéricos |
| `.reduce()` | Recorre el array acumulando la suma |
| `0` | Valor inicial del acumulador |

### Resultado

```
100
```

---

## Sobrecarga de Funciones

### Código

```typescript
// Firmas de sobrecarga
function saludar(nombre: string): string;
function saludar(nombre: string, edad: number): string;

// Implementación
function saludar(nombre: string, edad?: number): string {
  if (edad !== undefined) {
    return `Hola ${nombre}, tienes ${edad} años`;
  }
  return `Hola ${nombre}`;
}
```

### Uso

```typescript
saludar('Pedro');        // Forma 1
saludar('Pedro', 22);   // Forma 2
```

### Explicación

La sobrecarga permite que una función tenga **distintos comportamientos según los argumentos que recibe**. En TypeScript se declaran primero las **firmas de sobrecarga** (sin cuerpo), y luego una única **implementación** que maneja todos los casos.

```typescript
// Firma 1: solo recibe nombre
function saludar(nombre: string): string;

// Firma 2: recibe nombre y edad
function saludar(nombre: string, edad: number): string;

// Implementación: edad es opcional (?)
function saludar(nombre: string, edad?: number): string {
  ...
}
```

El `?` en `edad?` indica que el parámetro es opcional. Dentro de la implementación, se usa `if (edad !== undefined)` para detectar cuál de las dos formas fue llamada.

| Llamada | Comportamiento |
|---------|---------------|
| `saludar('Pedro')` | `edad` es `undefined` → retorna solo el saludo |
| `saludar('Pedro', 22)` | `edad` tiene valor → retorna saludo con edad |

### Resultado

```
"Hola Pedro"
"Hola Pedro, tienes 22 años"
```

---

## ¿Qué demuestra este ejercicio?

| Concepto | Ejemplo | Descripción |
|----------|---------|-------------|
| ✅ Función estándar | `sumar(5, 3)` | Función con parámetros y tipo de retorno definidos |
| ✅ Parámetros REST | `sumarVarios(...numeros)` | Acepta cualquier cantidad de argumentos |
| ✅ Sobrecarga | `saludar(nombre)` y `saludar(nombre, edad)` | Una función con múltiples firmas de comportamiento |
| ✅ `return` | `return a + b` | Devuelve el resultado de la función |
| ✅ Tipado TypeScript | `number`, `string` | Tipos explícitos en parámetros y retornos |