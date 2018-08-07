# Taller # 1
###### Realizado por: Miguel Beltrán y Juan Sebastian Triana Perez
1.
a)  Evaluar el polinomio en cada valor indicado y el número de operaciones mínimo para hacerlo, para los siguientes polinomios junto con sus derivadas
Codigo:

```r
hornet<-function(p,n,x ,iter){ #Funcion hornet p: vector de grados, n: Grado del polinomio, x: Valor inicial, iter: iteraciones
  y = p[c(1)];
  i = 0;
  for(i in 1:n+1){
    y = x*y + p[c(i)];
    
  }
  print(iter+i*2);
  return(y);
}

eval<-function(p, n, x ,iter){
  s = 0;
  i = 0;
  for(i in 0:n){
    s = s +(p[c(i+1)]*(x^(n-i)));
    print(i+1);
  }
  print(iter+i*3);
  return(s);
}

derivar<-function(p, n){  #Funcion que deriva p: Coeficientes, n: Grado del polinomio.
  d=numeric(0);
  iter = 0;
  for(i in 0: n){
    
    d[c(i+1)] = (n-i)*p[c(i+1)];
    iter = iter+1;
  }
  x = hornet(d, n-1, -2, iter); #Llamada a la funcion hornet.
  return(x)
}

p<-c(2,0,-3,3,4)

resultado = derivar(p,4);
resultado
```
Respuesta:

```r
        Con el polinomio: 13
        Con la derivada del polinomio: -49
```

2.
Se necesita un recipiente rectangular, sin tapa, de un litro de capacidad. Para construirlo se debe usar una lamina rectangular de 32 cm de largo y 24 cm de ancho. Eñ procedimiento será recortar un cuadro idéntico en cada una de las cuatro esquinas y doblar los bordes de la lámina para formar el recipiente.
Determine la medida del lado del cuadrado que se debe recortar en cada esquina para que el reccipiente tenga la capacidad requerida.

Utilice dos métodos diferentes para resolver el problema, instruméntelo en el lenguaje adecuado.

1 ¿Cual etapa del proceso ded resolución de un problema numérico requiere mas atención?
2 ¿Qué conocimientos son necesarios para formular un modelo matemático?
3 En el ejemplo de la caja ¿ Cual sería de la desventaja de intentar obtener experimentalmente la solución mediante prueba y error en lugar de analizar el modelo matematico?
4 ¿Que es más critico: el error de truncamiento o el error de redondeo ?
5 ¿Cuál es la ventaja de instrumentar computacionalmente un método numérico?
6 ¿Por que es importante validar los resultados obtenidos?

Codigo: 

```r
    #Metodo #1
    
    volbiseccion<-function(largo,ancho){
      a = 0;
      b = largo;
      x = ((a+b)/2);
      i = 0;
      error = abs(volumen(largo,ancho,x)-1000);
      while(error>1.E-8){
        print(x);
        i = i +1;
        if(volumen(largo,ancho,x)<1000)
        {
          b=x;
        }
        else
        {
          a=x;
        }
        x <- ((a+b)/2);
        error = abs(volumen(largo,ancho,x)-1000);
      }
      return (x);
    }
    volumen<-function(largo, ancho, x){
      return((largo-2*x)*(ancho-2*x)*x);
    }
    cubica<-function(largo, ancho){
      return()
    }
    y = volbiseccion(32,24);
    y
    
    #Metodo #2
    Fx <- function(x, largo, ancho) {return ((largo-2*x)*(ancho-2*x)*x)}
    F1x <- function(x, largo, ancho) {return (12*x^2-4*ancho*x-4*largo*x+largo*ancho)}
    
    newton <- function(x, largo, ancho) {
      for(i in 1:60) {
        x<-x-Fx(x, largo, ancho)/F1x(x, largo, ancho)
        if (Fx(x, largo, ancho) == 1000) break
        error<-abs(Fx(x, largo, ancho)/F1x(x, largo, ancho))
        cat("X=",x,"\t","E=",error,"\n")
      }
    }
    newton(10, 32, 24)
```
Respuesta metodo # 1

```r
    16
    8
    12
    10
    9
    8.5
    8.25
    8.125
    8.0625
    8.09375
    8.078125
    8.085938
    8.089844
    8.091797
    8.092773
    8.093262
    8.093018
    8.09314
    8.093201
    8.093231
    8.093216
    8.093224
    8.09322
    8.093218
    8.093219
    8.093219
    8.09322
    8.09322
    8.09322
    8.09322
    8.09322
    8.09322
    8.09322
    8.09322
    8.09322
    y = 8.09322
```

Respuestas a preguntas:

Respuesta metodo #2

```r
    X= 11.76471 	 E= 0.2272153
    X= 11.99192 	 E= 0.008067941
    X= 11.99999 	 E= 1.082665e-05
    X= 12 	 E= 1.953637e-11
    X= 12 	 E= 0
    X= 12 	 E= 0
```

Respuestas a preguntas:

3.
Implemente en R el siguiente algoritmo que sirve para calcular la raíz cuadrada. Aplíquelo para evaluar la raíz cuadrada de 7, analice su precisión, convergencia y validez.

Codigo:
```r
    tercerpunto<-function(n,e,x){
      
      y<- 1/2 * (x+n/x);
      print("Convergencia:");
      
      erroanter=abs(x-y);
      errornuevo=0;
      contador=0;
      plot(erroanter,type="s", main="plot(x,type=\"s\")");
      while (abs(x-y) > e) {
        
        errornuevo = abs(x-y);
        
        print(errornuevo/erroanter);
        x<-y;
        y<- 1/2 *(x+(n/x));
        erroanter = errornuevo;
        contador= contador+1;
        text(contador,erroanter,".",cex=1.0, col="red" );
      }
      return(y);
    } 
    
    raiz=tercerpunto(7,1.E-8,12);
    
    
    validez = raiz*raiz;
    
    print("Resultado:");
    format(round(raiz, 8), nsmall=8);
    print("Validez:");
    validez
```

Respuesta

```r
    "Convergencia:"
         1
        0.4536424
        0.3497373
        0.1619293
        0.02767229
        0.0007669302
        
        validez = raiz*raiz;
        Resultado:
        2.64575131
        Validez:
        7
```

6.
Eficiencia de un algoritmo esta denotada por T(n)
a) Recorra el algoritmo con n=73
b)  Suponga que T(n) representa la cantidad de operaciones aritméticas de división que se realizan para resolver el problema de tamaño n. Encuentre T(n) y exprésela con la notación O( ) Para obtener T(n) observe el hecho de que cada ciclo el valor de n se recude aproximadamente a la mitad.

Codigo:

```r
    sextopunto<-function(n){
      while (n>0){
        d<- n%%2;
        n<- trunc(n/2);
        print(d);
        #print(n);
      }
    }
    sextopunto(5);
    plot(funcionT, from=0, to=100);
    
    funcionT<-function(n){
      
      return(log2(n)+1);
    }
```

Explicación:

```r
     T(n)= T(n/2)+1
         =(T(n/4)+1)+1
         = T(n/4)+2
         =(T(n/8)+1)+2
         = T(n/8)+3
         ...
         = T(n/(2^i))+i
         ...
         =T(n/(2^(log(n))))+log 2(n)
         =T(1)+log2(n)
    Por tanto, T(n) es O(log n)
```

Grafica:

7.
Utilice el método de Newton para resolver el problema, muestre gráficamente cómo se comporta la convergencia a la solución.
Una particula se mueve en el espacio con el vector de posición R(t) = (2cos(t)), sen(t), 0). Se requiere conocer el tiempo en el que el objeto se encuentra más cerca del punto P(2,1,0). Utilice el método de Newton con cuatro decimales de precisión.

Codigo:

```r
    distancia=expression (sqrt ((2*cos(x)-2)^2+(sin*(x)-1)^2))
    f=D(distancia,"x")
    df<-expression(3*sin(x)*cos(x)-4*sin(x)+cos(x))
    df1=D(df,"x")
    Fx<-function(x) eval.parent(df,x)
    F1x<-function(x) eval.parent(df1,x)
    newton <- function(x) {
       for(i in 1:5) {
         x<-x-Fx(x)/F1x(x)
         if (Fx(x) == 0) break
         error<-abs(Fx(x)/F1x(x))
         cat("X=",round(x,4),"\t","E=",error,"\n")
       }
     }
    newton(0)
```

13.
Encuentre una fórmula iterativa de convergencia cuadrática y defina un intervalo de convergenica apropiado para calcular para calcular la raiz real n-ésima de un número real. El algoritmo solamente debe incluir operaciones aritmética elementales.

Codigo:

```r
    Fx <- function(x, b) {return (x*x-b)}
    F1x<- function(x, b){return(2*x)}
      
    
    newton <- function(x , b) {
        
      for(i in 1:10) {
        x<-x-Fx(x, b)/F1x(x, b)
        if (Fx(x, b) == sqrt(b)) break
        error<-abs(Fx(x, b)/F1x(x, b))
        cat("X=",x,"\t","E=",error,"\n")
      }
    }
    newton(2, 3)
```

Repuesta:

```r
    X= 1.75 	 E= 0.01785714 
    X= 1.732143 	 E= 9.204713e-05 
    X= 1.732051 	 E= 2.44585e-09 
    ...
```

15.
Se propone resolver la ecuación ... con el método del punto fijo.
a) Obtenga la ecuacón f(x)=0 resolviendo la integral
b) Mediante un gráfico aproximado, o evaluando directamenta, localice la raíces reales.
c) Proponga una ecuacion equivalente x= g(x) y determine el intervalo de convergencia para calcular una de las dos raices.
d) Del intervalo anterior, elija un valor inicial y realice 5 iteraciones. En cada ineración verifique que se cumple la condición de convergencia del punto fijo y estime el error de truncamiento con el último resultado.

Codigo: