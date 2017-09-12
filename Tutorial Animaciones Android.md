
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

3º A continuación pondremos un ImagenView en el xml de diseño del activity, si el activity que utilizas se llama MainActivity el archivo se llamará activity_main.xml, se encuentra en la ruta del proyecto /app/src/main/res/layout. En este deberás Insertar el siguiente código, como podemos ver el id del ImageView es **imageViewAnimacion** y le hemos asignado el xml que hemos creado antes en la línea **@drawable/animacion**

	<ImageView
        android:id="@+id/imageViewAnimacion"
        android:layout_width="484dp"
        android:layout_height="wrap_content"
        app:srcCompat="@drawable/animacion"
	/> 

4º Una vez hecho esto nos vamos al código java del Activity y aquí opcionalmente crearemos una variable ImagenView para posteriormente obtener el recurso animado e instanciar una objeto de la clase AnimationDrawable que se encargar de controlar la animación. El código que realiza esto es el siguiente


	public class MainActivity extends AppCompatActivity {

	    ImageView animacion;

	    @Override
	    protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);

		animacion = (ImageView) findViewById(R.id.imageViewAnimacion);
		AnimationDrawable animacionDrawable = (AnimationDrawable) animacion.getDrawable();
		animacionDrawable.start();
	    }
	}

4ºb de manera opcional también podríamos escribir el código sin usar un objeto ImageView pero es algo más díficil de leer 

	AnimationDrawable animacionDrawable = (AnimationDrawable) ((ImageView) findViewById(R.id.imageViewAnimacion)).getDrawable();
        animacionDrawable.start();

5º Una vez ejecutemos y revisemos los errores debería ejecutarse la animación, ya solo quedaría darle la velocidad deseada modificando el parametro **android:duration="65"** del archivo animacion.xml


	
