# Método numérico para encontrar la distribucción de probabilidad y energías de un electrón "atravesando" un pozo de cuadrado finito.

<center> <h2>Autor: Harold Yesid Laserna Diaz</h2> </center>

<p style='text-align: justify'>Un electrón es lanzado desde $x=-\infty$ e interactúa con un potencial $V(x)$ al pasar sobre él, como se muestra a continuación:</p>



$$    V(x)= 
\begin{cases}
    -V_{0},& \text{sí } |x| < a\\
    0,   &  \text{sí }   |x| > a.
\end{cases}
$$


![Pozo de potencial](pozo.png "Pozo de potencial")

<p style='text-align: justify;'>Dado que el potencial es independiente del tiempo tenemos que la ecuación de Schrödinder es:</p>

$$\frac{-\hbar^2}{2m}\frac{d^2\psi}{dx^2}+(V(x)-E)\psi=0,$$

<p style='text-align: justify;'>siendo $m$ la masa del electrón, $\hbar$ el cociente de la constante de Planck y 2 veces $\pi$ y, $E$ la energía que puede tomar el electrón.</p>

<p style='text-align: justify;'>Dependiendo de la región tomada, obtendremos diferentes soluciones para $\psi$, como se muestra a continuación:</p>

$$    \psi(x)= 
\begin{cases}
    Fe^{-\kappa x},& \text{sí } x > a\\
    Dcos(lx),   &  \text{sí }  0 < x < a \\
    \psi(-x), & \text{sí } x < 0,\\
\end{cases}
$$

<p style='text-align: justify;'>con $l$ y $\kappa$ como:</p>

$$l= \frac{\sqrt{2m(E+V_{0})}}{\hbar},$$
$$\kappa = \frac{\sqrt{-2mE}}{\hbar}.$$

<p style='text-align: justify;'>Tenemos que para una transmisión perfecta $T = 1$, obtenemos que la energía $E_{n}$ es:</p>

$$E_{n}= \frac{n^2\pi^2\hbar^2}{2m(2a)^2}-V_{0},$$

<p style='text-align: justify;'>lo anterior ocurre cuando estamos en un pozo de potencial cuadrado infinito o aproximadamente en pozos con potencial $V_{0}$ grandes. Se puede tomar la anterior ecuación como una aproximación.</p>
    
<p style='text-align: justify;'>Mediante la solución analítica anterior, nos puede dar una idea de la posible solución mediante métodos númericos que es nuestro objetivo como se mostrará a continuación.</p>




# Solución del pozo de potencial negativo por métodos numéricos

<p style='text-align: justify;'>Tenemos en cuenta que la solución de $\psi$ independientemente del potencial $V(x)$ tiene que ser normalizable. Esto quiere decir que  <strong>TODAS</strong> las funciones $\psi$ cumplen con la siguiente condición:</p>

$$\lim_{x \to -\infty}\psi(x)=0 \\ y \\ \lim_{x \to \infty}\psi(x)=0.$$

<p style='text-align: justify;'>Es decir que si tomamos una posición $x$ lo suficientemente lejana del evento de interés, por ejemplo un valor que denotaremos con $\sigma$, podemos usar las anteriores condiciones, es decir:</p> 
    
$$\lim_{x \to -\sigma}\psi(x)=0 \\ y \\ \lim_{x \to \sigma}\psi(x)=0.$$

<p style='text-align: justify;'>Lo anterior es importante dado que a la hora de simular nuestro sistema mediante metodos numéricos, tenemos que escoger una posición $\sigma$ lo suficientemente lejana al evento, ya que es en el único lugar donde conocemos la función $\psi$ que se espera que sea $0$, y con base a lo anterior poder conocer los demás valores de $\psi$ en las demás posiciones, es decir, todos los puntos $x \in [-\sigma,\sigma]$.</p>

