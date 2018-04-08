# Iniciando el Workshop: Command Line Apps Parte I

## Antes de comenzar: 
* Configura tu `$GOPATH` y asegura de que tu sistema sabe de él (`echo $GOPATH` no debería retornar vacío)
* Asegúrate de que tu `$GOPATH` está en tu `$PATH` de modo que pueda ser encontrado fuera de tu directorio del proyecto.

## Paquete main y la función main
* Aplicaciones en Go producen un solo ejecutable.
* El `paquete main`  es el único requerido por cualquier programa en Go.
* Una función `main` es requerida como punto de entrada en cualquier programa de Go.
* No puedes `importar` nada desde el paquete `main`, lo que quiere decir que el código que coloques dentro del `package main` no está disponible para ser descargado por otros programas de Go.

Programa ejemplo: https://gobyexample.com/hello-world

**ProTip**: Separa la lógica de lo que tu paquete provee como funcionalidad  de la interfaz que te permite usarla -- en este caso, la CLI.
(Mostrar ejemplo)

### Ejercicio
Vamos a construir un programa que de como salida proverbios, específicamente los provervios de Go (https://go-proverbs.github.io).
Vamos a comenzar bien fácil. Escribe un programa en Go que imprima todos los proverbios en la pantalla de la terminal y que cumpla los siguientes requerimientos: 

* Asegúrate que el programa se pueda construir con `go build`
* Asegúrate que tu programa es instalable con `go install`
* Asegúrate de que puedas localizar el binario en `$GOPATH`
* Asegúrate que tu programa corra desde donde sea en tu sistema.

## Argumentos de Línea de Comandos
Los argumentos de CLI ayudan a que se pueda parametrizar tu programa. Ve y lee lo que hay en https://gobyexample.com/command-line-arguments.

### Ejercicio
Es momento de mejorar el programa, Vamos a pasarle un argumento numérico indicando cuál proverbio mostrar. (ejemplo `proverbio 5`). Debe cumplir los siguientes requerimientos:

* Tomar un argumento numérico y mostrar un solo proverbio, el cuál debe coincidir con la posición del proverbio en la lista.
* Arguemntos no numéricos deben ser rechazados.
* Argumentos no positivos deben ser convertidos a su valor absoluto.
* Argumentos que excedan los límites de la lista deben ser rechazados. (ejemplo: pedir el proverbio 45º cuando hay solamente 19 debería mostrar queja al usuario).

ProTip: Hay una manera difícil de hacer esto (manipulando un string blob para extraer el texto en la posición correcta) y hay una manera fácil el cuál usa slices (https://gobyexample.com/slices). 

## Command Line Flags
Flags son comúnmente usadas para aplicaciones basadas en Interfaz de Línea de Comandos cuando hay la necesidad de especificar opciones (ejemplo: `ls -l` donde el flag `-l` le dice al programa alterar la salida que se hubiese obtenido de otra manera. Ver http://gobyexample.com/command-line-flags para aprender como extraer flags en tu programa.

### Ejercicio
Continuemos construyendo nuestro programa de `proverbios`, vamos a modificarlo para que tome el flag `-f` y un valor indicando un string para buscar en nuestra lista de proverbios. Si lo encuentra, el/los proverbio(s) son listados.

Por ejemplo, `proverbs -f cgo` debería encontrar las dos referencias a `cgo` y retornar:

```
Cgo must always be guarded with build tags.
Cgo is not Go.
```

Requerimientos:
* La búsqueda deber ser insensible a mayúsculas.
* No se retorna nada cuando no hay match

## Variables de Entorno
Cuando necesitas que tu aplicación se comporte de manera diferente dependiendo de su entorno, usas variables de entorno. Ver https://gobyexample.com/environment-variables. `os.Getenv` es usado para obtener valores del entorno mientras que `os.Setenv` es muy útil para configurar/eliminar esas variables (especialmente durante testing).

### Ejercicio
Agrega un nuevo comando a tu programa que, cuando se active, liste todas las variables de entorno encontradas.

## Leyendo Archivos
Es muy común querer leer archivos desde el disco durante la ejecución de tu programas. Usando https://gobyexample.com/reading-files como referencia, vamos hacer nuestro programa de `proverbios` un poco más flexible permitiéndole que cargue su lista de proverbios desde el sistema de archivos en vez de codificarlo directamente en el programa. 

### Ejercicio
Mejora tu programa permitiéndolo checar el entorno para saber si existe la variable de entorno `PROVERBS_FILE`. Si es encontrada, `PROVERBS_FILE` tendrá el path al archivo que contine la lista de proverbios a ser leídos en memoria.

Entonces tu programa debería ser capaz de ejecutar las mismas funciones como lo hizo previamente (ejemplo: escuchar, buscar y mostrar un proverbio específico).

Puedes también o `exportar` tu variable de entorno al shell cuál construirás y ejecetarás tu programa o puedes especificar la variable en el momento de invocación como:

```bash
$ PROVERBS_FILE=/some/path/to/proverbs.txt proverbs -f cgo
```

## Escribiendo Archivos
Así como es común leer archivos directamente del disco, es una práctica común escribir archivos al disco. En el siguiente paso, vamos a mejorar nuestro programa para que escriba los programas que son listados, mostrados o encontrados a un archivo. Puedes usar https://gobyexample.com/writing-files como referencia sobre cómo escribir archivos al disco.

### Ejercicio
Merjora tu programa de `proverbios` de manera que pueda tomas un flag `-o` cuyo argumento es el path al cuál debería ser escrito el resultado de la operación.

Por ejemplo: `proverbs list -o my-proverbs.txt` debería dar como salida el contenido que habría sido escrito a `STDOUT`, pero es realmente escrito a `my-proverbs.txt`.

Observa que se espera el mismo comportamiento de todos los comandos y flags que has estado usado hasta ahora. La única diferencia es que tienes la opción de escribir la salida a disco.

