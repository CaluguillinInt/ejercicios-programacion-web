---
sidebar_label: 'Tipos de Datos'
sidebar_position: 2
---

# Tipos de Datos

Una universidad necesita registrar información básica de sus estudiantes para el proceso de matriculación. Cada estudiante tiene nombre, edad, estado de matrícula, código institucional e identificador único.

## Código

```typescript
@Get('estudiante')
registroEstudiante() {

  const nombre: string = 'Carlos Pérez';
  const edad: number = 20;
  const matriculado: boolean = true;
  const codigo: bigint = 20260001n;
  const identificador: symbol = Symbol('EST001');

  return {
    nombre,
    edad,
    matriculado,
    codigo: codigo.toString(),
    identificador: identificador.toString()
  };
}
```

## Explicación

### `const nombre: string = 'Carlos Pérez';`
Tipo `string` para almacenar texto.

### `const edad: number = 20;`
Tipo `number` para almacenar números.

### `const matriculado: boolean = true;`
Tipo `boolean` porque solo puede ser verdadero o falso.

### `const codigo: bigint = 20260001n;`
Tipo `bigint` para números muy grandes.

### `const identificador: symbol = Symbol('EST001');`
Tipo `symbol`, que genera un identificador único.

## Resultado

```json
{
  "nombre": "Carlos Pérez",
  "edad": 20,
  "matriculado": true,
  "codigo": "20260001",
  "identificador": "Symbol(EST001)"
}
```

## ¿Qué demuestra?

| Tipo | Ejemplo |
|------|---------|
| `string` | nombre |
| `number` | edad |
| `boolean` | matriculado |
| `bigint` | codigo |
| `symbol` | identificador |