<p style='text-align: justify;'>También es importante adimensionar la ecuación de Schrödinger, ya que, en algunos métodos se la desventaja de tener solo unos límites de convergencia, es decir que si escogemos una posición demasiado grande, nuestro método númerico no va converger a una solución deseable, con lo cual, nuestro error de truncamiento será demasiado grande. 
Para adimensionar la ecuación de Schrödinger usamos el siguiente convenio:</p>

$$y=\frac{x}{L},$$

<p style='text-align: justify;'>siendo $L$ una constante a escoger, con las mismas unidades que $x$.</p>

<p style='text-align: justify;'>Teniendo en cuenta la regla de la cadena para la primera derivada obtenemos que:</p>

$$\frac{d\psi}{dx}=\frac{d\psi}{dy}\frac{dy}{dx}$$

$$\frac{d\psi}{dx}=\frac{d\psi}{dy}\frac{1}{L},$$

<p style='text-align: justify;'>aplicando una segunda derivada obtenemos que:</p>

$$\frac{d^2\psi}{dx^2}=\frac{d}{dx}\left(\frac{d\psi}{dy}\right)\frac{1}{L}.
$$

<p style='text-align: justify;'>Por teorema de Schwarz lo anterior se convierte en:</p>

$$\frac{d^2\psi}{dx^2}=\frac{d}{dy}\left(\frac{d\psi}{dx}\right)\frac{1}{L},$$

<p style='text-align: justify;'>teniendo en cuenta la primera derivada anteriormente definida, tal que:</p>

$$\frac{d^2\psi}{dx^2}=\frac{d}{dy}\left(\frac{d\psi}{dy}\frac{1}{L}\right)\frac{1}{L},$$

<p style='text-align: justify;'>con lo cual obtenemos que:</p>

$$\frac{d^2\psi}{dx^2}=\frac{d^2\psi}{dy^2}\frac{1}{L^2},$$

<p style='text-align: justify;'>remplazando lo anterior en la ecuación de Schrödinger independiente del tiempo:</p>

$$\frac{-\hbar^2}{2m}\frac{d^2\psi}{dy^2}\frac{1}{L^2}+(V(x)-E)\psi=0,$$

<p style='text-align: justify;'>y organizando términos tenemos que:</p>

$$\frac{d^2\psi}{dy^2}+\frac{2mL^2}{\hbar^2}(E-V(y))\psi=0.$$

<p style='text-align: justify;'>Esta anterior ecuación diferencial de segundo orden es posible solucionar con métodos numéricos de un paso, por ejemplo con Runge Kutta, Euler, etc. El unico problema es "tantear" la ecuación con varios valores de $E$ hasta encontrar una solución con sentido. Esto es debido a que $E$ no es un valor  continuo en un problema cuántico. A pesar de la discretización de $E$, si es posible solucionar con metodos de un paso mencionados anteriormente o por métodos numéricos multipaso.</p>

<p style='text-align: justify;'>El objetivo para poder aplicar un método numérico más eficiente, es convertir la anterior ecuación diferencial en una ecuación lineal sin derivadas. Con lo cual necesitamos transformar la segunda derivada de la función con respecto a $y$ en algo que no sea derivada.</p>

<p style='text-align: justify;'>Para esto, primero usamos la expansión de Taylor centrada en $y$ para $f(y+h)$ y $f(y-h)$ siendo $h$ un incremento arbitrario, que definiremos con más detalle más adelante. Escribiendo la expansión de Taylor únicamente a tercer orden, obtenemos que:</p>

$$f(y+h)\approx f(y)+ \frac{df(y)}{dy}h + \frac{d^2f(y)}{dy^2}\frac{h^2}{2} +\frac{d^3f(y)}{dy^3}\frac{h^3}{6}$$

$$f(y-h)\approx f(y)- \frac{df(y)}{dy}h + \frac{d^2f(y)}{dy^2}\frac{h^2}{2} - \frac{d^3f(y)}{dy^3}\frac{h^3}{6},$$

