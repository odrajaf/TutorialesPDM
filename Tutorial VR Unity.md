
# Tutorial, VR unity para dispositivos sin giroscopio

[dosCamaras]:https://github.com/odrajaf/TutorialesPDM/blob/master/images/imagen1.png
[confCamara1]:https://github.com/odrajaf/TutorialesPDM/blob/master/images/imagen2.png
[confCamara2]:https://github.com/odrajaf/TutorialesPDM/blob/master/images/imagen3.png
[vista]:https://github.com/odrajaf/TutorialesPDM/blob/master/images/imagen4.png

1º Lo más caracteristico del VR, es el uso de una vision estereoscópica para esto lo que haremos en primer lugar será duplicar nuestra camara principal del proyecto.

2º Una vez hecho esto tenemos dos camaras situadas en el mismo lugar y a la que podremos hacer de forma sencilla que le afecten todos los scripts de igual manera a ambas camaras. Creando un objeto vacio y añadiendo ambas camaras a este objeto.

![alt text][dosCamaras]

3º Ahora la camara uno deberá mostrar lo mismo que la camara dos pero solo en la mitad izquierda de la pantalla, para eso configuraremos los parametros deberán ser los siguientes: x=0 (para empezar el ancho desde el lado izquiero) w=0,5 (ya que solo usaremos la mitad de la pantalla) y como proyección en perspectiva y el campo de visión a gusto del programador. La configuración de la camara 1 será la siguiente.

![alt text][confCamara1]

4º La configuración de la camara dos es similar pero la x=0,5 ya que la proyección se verá en el lado derecho de la pantalla y el ancho es también la mitad por tanto w=0,5. La camara 2 tendrá siguiente configuración.

![alt text][confCamara2]

Ya podremos apreciar que tenemos un efecto estereoscópico en nuestro juego independientemente si lo ejecutamos en pc o android.

![alt text][vista]


5º Ahora debemos aprovechar el un sensor como el acelerometro para imitar con las camaras el movimiento de la cabeza, para ello usaremos el eje z del acelerometro que percibirá cuando agachamos o levantamos la cabeza. Para ello crearemos un script al que llamaremos camaraAcelerometro.cs

	using System.Collections;
	using System.Collections.Generic;
	using UnityEngine;

	public class camaraAcelerometro : MonoBehaviour {

			float hRotation = 0.0f;   
			float vRotation = 0.0f;  
			float valorAnterior = 0;
	

			void Start () {

			}

			void Update() {
				float valorZ = -(Input.acceleration.z)* 45;			
				transform.rotation = Quaternion.Euler((valorZ+ valorAnterior)/2, vRotation, 0.0f);
				valorAnterior = valorZ;
			}
		}
El acelerometro va aproximadamente de valores de -0,7 a 0,6 (multiplicado por 45 para que diera el angulo adecuado) cuando agachamos y levantamos la cabeza respectivamente, este script usa la variable valorAnterior para suavizar el movimiento (evitando cambios bruscos) y el valoz del eje z del acelerometro rotará más o menos la camara. El giro a izquiera o derecha es dificil de captar por la precisión del acelerometro y se mantiene a 0 el giro en horizontal.
