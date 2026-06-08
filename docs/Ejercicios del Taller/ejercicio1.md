---
sidebar_label: 'Variables'
sidebar_position: 1
---

# Variables

## Contexto del ejercicio

Una tienda vende productos y necesita calcular el total a pagar aplicando el IVA. El porcentaje de IVA nunca cambia, pero el precio del producto puede modificarse.

## Código

```typescript
@Get('let-const')
letConst() {

  const iva = 0.15;

  let precio = 100;

  let total = precio + (precio * iva);

  precio = 200;

  let nuevoTotal = precio + (precio * iva);

  return {
    iva,
    precioInicial: 100,
    precioActual: precio,
    totalInicial: total,
    totalActual: nuevoTotal
  };
}
```

## Explicación

### `const iva = 0.15;`
Se utiliza `const` porque el porcentaje de IVA no cambiará durante la ejecución del programa.

### `let precio = 100;`
Se utiliza `let` porque el precio puede modificarse posteriormente.

### `let total = precio + (precio * iva);`
Calcula el total del producto incluyendo el IVA.

### `precio = 200;`
Se modifica el valor de la variable `precio`.

### `let nuevoTotal = precio + (precio * iva);`
Se vuelve a calcular el total utilizando el nuevo precio.

## Resultado

```json
{
  "iva": 0.15,
  "precioInicial": 100,
  "precioActual": 200,
  "totalInicial": 115,
  "totalActual": 230
}
```

## ¿Qué demuestra?

- ✅ Uso de `const`
- ✅ Uso de `let`
- ✅ Operaciones matemáticas
- ✅ Variables y constantes