
# Tutorial, canvas en android y paso de imagenes


1º Primero en código java tendremos crear un clase que herede de la clase View y sobreescribir el método onDraw, esta clase será donde pondremos nuestro código con las imagenes o forma que queremos que se dibujen en el lienzo. De forma que podría quedar así:

	public class CanvasView extends View {
        	public CanvasView(Context context) {
          	  super(context);
        	}

       	 @Override
      	  protected void onDraw(Canvas canvas) {
         	   super.onDraw(canvas);
          	  Paint paint = new Paint();
       	 }
	}


2º Luego crearemos un Activity vacía (empty), en esta tendremos que crear un atributo del tipo CanvasView (como hemos llamado a la clase anterior), la inicializamos en el  onCreate y asignamos el canvasView al setContentView. De este modo tendremos un canvas en toda la superficie del activity, a continuación un ejemplo de como podría quedar el código.

	CanvasView liezo;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
        
		liezo = new CanvasView(this);
		setContentView(liezo);
    	}

3º Si ejecutamos el siguiente código, no notaremos diferencia ya que el fondo del canvas es blanco, así que dibujaremos un cuadrado negro de 70x70, los dos primeros ceros son la posición de la esquina superior, y los dos 70 son la posición de la esquina opuesta, el código irá dentro dentro del método onDraw.

	paint.setColor(Color.BLACK);
	canvas.drawRect(0 , 0, 70 , 70 , paint);


4º Ahora si podremos apreciar que hemos dibujado un cuadrado negro en el canvas, ahora colocaremos una pequeña imagen en el lienzo, para ello introduciremos una imagen llamada cocacola.jpg en el directorio /app/src/main/res/mipmap-hdpi de nuestro proyecto. Una vez hecho esto en la clase principal donde está el método onCreate cargamos en un Bitmap tal imagen, como muestra el código. Es importante que la imagen tenga el nombre todo en minusculas y sin caracteres raros ya que sino no podríamos referirnos a ella con R.mipmap.cocacola

	public class MainActivity extends AppCompatActivity {

	CanvasView liezo;
	Bitmap cocacola;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);

		liezo = new CanvasView(this);
		setContentView(liezo);

		cocacola = BitmapFactory.decodeResource(getResources(),  R.mipmap.cocacola);
	}


5º Ahora deberemos en el método onDraw decirle al canvas que dibuje la imagen que hemos seleccionado, donde colocaremos la línea `canvas.drawBitmap(cocacola, 70, 70, null);` donde 70, 70 será donde colocará la esquina superior de la imagen. Mod

	public class CanvasView extends View {
        	public CanvasView(Context context) {
            	super(context);
        	}

		@Override
		protected void onDraw(Canvas canvas) {
			super.onDraw(canvas);
			Paint paint = new Paint();

			paint.setColor(Color.BLACK);
			canvas.drawRect(0 , 0, 70 , 70 , paint);

			canvas.drawBitmap(cocacola, 70, 70, null);
		}
	}

6º Es muy importante si queremos realizar alguna animación como podría ser mover cualquier elemento dibujado, debemos usar el método liezo.invalidate(); para indicarle a la aplicación que se redibuje el canvas con los cambios en los parametros. En el siguiente ejemplo mostramos un ejemplo sencillo de como mover el cuadrado negro por la pantalla usando un sencillo contador y la función invalidate.


	package com.ugr.fajardo.tutorial1;

	import android.content.Context;
	import android.graphics.Bitmap;
	import android.graphics.BitmapFactory;
	import android.graphics.Color;
	import android.graphics.Paint;
	import android.support.v7.app.AppCompatActivity;
	import android.os.Bundle;
	import android.graphics.Canvas;
	import android.view.View;

	public class MainActivity extends AppCompatActivity {

	    CanvasView liezo;
	    Bitmap cocacola;
	    float contador = 0.0f;

	    @Override
	    protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);

		liezo = new CanvasView(this);
		setContentView(liezo);

		cocacola = BitmapFactory.decodeResource(getResources(),  R.mipmap.cocacola);
	    }


	    public class CanvasView extends View {
		public CanvasView(Context context) {
		    super(context);
		}

		@Override
		protected void onDraw(Canvas canvas) {
		    super.onDraw(canvas);
		    Paint paint = new Paint();

		    paint.setColor(Color.BLACK);
		    canvas.drawRect(contador+0 , contador+0, contador+70 , contador+70 , paint);
		    contador=+ contador + 0.5f;

		    canvas.drawBitmap(cocacola, 70, 70, null);
		    liezo.invalidate();
		}
	    }
	}


	
