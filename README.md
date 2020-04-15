# Prueba para educación
# Reflejo de arranque con Windows 2016 Server y particiones GPT

# Objetivo
- Reflejar un disco de arranque Windows 2016 con particiones GPT de manera que el sistema pueda arrancar,
indistintamente, con cualquiera de los discos.

## ¿Qué necesitamos?
- VirtualBox 6.1
- Una imagen de Windows Server 2016

## Resumen

  El documento transcribe una práctica en la que se duplica el arranque de Windows. Utilizamos dos discos SATA con el mismo tamaño.
  En el primer disco instalamos el Sistema Operativo con las particiones por defecto:
  
![partitionsWindowsServer](https://user-images.githubusercontent.com/22640799/79308990-d7298380-7ef9-11ea-9e28-b6bfd671772a.jpg)

A continuación:
- Creamos las particiones RE, System (EFI) y msr el el segundo disco con Diskpart
- Formateamos la partición RE en NTFS y la EFI con FAT 32
- Reflejamos el volumen C
- Modificamos el almacén BCD añadiéndole las nuevas entradas del disco 1 con bcdedit.exe
- Copiamos el contenido de la partición RE (con robocopy) del disco 0 al disco 1
- Copiamos el contenido de la partición EFI (con robocopy) del disco 0 al disco 1
- Probamos el arranque del disco 1
- Sustituimos el disco 0 por otro con las mismas características que el inicial (SATA 50 GB) 
- Tras comprobar que el sistema arranca con el disco 1 podemos restaurar el disco dañado con el mismo proceso
