# Reporte: Implementación de la Criba de Eratóstenes en Bash

## Descripción General

Este script implementa el algoritmo de la Criba de Eratóstenes en Bash para encontrar todos los números primos hasta un límite especificado por el usuario. La Criba de Eratóstenes es un método clásico y eficiente para calcular números primos menores que un número dado. El algoritmo marca los múltiplos de cada número primo comenzando desde 2, y continúa hasta que todos los múltiplos de los números primos menores que el límite han sido marcados como no primos.

## Descripción del Script

### Estructura del Script

El script consta de las siguientes secciones:

1. **Definición de la función `criba_eratostenes`:**
   - Esta función implementa la lógica de la Criba de Eratóstenes para encontrar números primos.
   - Parámetro: `limite`, el límite superior hasta donde se deben calcular los números primos.

2. **Inicialización del Array `primos`:**
   - Se utiliza un array para representar si un número dado es primo (`1`) o no (`0`).
   - Todos los valores se inicializan en `1` (asumiendo que son primos) al comienzo.

3. **Aplicación de la Criba:**
   - Se itera sobre cada número `i` desde 2 hasta la raíz cuadrada del límite.
   - Si `primos[i]` es `1`, se marcan todos los múltiplos de `i` como `0` (no primos).

4. **Impresión de los Resultados:**
   - Al finalizar, se imprimen todos los números primos hasta el límite especificado.

### Ejecución del Script

El script comienza verificando que se haya pasado un argumento, el cual representa el límite hasta donde se desea calcular los números primos. Si no se proporciona un límite, el script muestra un mensaje de uso y finaliza.

### Llamada a la Función `criba_eratostenes`

Si se proporciona un límite válido, el script llama a la función `criba_eratostenes` con el límite como parámetro, generando la lista de números primos.

### Código del Script

```bash
#!/bin/bash

# Función para implementar la Criba de Eratóstenes
criba_eratostenes() {
    local limite=$1
    local i j

    # Inicializar el array de números primos
    local -a primos
    for ((i=2; i<=limite; i++)); do
        primos[i]=1
    done

    # Aplicar la criba
    for ((i=2; i*i<=limite; i++)); do
        if [ ${primos[i]} -eq 1 ]; then
            for ((j=i*i; j<=limite; j+=i)); do
                primos[j]=0
            done
        fi
    done

    # Imprimir los números primos
    echo "Números primos hasta $limite:"
    for ((i=2; i<=limite; i++)); do
        if [ ${primos[i]} -eq 1 ]; then
            echo -n "$i "
        fi
    done
    echo
}

# Verificar que se ha proporcionado un argumento
if [ $# -eq 0 ]; then
    echo "Uso: $0 <limite>"
    exit 1
fi

# Llamar a la función con el límite proporcionado
criba_eratostenes $1
