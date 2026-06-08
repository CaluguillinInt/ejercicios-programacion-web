---
sidebar_label: 'Sentencias de Control'
sidebar_position: 4
---

# Sentencias de Control

## Contexto del ejercicio

Una tienda necesita un sistema de reportes. Según la opción seleccionada, el sistema ejecuta un reporte diferente:

| Opción | Reporte | Sentencias usadas |
|--------|---------|-------------------|
| `'inventario'` | Revisa el stock de cada producto y alerta si está bajo | `switch` + `for` + `if/else` |
| `'ventas'` | Acumula ventas del día hasta alcanzar la meta diaria | `switch` + `while` + `if/else` |
| `'descuentos'` | Aplica descuentos según la categoría de cada producto | `switch` + `for` + `if/else` |

---

## Código completo

```typescript
@Get('SentenciasControl')
sentenciasControl() {
  const opcion: string = 'inventario';

  switch (opcion) {

    // CASO 1 — for + if/else
    case 'inventario': {
      const productos = [
        { nombre: 'Arroz', stock: 3 },
        { nombre: 'Aceite', stock: 20 },
        { nombre: 'Azúcar', stock: 1 },
        { nombre: 'Harina', stock: 15 },
        { nombre: 'Sal', stock: 0 },
      ];

      const reporte: string[] = [];

      for (let i = 0; i < productos.length; i++) {
        const p = productos[i];

        if (p.stock === 0) {
          reporte.push(`❌ ${p.nombre}: SIN STOCK`);
        } else if (p.stock <= 3) {
          reporte.push(`⚠️ ${p.nombre}: Stock bajo (${p.stock} unidades)`);
        } else {
          reporte.push(`✅ ${p.nombre}: Stock OK (${p.stock} unidades)`);
        }
      }

      return { reporte };
    }

    // CASO 2 — while + if/else
    case 'ventas': {
      const meta = 500;
      const ventasPorHora = [80, 120, 60, 200, 90];

      let total = 0;
      let hora = 0;
      const registro: string[] = [];

      while (total < meta && hora < ventasPorHora.length) {
        total += ventasPorHora[hora];
        registro.push(`Hora ${hora + 1}: $${ventasPorHora[hora]} acumulado — Total: $${total}`);
        hora++;
      }

      if (total >= meta) {
        return {
          registro,
          resultado: `✅ Meta alcanzada en hora ${hora} con $${total}`,
        };
      } else {
        return {
          registro,
          resultado: `❌ Meta no alcanzada. Total del día: $${total}`,
        };
      }
    }

    // CASO 3 — for + if/else
    case 'descuentos': {
      const productos = [
        { nombre: 'Leche', categoria: 'lacteos', precio: 1.50 },
        { nombre: 'Pollo', categoria: 'carnes', precio: 5.00 },
        { nombre: 'Pan', categoria: 'panaderia', precio: 0.80 },
        { nombre: 'Queso', categoria: 'lacteos', precio: 3.20 },
        { nombre: 'Res', categoria: 'carnes', precio: 7.00 },
      ];

      const reporte: object[] = [];

      for (const p of productos) {
        let descuento = 0;

        if (p.categoria === 'lacteos') {
          descuento = 0.10;
        } else if (p.categoria === 'carnes') {
          descuento = 0.15;
        } else {
          descuento = 0.05;
        }

        const precioFinal = parseFloat((p.precio * (1 - descuento)).toFixed(2));

        reporte.push({
          producto: p.nombre,
          precioOriginal: p.precio,
          descuento: `${descuento * 100}%`,
          precioFinal,
        });
      }

      return { reporte };
    }

    default:
      return { mensaje: 'Opción no válida' };
  }
}
```

---

## Caso 1 — Reporte de Inventario

> **Sentencias:** `switch` → `for` → `if / else if / else`

### Código del caso

```typescript
case 'inventario': {
  const productos = [
    { nombre: 'Arroz',   stock: 3  },
    { nombre: 'Aceite',  stock: 20 },
    { nombre: 'Azúcar',  stock: 1  },
    { nombre: 'Harina',  stock: 15 },
    { nombre: 'Sal',     stock: 0  },
  ];

  const reporte: string[] = [];

  for (let i = 0; i < productos.length; i++) {
    const p = productos[i];

    if (p.stock === 0) {
      reporte.push(`❌ ${p.nombre}: SIN STOCK`);
    } else if (p.stock <= 3) {
      reporte.push(`⚠️ ${p.nombre}: Stock bajo (${p.stock} unidades)`);
    } else {
      reporte.push(`✅ ${p.nombre}: Stock OK (${p.stock} unidades)`);
    }
  }

  return { reporte };
}
```

### Explicación

El `for` recorre todos los productos uno a uno. En cada iteración, el `if/else` evalúa el nivel de stock y asigna un estado:

| Condición | Estado |
|-----------|--------|
| `stock === 0` | Sin stock |
| `stock <= 3` | Stock bajo |
| Cualquier otro | Stock OK |