<p style='text-align: justify;'>sumando $f(y+h)$ y $f(y-h)$ tenemos que:</p>

$$f(y+h)+f(y+h) \approx 2f(y)+\frac{d^2f(y)}{dy^2}h^2,$$

<p style='text-align: justify;'>despejando la segunda derivada tenemos que:</p>

$$\frac{d^2f(y)}{dy^2} \approx \frac{f(y+h)+f(y-h)-2f(y)}{h^2}.$$

<p style='text-align: justify;'>Como observamos de la anterior ecuación, mediante la aproximación por expansión de Taylor, es posible convertir la segunda derivada en términos de sumas y restas de la función $f$, teniendo en cuenta un incremento $h$ escogido. Con lo anterior, aún no es posible pasar a simular nuestro sistema, debido a que en la ecuación anterior, $y$ sigue siendo continua. Para esto necesitamos discretizar $y$ de la siguente forma:</p>

![discretizar](discretizar.jpg "Discretización")

<p style='text-align: justify;'>Como se muestra en la imagen anterior, para poder discretizar, mediante la función $f$ continua, seleccionamos únicamente puntos $x_{i}$ que estén separados a una distancia $h$ entre sí. para este caso discretizamos desde un punto $x_{o}$ hasta un punto $x_{n}$, siendo $n+1$ la cantidad total de puntos $x_{i}$, en este caso, $x_{o}$ y $x_{n}$ son las fronteras de puntos a usar. Dado que podemos definir las fronteras y podemos definir la cantidad de puntos totales a usar podemos determinar la distancia $h$ de separación entre los puntos $x_{i}$ de la siguiente forma:</p>

$$h=\frac{x_{n}-x_{0}}{n},$$

<p style='text-align: justify;'>lo anterior exige que $x_{n}>x_{0}$.
Definido el incremento $h$ es posible definir $x_{1}$, $x_{2}$, $x_{3}$ de la siguiente forma:</p>

$$x_{1}=x_{0}+h$$
$$x_{2}=x_{1}+h$$
$$x_{3}=x_{2}+h,$$

<p style='text-align: justify;'>de lo anterior notamos que para definir cualquier $x_{i+1}$ es necesario tener el valor de $x_{i}$. Es decir, que en general:</p>

$$x_{i+1}=x_{i}+h.$$

<p style='text-align: justify;'>para seguir nuestro desarrollo de la segunda derivada cambiamos la variable $x$ por la $y$ en nuestra discretización tal que obtenemos dos ecuaciónes importantes:</p>

$$h=\frac{y_{n}-y_{0}}{n}$$

$$y_{i+1}=y_{i}+h.$$

<p style='text-align: justify;'>Desde esta anterior perspectiva de la discretización, ahora el valor obtenido de la segunda derivada anterior, puede ser escrita como:</p>

$$\frac{d^2f(y_{i})}{dy_{i}^2} \approx \frac{f(y_{i}+h)+f(y_{i}-h)-2f(y_{i})}{h^2},$$

<p style='text-align: justify;'>teniendo en cuenta el incremento $h$, podemos reorganizar lo anterior como:</p>

$$\frac{d^2f(y_{i})}{dy_{i}^2} \approx \frac{f(y_{i+1})+f(y_{i-1})-2f(y_{i})}{h^2},$$

<p style='text-align: justify;'>aclarando que: $y_{i-1}=y_i-h$. Teniendo en cuenta la "transformación" de la segunda derivada y la discretización de $y$ ahora definamos la segunda derivada con respecto a la posición en este caso para la función $\psi$ y asumiendo la aproximación como una igualdad, tal que:</p>

$$\frac{d^2\psi(y_{i})}{dy_{i}^2} = \frac{\psi(y_{i+1})+\psi(y_{i-1})-2\psi(y_{i})}{h^2}.$$

<p style='text-align: justify;'>Escribiendo la ecuación de Schrödinger con la variable $y$ discretizada, en este caso usamos $y_{i}$ tal que:</p>

