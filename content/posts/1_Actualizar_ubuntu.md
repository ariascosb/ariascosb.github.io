---
title: "Mi código bash para actualizar Ubuntu"
date: 2021-05-22T10:43:26-05:00
draft: false
tags: ["WSL", "Linux","Ubuntu","Bash"]
categories: ["Linux"]
---

WSL nos permite tener una distribución linux en windows 10. La nueva version WSL2 mejora el rendimiento notablemente con la version anterior y la he adoptado como entorno de desarrollo en mi dia a dia. Una labor rutinaria y frecuente que se realiza es mantener actualizado el sistema, por eso te quiero mostrar el código bash que utilizo para realizar esta tarea.

                
1. Creamos un script .sh, en mi caso lo llamo ubuntu.sh

~~~bash
nano ubuntu.sh
~~~

2. Ingresamos el siguiente código dentro del script. Este permite actualizar los repositorios, luego los paquetes y finalmente limpiar la cache. Al final siempre se imprime un mensaje de éxito o alerta para avisarnos el estado final del proceso.

~~~bash
#!/bin/bash

update() {

apt-get update;

apt-get upgrade;
    
if [ $? -ne 0 ]; then
    echo "UBUNTU NO SE ACTUALIZO CORRECTAMENTE "
else 
    apt-get autoclean;
    apt-get clean;
    apt-get autoremove
    echo "UBUNTU SE ACTUALIZO CORRECTAMENTE "        
fi
}

update
~~~

3. Añadimos permisos de ejecución.

~~~bash
chmod +x ubuntu.sh
~~~

4. Creamos un alias. Esto nos permitirá ejecutar el script con un nombre personalizado. Iniciamos abriendo el archivo .bashrc

~~~bash
nano ~/.bashrc
~~~

5. Bajamos hasta el final del archivo .bashrc y copiamos la siguiente linea de código. Debes tener cuidado con colocar la ubicación correcta de tu archivo .sh

~~~bash
alias ubuntu="sudo /home/ariascosb/ubuntu.sh"
~~~

En mi caso el nombre personalizado que les estoy dando es ubuntu, pero tu lo puedes cambiar al editar la palabra que esta después de alias y antes del signo igual (=). 

6. Esta todo listo, ahora para ejecutar el script solo bastara con escribir en la terminal el alias (en mi caso: ubuntu) y automáticamente se actualizara nuestra distribución en WSL.

~~~bash
ubuntu
~~~