### Resultado

```json
{
  "reporte": [
    "⚠️ Arroz: Stock bajo (3 unidades)",
    "✅ Aceite: Stock OK (20 unidades)",
    "⚠️ Azúcar: Stock bajo (1 unidades)",
    "✅ Harina: Stock OK (15 unidades)",
    "❌ Sal: SIN STOCK"
  ]
}
```

---

## Caso 2 — Reporte de Ventas

> **Sentencias:** `switch` → `while` → `if / else`

### Código del caso

```typescript
case 'ventas': {
  const meta = 500;
  const ventasPorHora = [80, 120, 60, 200, 90];

  let total = 0;
  let hora = 0;
  const registro: string[] = [];

  while (total < meta && hora < ventasPorHora.length) {
    total += ventasPorHora[hora];
    registro.push(`Hora ${hora + 1}: $${ventasPorHora[hora]} acumulado — Total: $${total}`);
    hora++;
  }

  if (total >= meta) {
    return {
      registro,
      resultado: `✅ Meta alcanzada en hora ${hora} con $${total}`,
    };
  } else {
    return {
      registro,
      resultado: `❌ Meta no alcanzada. Total del día: $${total}`,
    };
  }
}
```

### Explicación

El `while` sigue acumulando ventas **hora por hora** mientras no se alcance la meta (`$500`) y haya horas disponibles. Tiene dos condiciones de parada:

- `total >= meta` → se alcanzó el objetivo, se detiene.
- `hora >= ventasPorHora.length` → se acabaron las horas del día.

Al terminar el `while`, el `if/else` determina si la meta fue alcanzada o no.

### Resultado

```json
{
  "registro": [
    "Hora 1: $80 acumulado — Total: $80",
    "Hora 2: $120 acumulado — Total: $200",
    "Hora 3: $60 acumulado — Total: $260",
    "Hora 4: $200 acumulado — Total: $460",
    "Hora 5: $90 acumulado — Total: $550"
  ],
  "resultado": "✅ Meta alcanzada en hora 5 con $550"
}
```

---

## Caso 3 — Reporte de Descuentos

> **Sentencias:** `switch` → `for...of` → `if / else if / else`

### Código del caso

```typescript
case 'descuentos': {
  const productos = [
    { nombre: 'Leche',  categoria: 'lacteos',   precio: 1.50 },
    { nombre: 'Pollo',  categoria: 'carnes',    precio: 5.00 },
    { nombre: 'Pan',    categoria: 'panaderia', precio: 0.80 },
    { nombre: 'Queso',  categoria: 'lacteos',   precio: 3.20 },
    { nombre: 'Res',    categoria: 'carnes',    precio: 7.00 },
  ];

  const reporte: object[] = [];

  for (const p of productos) {
    let descuento = 0;

    if (p.categoria === 'lacteos') {
      descuento = 0.10;
    } else if (p.categoria === 'carnes') {
      descuento = 0.15;
    } else {
      descuento = 0.05;
    }

    const precioFinal = parseFloat((p.precio * (1 - descuento)).toFixed(2));

    reporte.push({
      producto: p.nombre,
      precioOriginal: p.precio,
      descuento: `${descuento * 100}%`,
      precioFinal,
    });
  }

  return { reporte };
}
```

### Explicación

El `for...of` recorre directamente cada producto (sin índice). Para cada uno, el `if/else` determina el porcentaje de descuento según su categoría:

| Categoría | Descuento |
|-----------|-----------|
| `lacteos` | 10% |
| `carnes` | 15% |
| Cualquier otra | 5% |

Luego se calcula el precio final aplicando la fórmula: `precio * (1 - descuento)`.

### Resultado

```json
{
  "reporte": [
    { "producto": "Leche",  "precioOriginal": 1.50, "descuento": "10%", "precioFinal": 1.35 },
    { "producto": "Pollo",  "precioOriginal": 5.00, "descuento": "15%", "precioFinal": 4.25 },
    { "producto": "Pan",    "precioOriginal": 0.80, "descuento": "5%",  "precioFinal": 0.76 },
    { "producto": "Queso",  "precioOriginal": 3.20, "descuento": "10%", "precioFinal": 2.88 },
    { "producto": "Res",    "precioOriginal": 7.00, "descuento": "15%", "precioFinal": 5.95 }
  ]
}
```

---

## ¿Qué demuestra este ejercicio?

| Sentencia | Caso | Uso |
|-----------|------|-----|
| `switch` | Todos | Selecciona el reporte a ejecutar según la opción |
| `for` | Inventario | Recorre todos los productos para revisar su stock |
| `if / else if / else` | Inventario y Descuentos | Evalúa condiciones y asigna un resultado por producto |
| `while` | Ventas | Acumula ventas mientras no se cumpla la condición de parada |
| `for...of` | Descuentos | Recorre productos sin necesitar el índice |