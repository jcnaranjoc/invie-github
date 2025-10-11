# Solución al Error de DAX: Operadores && vs &

## Problema

Al intentar usar esta fórmula DAX:

```dax
Ubicación = CONSOLIDADO[Municipio] && ", CALDAS, COLOMBIA"
```

Se obtiene el error:

```
Cannot convert value 'MANIZALES' of type Text to type True/False.
```

## Causa del Error

En DAX, el operador `&&` es un **operador lógico AND** que se usa para operaciones booleanas (verdadero/falso), no para concatenar cadenas de texto.

Cuando intentas usar `&&` con valores de texto como `'MANIZALES'`, DAX espera valores booleanos (TRUE/FALSE) en ambos lados del operador, por lo que genera un error al intentar convertir el texto a un valor booleano.

## Solución

Para **concatenar cadenas de texto** en DAX, debes usar el operador `&` (un solo ampersand):

```dax
Ubicación = CONSOLIDADO[Municipio] & ", CALDAS, COLOMBIA"
```

## Diferencia entre Operadores

### `&` (Concatenación de texto)
- **Uso**: Unir/concatenar cadenas de texto
- **Ejemplo**: `"MANIZALES" & ", CALDAS"` → `"MANIZALES, CALDAS"`
- **Tipo de resultado**: Texto

### `&&` (AND Lógico)
- **Uso**: Operaciones lógicas (evaluar condiciones)
- **Ejemplo**: `[Ventas] > 100 && [Estado] = "Activo"` → `TRUE` o `FALSE`
- **Tipo de resultado**: Booleano (TRUE/FALSE)

## Ejemplos Adicionales

### ✅ Correcto - Concatenación de texto
```dax
Dirección Completa = [Calle] & ", " & [Ciudad] & ", " & [País]
Nombre Completo = [Nombre] & " " & [Apellido]
Código = "COD-" & [ID]
```

### ✅ Correcto - Operador lógico
```dax
Es Válido = [Precio] > 0 && [Stock] > 0
Filtro = [Categoría] = "A" && [Estado] = "Activo"
```

### ❌ Incorrecto - Mezclar operadores
```dax
// Error: Usando && para concatenación
Texto = "Hola" && "Mundo"

// Error: Usando & para lógica
Condición = [A] > 5 & [B] < 10
```

## Otras Alternativas para Concatenación

Además del operador `&`, también puedes usar la función `CONCATENATE`:

```dax
Ubicación = CONCATENATE(CONSOLIDADO[Municipio], ", CALDAS, COLOMBIA")
```

O para múltiples valores, usa `CONCATENATEX`:

```dax
Lista = CONCATENATEX(Tabla, [Columna], ", ")
```

## Resumen

**Para tu caso específico, la solución es:**

```dax
Ubicación = CONSOLIDADO[Municipio] & ", CALDAS, COLOMBIA"
```

Esto concatenará correctamente el valor del municipio (ej: "MANIZALES") con la cadena ", CALDAS, COLOMBIA" para producir "MANIZALES, CALDAS, COLOMBIA".
