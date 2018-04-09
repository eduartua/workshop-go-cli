# Workshop: Command Line Apps Parte II 

# Generado un Proceso
En esta sección, usaremos una de las utilidades de búsqueda más comunes en los sistemas operativos (UNIX-like) `grep` para hacer la búsqueda por ti cuando tu programa es llamado con el flag previamente agregado `-f`.

Tu tarea es pasarle "via shell" el string de búsqueda a la utilidad `grep` en lugar de utilizar tu propia lógica de búsqueda basada en dicho string.

Usa https://gobyexample.com/spawning-processes como guía para este ejercicio.

# Ejecutando Procesos
https://gobyexample.com/execing-processes

# Manejando Señales
https://gobyexample.com/signals

## Salir y Códigos de Salida
Cuando tu programa se finaliza, los usuarios (sysadmins, etc) esperarán que se comporten como cualquier otra utilidad UNIX/Linux. Por lo tanto, desearás que el programa tenga salida de manera limpia y se ejecute como es esperado cunado tu aplicación recive una señal del Sistema Operativo, tal como SIGINT, SIGHUP entre otras.

Example: https://gobyexample.com/exit

La mayoría de las aplicaciones en Go pueden usar `os.Exit(code int)` o algo que implícitamente llame a `os.Exit` como en el caso de `log.Fatal`.

ProTip: Evita usar `os.Exit` o código que llame a `os.Exit` durante pruebas unitarias. Al correr la prueba el proceso simplemente tendrá salida.
