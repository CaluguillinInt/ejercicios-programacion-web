---
sidebar_label: 'Tipos de Datos'
sidebar_position: 3
---

# Tipos de Datos

## Contexto del ejercicio

Un sistema de automatización requiere evaluar el estado de una condición para decidir qué grupo de datos técnicos mostrar en la interfaz web. El sistema maneja variables lógicas, textos de desarrollo, identificadores únicos, valores numéricos decimales, comodines libres y reportes de seguridad encriptados.

## Código

```typescript
@Get('super-pizarra/:estado')
mostrarTodoLaPizarra(@Param() p) {

  let esVerdadero: boolean = (p.estado == 'true');

  let numeroGrande: bigint = 9007199254740991n;
  let texto: string = "hola desarrollador principal";
  let identificadorUnico: symbol = Symbol("id-flor");

  let precioDolar: number = 18.50;

  let comodinAny: any = "cualquier dato porque fallo el sistema ";
  let secretoUnknown: unknown = "Alerta de sistema";

  let textoSeguro;
  if (typeof secretoUnknown === "string") {
    textoSeguro = secretoUnknown;
  }

  if (esVerdadero == true) {

    return {
      tipo_boolean: esVerdadero,
      tipo_bigint: numeroGrande.toString(),
      tipo_string: texto,
      tipo_symbol: identificadorUnico.toString()
    };

  } else {

    return {
      tipo_boolean: esVerdadero,
      tipo_number: precioDolar,
      tipo_any: comodinAny,
      tipo_unknown: textoSeguro
    };
  }
}
```

## Explicación

### `let esVerdadero: boolean = (p.estado == 'true');`
Tipo `boolean` que almacena un valor lógico verdadero (`true`) o falso (`false`) evaluado desde la URL. Si el parámetro recibido es el texto `'true'`, la expresión devuelve `true`; cualquier otro valor devuelve `false`.

### `let numeroGrande: bigint = 9007199254740991n;`
Tipo `bigint` utilizado para almacenar números enteros extremadamente grandes. Se identifica por la letra `n` al final del valor.

### `let texto: string = "hola desarrollador principal";`
Tipo `string` utilizado para almacenar cadenas de texto o palabras.

### `let identificadorUnico: symbol = Symbol("id-flor");`
Tipo `symbol` que genera un identificador único absoluto en memoria para evitar colisiones entre valores.

### `let precioDolar: number = 18.50;`
Tipo `number` utilizado para almacenar valores numéricos, ya sean enteros o con decimales.

### `let comodinAny: any = "cualquier dato porque fallo el sistema ";`
Tipo `any` que actúa como un comodín dinámico para almacenar cualquier valor sin restricción de tipo.

### `let secretoUnknown: unknown = "Alerta de sistema";`
Tipo `unknown` que almacena un tipo de dato desconocido de forma segura, obligando a una validación previa antes de poder ser utilizado:

```typescript
let textoSeguro;
if (typeof secretoUnknown === "string") {
  textoSeguro = secretoUnknown;
}
```

A diferencia de `any`, `unknown` no permite usar el valor directamente sin antes verificar su tipo con `typeof`.

## Resultados

El endpoint recibe el parámetro `estado` desde la URL y según su valor retorna un grupo diferente de datos.

### Si se envía `true`
> `GET /super-pizarra/true`

```json
{
  "tipo_boolean": true,
  "tipo_bigint": "9007199254740991",
  "tipo_string": "hola desarrollador principal",
  "tipo_symbol": "Symbol(id-flor)"
}
```

### Si se envía `false`
> `GET /super-pizarra/false`

```json
{
  "tipo_boolean": false,
  "tipo_number": 18.5,
  "tipo_any": "cualquier dato porque fallo el sistema ",
  "tipo_unknown": "Alerta de sistema"
}
```

## ¿Qué demuestra?

| Tipo | Variable | Característica |
|------|----------|----------------|
| `boolean` | `esVerdadero` | Solo acepta `true` o `false` |
| `bigint` | `numeroGrande` | Números enteros de gran magnitud, termina en `n` |
| `string` | `texto` | Cadenas de texto |
| `symbol` | `identificadorUnico` | Identificador único irrepetible en memoria |
| `number` | `precioDolar` | Valores numéricos enteros o decimales |
| `any` | `comodinAny` | Acepta cualquier tipo sin restricción |
| `unknown` | `secretoUnknown` | Tipo desconocido que requiere validación previa |