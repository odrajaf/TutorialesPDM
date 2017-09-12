
# Tutorial, como mostrar un gif en android


1º En primer lugar deberemos escoger un gif y descomponerlo en los diferentes frames que lo componen (si no tenemos ya las diferentes imagenes que componen un gif), podemos usar páginas como http://gifmaker.me/exploder/. Una vez tengamos todas las imagenes, las colocaremos en la ruta /app/src/main/res/drawable. Es recomendable renombrar todas la imagenes con nombres sencillos en minuscula como podrían ser imagen1.gif, imagen2.gif,... 

2º En la carpeta /app/src/main/res/drawable creamos un xml al que llamaremos por ejemplo animacion.xml en el que le especificaremos todos los frames que contendrá que iamgenes tendrá la animación y que tiempo estará en pantalla cada imágen. El archivo animacion.xml quedaría de la siguiente manera:

	<?xml version="1.0" encoding="utf-8"?>
	<animation-list xmlns:android="http://schemas.android.com/apk/res/android"
	    android:oneshot="false">
	    <item android:drawable="@drawable/imagen1" android:duration="65" />
	    <item android:drawable="@drawable/imagen2" android:duration="65" />
	    <item android:drawable="@drawable/imagen3" android:duration="65" />
	    <item android:drawable="@drawable/imagen4" android:duration="65" />
	</animation-list>




	
