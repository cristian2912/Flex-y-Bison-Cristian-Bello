# Flex-y-Bison-Cristian-Bello
# Proyecto de Análisis Léxico con Flex y Bison

## Descripción
Este proyecto contiene una serie de ejemplos progresivos para el desarrollo de analizadores léxicos utilizando Flex, y su integración con Bison para el análisis sintáctico. Los ejemplos van desde un escáner básico hasta una calculadora funcional, pasando por comparaciones con implementaciones manuales.

## Ejemplos incluidos

### 1. Ejemplos básicos de Flex

# cr1-1.l - Escáner simple
- **Descripción**: Primer ejemplo de escáner que reconoce palabras y números.
- **Compilación**:
  ```bash
  flex cr1-1.l
  cc lex.yy.c -lfl 
  ./a.out
  ```
- **Salida esperada**: Muestra palabras y números encontrados en el texto de entrada.

# cr1-2.l - Escáner avanzado
- **Mejoras**: Reconoce operadores y tiene manejo de casos por defecto.
- **Compilación**:
  ```bash
  flex cr1-2.l
  cc lex.yy.c -lfl 
  ./a.out
  ```
- **Salida**: Listado de tokens con sus categorías.

# cr1-3.l - Escáner modular
- **Característica**: Separa lógica de procesamiento en funciones auxiliares.
- **Compilación**: Similar a ejemplos anteriores.

### 2. Comparación con implementación manual

# cr1-4.l - Versión manuscrita
- **Propósito**: Comparar Flex con implementación manual.
- **Hallazgos**: La versión manual es menos flexible con espacios y caracteres inesperados.

### 3. Calculadora con Flex y Bison

#### fb1-5.l y fb1-5.y
- **Funcionalidad**: Calculadora que soporta operaciones básicas.
- **Compilación**:
  ```bash
  bison -d fb1-5.y
  flex fb1-5.l
  cc lex.yy.c fb1-5.tab.c -lfl 
  ./a.out
  ```
- **Extensiones implementadas**:
  - Soporte para números hexadecimales
  - Operadores a nivel de bits (&, |)

## Preguntas y respuestas clave

### 2.1 Manejo de comentarios
- **Problema**: Líneas con solo comentarios no son procesadas.
- **Solución**: Modificar regla para devolver token COMMENT:
  ```lex
  "//".*        { return COMMENT; }
  ```

### 2.6 Contador de palabras en C
  ```
#include <stdio.h>
#include <ctype.h>

int main(void) {
    int c, inword = 0, count = 0;
    while ((c = getchar()) != EOF) {
        if (isspace(c)) {
            inword = 0;
        } else if (!inword) {
            inword = 1;
            count++;
        }
    }
    printf("Palabras: %d\n", count);
    return 0;
}
  ```
- **Implementación alternativa**: Código manual más eficiente pero menos mantenible.
- **Comparación**:
  - **Ventaja**: 15-20% más rápido en archivos grandes
  - **Desventaja**: Difícil de extender y mantener

## Limitaciones conocidas
1. Dificultad para manejar lenguajes con indentación significativa (como Python)
2. Problemas con gramáticas ambiguas
3. La implementación manual es más frágil ante entradas inesperadas

## Requisitos
- Flex (>= 2.6)
- Bison (>= 3.0)
- Compilador C (gcc o clang)

## Uso
Para probar cualquier ejemplo:
```bash
cd src/
flex <archivo>.l
# Para ejemplos con Bison:
bison -d <archivo>.y
cc lex.yy.c [archivo.tab.c si usa Bison] -lfl 
./a.out
```

## Contribuciones
Se aceptan mejoras, especialmente en:
- Manejo de errores
- Soporte para más operadores
- Optimizaciones de rendimiento