$$\frac{d^2\psi(y_{i})}{dy_{i}^2}+\frac{2mL^2}{\hbar^2}(E-V(y_{i}))\psi(y_{i})=0,$$

<p style='text-align: justify;'>ahora, reemplazando la derivada con la aproximación anterior se tiene que:</p>

$$\frac{\psi(y_{i+1})+\psi(y_{i-1})-2\psi(y_{i})}{h^2}+\frac{2mL^2}{\hbar^2}(E-V(y_{i}))\psi(y_{i})=0.$$

<p style='text-align: justify;'>Reorganizando terminos, tenemos la siguiente ecuación (el objetivo de la reorganización es compararlo más adelante para construir una matriz):</p>

$$-\frac{1}{2}\frac{\psi(y_{i-1})}{h^2} + \left( \frac{1}{h^2} + \frac{mL^2}{\hbar^2}V(y_{i})\right)\psi(y_{i}) -\frac{1}{2}\frac{\psi(y_{i+1})}{h^2}=\frac{mL^2E}{\hbar^2}\psi(y_{i}).$$

<p style='text-align: justify;'>Para tener una solución del sistema, necesitamos conocer los valores de frontera de $\psi$, es decir $\psi(y_{0})$ y $\psi(y_{n})$. En este caso $y_{0}$ y $y_{n}$ son puntos lejanos al evento de interés, tal que:</p>

$$\psi(y_{n}) = \psi(y_{0}) = 0.$$

<p style='text-align: justify;'>Construyendo las ecuaciones para $y_{1}$, $y_{2}$ y $y_{n-1}$ tenemos lo siguiente: </p>

$x_{1}:$

$$-\frac{1}{2}\frac{\psi(y_{0})}{h^2} + \left( \frac{1}{h^2} + \frac{mL^2}{\hbar^2}V(y_{1})\right)\psi(y_{1}) -\frac{1}{2}\frac{\psi(y_{2})}{h^2}=\frac{mL^2E}{\hbar^2}\psi(y_{1}).$$

$x_{2}:$

$$-\frac{1}{2}\frac{\psi(y_{1})}{h^2} + \left( \frac{1}{h^2} + \frac{mL^2}{\hbar^2}V(y_{2})\right)\psi(y_{2}) -\frac{1}{2}\frac{\psi(y_{3})}{h^2}=\frac{mL^2E}{\hbar^2}\psi(y_{2}).$$

$x_{n-1}:$

$$-\frac{1}{2}\frac{\psi(y_{n})}{h^2} + \left( \frac{1}{h^2} + \frac{mL^2}{\hbar^2}V(y_{n-1})\right)\psi(y_{n-1}) -\frac{1}{2}\frac{\psi(y_{n-2})}{h^2}=\frac{mL^2E}{\hbar^2}\psi(y_{n-1}).$$

<p style='text-align: justify;'>Teniendo en cuenta que $\psi(y_{n})$ y $\psi(y_{0})$ son 0 y con esto, con los demás $y_{i}$ es posible construir la siguiente ecuación lineal matricial:</p>

![matriz](matrix.png "MarineGEO logo")

<p style='text-align: justify;'>De esto, podemos observar que lo anterior es un poblema de autovalores y autovectore, siendo el autovector el vector con las componentes $\psi(y_i)$ y los autovalores $\frac{mL^2E}{\hbar^2}.$</p>

<p style='text-align: justify;'>Esta matriz es una <strong>matriz tridiagonal</strong> que puede ser definida de forma simple de la siguiente forma:</p>

$$A_{i,i} = \frac{1}{h^2} + \frac{mL^2}{\hbar^2}V(y_{i})$$

$$A_{i,i+1} = A_{i,i-1} = -\frac{1}{h^2}$$

$$A_{i,j} = 0, \ para \ j \neq i+1 \ y \ \ j \neq i-1.$$
