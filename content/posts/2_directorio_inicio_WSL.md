---
title: "Como configurar el directorio de inicio para WSL en la windows terminal"
date: 2023-05-29T15:30:03-05:00
draft: false
tags: ["WSL", "Linux","Ubuntu","Windows terminal","terminal do windows"]
categories: ["Programación"]
showtoc: false #si quiero mostrar el contenido true
---

Trabajando con WSL encontré la nueva windows terminal y se me hizo muy comodo trabajar en ella. Sin embargo, el principal problema que tenia era que cada vez que iniciaba el directorio predeterminado era uno tipo `/mnt/c/Users/`. Esto era molesto dado que constantemente tenia que trasladarme a un directorio dentro de mi home. Para solucionar este problema tenemos que seguir los siguientes pasos.

1. Entramos al archivo de configuración settings.json presionando las siguientes teclas `ctrl + shift + ,`  
2. Dentro de este archivo configuramos la sección `startingDirectory`. Después del código `//wsl$/Ubuntu-20.04` se añade la ubicación que deseamos. En mi caso quiero iniciar dentro de la carpeta `/home/ariascosb/Projects` por tanto debe quedar asi:

~~~
{
"guid": "{07b52e3e-de2c-5db4-bd2d-ba144ed6c273}",
"hidden": false,
"name": "Ubuntu-20.04",
"source": "Windows.Terminal.Wsl",
"startingDirectory" : "//wsl$/Ubuntu-20.04/home/ariascosb/Projects"
},
~~~

**NOTA:** Solo se debe agregar la linea `startingDirectory`, por favor no modifiques nada adicional. Si estas usando otra version de linux cambias el Ubuntu-20.04 por la tuya