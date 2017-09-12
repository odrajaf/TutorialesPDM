
# Tutorial, VR unity para dispositivos sin giroscopio

[dosCamaras]:https://github.com/odrajaf/TutorialesPDM/blob/master/images/imagen1.png
[confCamara1]:https://github.com/odrajaf/TutorialesPDM/blob/master/images/imagen2.png
[confCamara2]:https://github.com/odrajaf/TutorialesPDM/blob/master/images/imagen3.png

1º Lo más caracteristico del VR, es el uso de una vision estereoscópica para esto lo que haremos en primer lugar será duplicar nuestra camara principal del proyecto.

2º Una vez hecho esto tenemos dos camaras situadas en el mismo lugar y a la que podremos hacer de forma sencilla que le afecten todos los scripts de igual manera a ambas camaras. Creando un objeto vacio y añadiendo ambas camaras a este objeto.

![alt text][dosCamaras]

3º Ahora la camara uno deberá mostrar lo mismo que la camara dos pero solo en la mitad izquierda de la pantalla, para eso configuraremos los parametros deberán ser los siguientes: x=0 (para empezar el ancho desde el lado izquiero) w=0,5 (ya que solo usaremos la mitad de la pantalla) y como proyección en perspectiva y el campo de visión a gusto del programador. La configuración de la camara 1 será la siguiente.

![alt text][confCamara1]

4º La configuración de la camara dos es similar pero la x=0,5 ya que la proyección se verá en el lado derecho de la pantalla y el ancho es también la mitad por tanto w=0,5. La camara 2 tendrá siguiente configuración.

![alt text][confCamara2]
