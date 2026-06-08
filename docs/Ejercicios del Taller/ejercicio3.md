---
sidebar_label: 'Estructuras de Datos'
sidebar_position: 3
---

# Estructuras de Datos

## Contexto del ejercicio

Una institución educativa necesita almacenar información de estudiantes, materias, usuarios y docentes para su sistema académico.

## Código

### Interface

```typescript
interface Docente {
  nombre: string;
  materia: string;
  experiencia: number;
}
```

### Endpoint

```typescript
@Get('estructurasDatos')
estructurasDatos() {

  const estudiante = {
    nombre: 'Aldair',
    edad: 20,
    carrera: 'Software'
  };

  const materias = [
    'Programación',
    'Base de Datos',
    'Redes'
  ];

  const usuario: [number, string] = [
    1,
    'Administrador'
  ];

  const estado = 'Activo';

  let identificador: number | string = 1001;
  identificador = 'EST-1001';

  let rol: 'Admin' | 'Estudiante' = 'Admin';

  const docente: Docente = {
    nombre: 'Carlos Pérez',
    materia: 'Programación',
    experiencia: 10
  };

  return {
    mensaje: 'Ejemplo de estructuras de datos',
    estudiante,
    materias,
    usuario,
    estado,
    identificador,
    rol,
    docente
  };
}
```

## Explicación

### Interface

```typescript
interface Docente {
  nombre: string;
  materia: string;
  experiencia: number;
}
```

Define la estructura que debe tener un docente. Al usarla con `const docente: Docente`, obliga a que el objeto tenga exactamente las propiedades `nombre`, `materia` y `experiencia`.

### Object

```typescript
const estudiante = {
  nombre: 'Aldair',
  edad: 20,
  carrera: 'Software'
};
```

Representa los datos de un estudiante mediante un objeto.

### Array

```typescript
const materias = [
  'Programación',
  'Base de Datos',
  'Redes'
];
```

Almacena varias materias dentro de una misma variable.

### Tupla

```typescript
const usuario: [number, string] = [
  1,
  'Administrador'
];
```

La primera posición debe contener un número y la segunda un texto.

| Posición | Valor | Descripción |
|----------|-------|-------------|
| `0` | `1` | ID del usuario |
| `1` | `'Administrador'` | Tipo de usuario |

### Enum

```typescript
const estado = 'Activo';
```

Representa el estado actual del usuario.

### Unión

```typescript
let identificador: number | string = 1001;
identificador = 'EST-1001';
```

Puede almacenar números o texto.

### Literal

```typescript
let rol: 'Admin' | 'Estudiante' = 'Admin';
```

Solo permite dos valores posibles: `Admin` o `Estudiante`.

### Interface aplicada

```typescript
const docente: Docente = {
  nombre: 'Carlos Pérez',
  materia: 'Programación',
  experiencia: 10
};
```

Representa los datos de un docente respetando la estructura definida en la interfaz.

## Resultado

```json
{
  "mensaje": "Ejemplo de estructuras de datos",
  "estudiante": {
    "nombre": "Aldair",
    "edad": 20,
    "carrera": "Software"
  },
  "materias": [
    "Programación",
    "Base de Datos",
    "Redes"
  ],
  "usuario": [
    1,
    "Administrador"
  ],
  "estado": "Activo",
  "identificador": "EST-1001",
  "rol": "Admin",
  "docente": {
    "nombre": "Carlos Pérez",
    "materia": "Programación",
    "experiencia": 10
  }
}
```

## ¿Qué demuestra?

| Estructura | Descripción |
|------------|-------------|
| ✅ Interface | Define la forma obligatoria de un objeto |
| ✅ Object | Agrupa datos relacionados de un estudiante |
| ✅ Array | Lista de materias en una sola variable |
| ✅ Tupla | Array con tipos fijos por posición |
| ✅ Enum | Estado predefinido del usuario |
| ✅ Unión | Variable que acepta `number` o `string` |
| ✅ Literal | Variable restringida a valores específicos |