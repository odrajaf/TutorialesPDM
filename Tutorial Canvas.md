
#Tutorial, canvas en android y paso de imagenes

[cpClavePublica]:https://github.com/odrajaf/swap1415/blob/master/Practica2/copiando%20clave%20publica.png
[sshClavePub]:https://github.com/odrajaf/swap1415/blob/master/Practica2/ssh%20mediante%20clave%20publica.png
[crontab]:https://github.com/odrajaf/swap1415/blob/master/Practica2/crontab.png
[resultado]:https://github.com/odrajaf/swap1415/blob/master/Practica2/contrab%20con%20rsync.png

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


4º Ahora si podremos apreciar que hemos dibujado un cuadrado negro en el canvas, ahora colocaremos una pequeña imagen en el lienzo, para ello introduciremos una imagen llamada cocacola.jpg en el directorio /app/src/main/res/mipmap-hdpi de nuestro proyecto. Una vez hecho esto en la clase principal donde está el método onCreate cargamos en un Bitmap tal imagen, como muestra el código.


3º Creamos otra máquina virtual e instalamos Ubuntu server 12.04.5 con exactamente las mismas opciones de antes, a la que llamaremos ubuntu02

4º Modificamos también el archivo /etc/network/interfaces pero cambiando la dirección ip de ubuntu02

    auto eth1
    iface eth1 inet static
    address 192.168.1.101
    gateway 192.168.1.1
    netmask 255.255.255.0
    network 192.168.1.0
    broadcast 192.168.1.255


5º Antes de usar rsync es conveniente para evitar problemas de permisos hacer en ambas maquinas<br/>`sudo chown fajardo:fajardo -R /var/www`

para instalar rsync usamos `sudo apt-get install rsync`
		

6º Preferimos por usar un usuario normal en lugar de root para el ssh, 
   generamos la clave publica en ubuntu02<br/>`ssh-keygen -t dsa`

copiamos la clave publica de ubuntu02 en ubuntu01<br/>
`ssh-copy-id -i ~/.ssh/id_dsa.pub fajardo@192.168.1.100`
	
![alt text][cpClavePublica]

probamos a conectarnos por ssh sin que nos pida clave<br/>
	`ssh 192.168.1.100 -l fajardo`
	
![alt text][sshClavePub]

7º Modificamos el archivo crontab de ubuntu02 con `sudo vim /etc/crontab`
añadimos la línea<br/>`* * * * *	fajardo	rsync -avz -e ssh fajardo@192.168.1.100:/var/www/* /var/www`

esto actualizará el contenido de las carpetas cada minuto.

![alt text][crontab]

En caso de modificar algún archivo de /var/www/ en ubuntu01 se modificará en ubuntu02 cada minuto

![alt text][resultado]
	
