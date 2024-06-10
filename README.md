![Banner](Banner.png)

# Proyecto 1 - Algoritmo de sistema de costos

Para este primer proyecto se aplicaron los conceptos de algoritmos, programación estructurada, control de flujo, arreglos y el uso de Git y GitHub.

## Planteamiento

Construir un algoritmo en pseudocódigo que simule un sistema para calcular el costo de un producto con base en su precio original y el porcentaje de descuento aplicado. El algoritmo debia cumplir con los siguientes requisitos:

- Leer el precio original del producto.
- Aplicar un descuento al producto si es aplicable (por ejemplo, si el cliente tiene un cupón de descuento).
- Aplicar impuestos al producto (por ejemplo, el IVA u otros impuestos).
- Si el cliente compra más de un artículo, aplicar un descuento por cantidad.
- Calcular el costo de envío basado en el destino y el peso del paquete.
- Calcular el costo final del producto sumando el precio con descuento, impuestos, descuento por cantidad y costo de envío.
- Mostrar el costo final del producto, desglosando los diferentes componentes (descuentos, impuestos, descuento por cantidad y costo de envío).

## Solución explicada paso a paso

1. Primero, se declararon las variables utilizadas en el proyecto:
- `n` y `p` son enteros que se usaron pare representar el número de articulos comprados y los precios de cada producto
- `despachogramaje` es un arreglo bidimensional de reales que almacena el precio de despacho de los articulos según sus dimensiones `región` y `peso`, ambas declaradas como reales
- `regiones` es un arreglo unidimensional de caracteres que almacena las opciones de despacho para todas las regiones de Chile.
- `x`e `i` y `promedio` son enteros que se usaron para controlar los bucles y realizar cálculos.

```scss
Definir n,p Como Entero
Definir despachogramaje, region, peso Como Real
Definir regiones como Caracter
Definir x,i Como Entero
```

2. Se solicita al usuario que ingrese el número de productos comprados:
- Se muestra mensaje en la pantalla: _"Ingresa el número de productos comprados:"_
- El número de productos comprados se lee y se guarda en la variable `n`

```scss
Escribir "Ingresa el número de productos comprados: "
Leer n
```

3. Se utiliza un bucle `Para` para leer los precios de los productos:
- El bucle se ejecuta `n` veces para leer los precios de los productos.
- En cada iteración del bucle, se solicita al usuario que ingrese el precio del producto.

```scss
Para producto desde 1 hasta n Hacer
Escribir "Producto ", producto	
Escribir "Ingrese el precio del producto ", producto
Leer p
```
4. Dentro del mismo bucle, luego de ingresar el precio de cada producto, se le solicita al usuario ingresar "verdadero" o "falso", según si cada producto tiene o no un cupón de descuento.
- Se muestra mensaje en la pantalla: _"Indique VERDADERO o FALSO si el producto tiene un cupon de descuento"_
- La respuesta se lee y se guarda en la variable `cupon_descuento`

```scss
Escribir "Indique VERDADERO o FALSO si el producto tiene un cupon de descuento "
Leer cupon_descuento
```
5. Se utiliza la estructura de control SI para comprobar la respuesta, si la respuesta es verdadera, se aplica un descuento de 15% al producto y se guarda en la variante `precioconcupon`
En caso de que la respuesta sea falsa, no se aplica descuento y el precio `p` queda registrado en la variante `precionormal`.
Luego para ambos casos se guarda el precio total final con la variante `precio_bruto`.

```scss
si (cupon_descuento = VERDADERO) entonces
precioconcupon <- p * 0.85
			
Escribir  "¡Se ha aplicado un descuento de 15%! El valor del producto ", producto, " con descuento aplicado es de: $", precioconcupon
precio_bruto <- precio_bruto + precioconcupon // Sumar el consumo con descuento al total
			
sino precionormal <- p
			
Escribir  "Hoy no tienes descuento extra, el valor del producto ", producto, " es: $", precionormal
precio_bruto <- precio_bruto + precionormal // Sumar el consumo al total
			
fin si
```

6. Se muestra un resumen hasta este punto con la información recopilada.

```scss
Escribir "El número de productos en tu carro es de ", n ," y el precio total de tu carrito es de: $", precio_bruto
```

7. Luego, en caso de que el número de articulos comprados `n` sea mayor o igual a 3, se aplicará un descuento extra del 10%.
- Se utiliza la estructura de control SI para comprobar el valor de `n`
- Ambos resultados quedan guardados en la variante `preciocondescuento`

```scss
Si n>=3 Entonces
preciocondescuento <- precio_bruto * 0.90
Escribir "¡Felicidades! Tienes 3 o más productos en tu carro, por lo que se te ha aplicado un descuento extra de 10%, el nuevo valor de tu carrito: $" preciocondescuento
SiNo 
preciocondescuento <- precio_bruto
Escribir "Tu compra no califica para acceder al descuento, el valor de tus productos es de $: " preciocondescuento
FinSi
```

8. Se aplica iva al total de la compra.
- Se lee y guarda el valor total más iva aplicado en la variante `subtotal_producto`

```scss
Escribir "Aplicación de impuestos a tu compra:"
subtotal_producto <- preciocondescuento * 1.19
Escribir "El total de tu carrito, con iva incluido, es: $" subtotal_producto 
```
Una vez completados los puntos anteriores se comienza a calcular la tarifa de despacho.

9. Se aplica un arreglo unidimensional para registrar las regiones de despacho disponibles para envío, en este caso son todas las regiones de Chile.
- Se define la dimensión `región[15]`

```scss
Dimension regiones[15]
	
regiones[1] <-"Arica y Parinacota"	
regiones[2] <-"Tarapacá"
regiones[3] <-"Antofagasta"
regiones[4] <-"Atacama"
regiones[5] <-"Coquimbo"
regiones[6] <-"Valparaiso"
regiones[7] <-"Metropolitana"
regiones[8] <-"OHiggins"
regiones[9] <-"Maule"
regiones[10] <-"Biobio"
regiones[11] <-"Araucania"
regiones[12] <-"Rios"
regiones[13] <-"Lagos"
regiones[14] <-"Aysén"
regiones[15] <-"Magallanes"
```

10. Se aplica un arreglo bidimensional donde se registró la tarifa de despacho según peso y por región.
- Se define la dimensión `despachogramaje[15,4]`, donde el primer campo corresponde a las regiones de Chile, y el segundo campo correponde a el peso del producto según el segmento donde se encuentra.
- Segmento 1: Para articulos de entre 0 a 1 kilo
- Segmento 2: Para articulos de entre 1 a 3 kilos
- Segmento 3: Para articulos de entre 3 a 6 kilos
- Segmento 4: Para articulos de más de 6 kilos

Visualmente el arreglo se ve de la siguiente manera:

| Región/Peso  | Entre 0 a 1 kilo | Entre 1 a 3 kilos  | Entre 3 a 6 kilos | Más de 6 kilos |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| Arica y Parinacota  | $7.850  | $10.100 | $13.300 | $15.100 |
| Tarapacá  | $7.850  | $10.100 | $13.300 | $15.100 |
| Antofagasta  | $7.500  | $9.800 | $12.500 | $14.900 |
| Atacama  | $4.400  | $7.600 | $9.900 | $11.300 |
| Coquimbo  | $4.400  | $7.600 | $9.900 | $11.300 |
| Valparaiso  | $4.200  | $7.400 | $9.700 | $11.100 |
| Metropolitana  | $2.900  | $4.800 | $6.000 | $7.900 |
| OHiggins  | $3.700  | $6.900 | $8.600 | $10.900 |
| Maule  | $3.700  | $6.900 | $8.600 | $10.900 |
| Biobio | $3.700  | $6.900 | $8.600 | $10.900 |
| Araucanía  | $4.100  | $7.400 | $9.600 | $11.300 |
| Los Ríos  | $4.100  | $7.400 | $9.600 | $11.300 |
| Los Lagos  | $4.100  | $7.400 | $9.600 | $11.300 |
| Aysén  | $7.000  | $10.300 | $12.500 | $14.800 |
| Magallanes  | $7.000  | $10.300 | $12.500 | $14.800 |

```scss
// Despachos a la región de Arica y Parinacota
despachogramaje[1,1]=7850
despachogramaje[1,2]=10100
despachogramaje[1,3]=13300
despachogramaje[1,4]=15100

//y asi sucesivamente para todas las regiones
```

11. Se muestra en pantalla las regiones de Chile del arreglo unidimensional mediante un bucle `para`, habiendo definidio que `x=15` y `i=0`

```scss
Escribir "Opciones de despacho a todo Chile:"
Para i=1 hasta x con paso 1 hacer
Escribir "#",i," para la región de ", regiones[i]
FinPara
```

12. Se le pide al usuario que ingrese su región correspondiente a su domicilio, mediante la selección del número del 1 al 15, indicado en el paso anterior.
- Se muestra mensaje en la pantalla: _"Ingrese el número correspondiente a la región donde quiere que realizemos el despacho:"_
- La respuesta se lee y se guarda en la variable `regioningresada`

```scss
Escribir "Ingrese el número correspondiente a la región donde quiere que realizemos el despacho: "
Leer regioningresada
```

13. Se le pide al usuario que ingrese el peso total de los articulos comprados en kilos.
- Se muestra mensaje en la pantalla: _"Ingrese el peso total (en kilos) de los articulos agregados en su carrito:"_
- La respuesta se lee y se guarda en la variable `m`

```scss
Escribir "Ingrese el peso total (en kilos) de los articulos agregados en su carrito: "
Leer m
```

14. Una vez ingresado el peso del producto, se revisa a que segmento pertenece (1, 2, 3 o 4), mediante una estructura de control SI.
- La respuesta ingresada se lee y se guarda en la variante `pesoproducto`

```scss
Si m >= 0 y m < 1 Entonces
pesoproducto<-1
FinSi
	
Si m >= 1 y m < 3 Entonces
pesoproducto<-2
FinSi
	
Si m >= 3 y m < 6 Entonces
pesoproducto<-3
FinSi
	
Si m >= 6 Entonces
pesoproducto<-4
FinSi
```

15. Se muestra en pantalla el valor total del despacho según la región y peso ingresados, se lee `despachogramaje[regioningresada,pesoproducto]`
El resultado además se guarda en la variante `valordespacho`

```scss
Escribir "El valor del despacho de su compra para la región ingresada es de: $" despachogramaje[regioningresada,pesoproducto]
valordespacho <- despachogramaje[regioningresada,pesoproducto]
```

16. Se calcula el valor total a pagar, considerando el precio total de los productos, con descuentos e iva aplicados, más el valor de despacho. Se suman las variantes `valordespacho` y `subtotal_producto` y se lee y guarda el resultado en la variante `valortotal`

```scss
valortotal <- valordespacho+subtotal_producto
```

17. Se muestra en pantalla el valor total a cancelar
```scss
Escribir "¡Ya estas listo para ir al checkout! El valor total a pagar es de: $" valortotal
```

18. La solución en conjunto sería:

```scss
Algoritmo ProyectoM1
	
// Declaración de variables
	
Definir n,p Como Entero // número de articulos comprados // precio del producto
Definir despachogramaje, region, peso Como real
Definir regiones como caracter
Definir x,i Como Entero
	
// Ingreso de datos
	
Escribir "Ingresa el número de productos comprados: "
Leer n
	
Para producto desde 1 hasta n Hacer
  Escribir "Producto ", producto
		
  Escribir "Ingrese el precio del producto ", producto
  Leer p
				
  Escribir "Indique VERDADERO o FALSO si el producto tiene un cupon de descuento "
  Leer cupon_descuento
		
  si (cupon_descuento = VERDADERO) entonces
    precioconcupon <- p * 0.85
			
    Escribir  "¡Se ha aplicado un descuento de 15%! El valor del producto ", producto, " con descuento aplicado es de: $", precioconcupon
    precio_bruto <- precio_bruto + precioconcupon // Sumar el consumo con descuento al total
			
  sino precionormal <- p
			
    Escribir  "Hoy no tienes descuento extra, el valor del producto ", producto, " es: $", precionormal
    precio_bruto <- precio_bruto + precionormal // Sumar el consumo al total
			
  fin si
		
  Escribir "---------------------------------------"
		
FinPara
	
	
Escribir "El número de productos en tu carro es de ", n ," y el precio total de tu carrito es de: $", precio_bruto // Mostrar el subtotal de todos los productos
	
Escribir "---------------------------------------"
	
//Aplicar descuento del 10% sobre 3 cantidad de productos
	
Si n>=3 Entonces // 
  preciocondescuento <- precio_bruto * 0.90
  Escribir "¡Felicidades! Tienes 3 o más productos en tu carro, por lo que se te ha aplicado un descuento extra de 10%, el nuevo valor de tu carrito: $" preciocondescuento
SiNo 
  preciocondescuento <- precio_bruto
  Escribir "Tu compra no califica para acceder al descuento, el valor de tus productos es de $: " preciocondescuento
FinSi

Escribir "---------------------------------------"
	
//aplicar iva
	
Escribir "Aplicación de impuestos a tu compra:"
subtotal_producto <- preciocondescuento * 1.19
Escribir "El total de tu carrito, con iva incluido, es: $" subtotal_producto 
	
Escribir "---------------------------------------"

//Aplicar precio despacho
	
Dimension regiones[15]
	
regiones[1] <-"Arica y Parinacota"
regiones[2] <-"Tarapacá"
regiones[3] <-"Antofagasta"
regiones[4] <-"Atacama"
regiones[5] <-"Coquimbo"
regiones[6] <-"Valparaiso"
regiones[7] <-"Metropolitana"
regiones[8] <-"OHiggins"
regiones[9] <-"Maule"
regiones[10] <-"Biobio"
regiones[11] <-"Araucania"
regiones[12] <-"Rios"
regiones[13] <-"Lagos"
regiones[14] <-"Aysén"
regiones[15] <-"Magallanes"
	
	
Dimension despachogramaje[15,4]
	
x=15; i=0
	
// Despachos a la región de Arica y Parinacota
despachogramaje[1,1]=7850 // Para articulos de entre 0 a 1 kilo 
despachogramaje[1,2]=10100 // Para articulos de entre 1 a 3 kilos
despachogramaje[1,3]=13300 // Para articulos de entre 3 a 6 kilos
despachogramaje[1,4]=15100 // Para articulos de más de 6 kilos
	
// Despachos a la región de Tarapacá
despachogramaje[2,1]=7850 // Para articulos de entre 0 a 1 kilo
despachogramaje[2,2]=10100 // Para articulos de entre 1 a 3 kilos
despachogramaje[2,3]=13300 // Para articulos de entre 3 a 6 kilos
despachogramaje[2,4]=15100 // Para articulos de más de 6 kilos
	
// Despachos a la región de Antofagasta
despachogramaje[3,1]=7500 // Para articulos de entre 0 a 1 kilo
despachogramaje[3,2]=9800 // Para articulos de entre 1 a 3 kilos
despachogramaje[3,3]=12500 // Para articulos de entre 3 a 6 kilos
despachogramaje[3,4]=14900 // Para articulos de más de 6 kilos
	
// Despachos a la región de Atacama
despachogramaje[4,1]=4400 // Para articulos de entre 0 a 1 kilo
despachogramaje[4,2]=7600 // Para articulos de entre 1 a 3 kilos
despachogramaje[4,3]=9900 // Para articulos de entre 3 a 6 kilos
despachogramaje[4,4]=11300 // Para articulos de más de 6 kilos
	
// Despachos a la región de Coquimbo
despachogramaje[5,1]=4400 // Para articulos de entre 0 a 1 kilo
despachogramaje[5,2]=7600 // Para articulos de entre 1 a 3 kilos
despachogramaje[5,3]=9900 // Para articulos de entre 3 a 6 kilos
despachogramaje[5,4]=11300 // Para articulos de más de 6 kilos
	
// Despachos a la región de Valparaiso
despachogramaje[6,1]=4200 // Para articulos de entre 0 a 1 kilo
despachogramaje[6,2]=7400 // Para articulos de entre 1 a 3 kilos
despachogramaje[6,3]=9700 // Para articulos de entre 3 a 6 kilos
despachogramaje[6,4]=11100 // Para articulos de más de 6 kilos
	
// Despachos a la región Metropolitana
despachogramaje[7,1]=2900 // Para articulos de entre 0 a 1 kilo
despachogramaje[7,2]=4800 // Para articulos de entre 1 a 3 kilos
despachogramaje[7,3]=6000 // Para articulos de entre 3 a 6 kilos
despachogramaje[7,4]=7900 // Para articulos de más de 6 kilos
	
// Despachos a la región de OHiggins
despachogramaje[8,1]=3700 // Para articulos de entre 0 a 1 kilo
despachogramaje[8,2]=6900 // Para articulos de entre 1 a 3 kilos
despachogramaje[8,3]=8600 // Para articulos de entre 3 a 6 kilos
despachogramaje[8,4]=10900 // Para articulos de más de 6 kilos
	
// Despachos a la región de Maule
despachogramaje[9,1]=3700 // Para articulos de entre 0 a 1 kilo
despachogramaje[9,2]=6900 // Para articulos de entre 1 a 3 kilos
despachogramaje[9,3]=8600 // Para articulos de entre 3 a 6 kilos
despachogramaje[9,4]=10900 // Para articulos de más de 6 kilos
	
// Despachos a la región de Biobio
despachogramaje[10,1]=3700 // Para articulos de entre 0 a 1 kilo
despachogramaje[10,2]=6900 // Para articulos de entre 1 a 3 kilos
despachogramaje[10,3]=8600 // Para articulos de entre 3 a 6 kilos
despachogramaje[10,4]=10900 // Para articulos de más de 6 kilos
	
// Despachos a la región de Araucania
despachogramaje[11,1]=4100 // Para articulos de entre 0 a 1 kilo
despachogramaje[11,2]=7400 // Para articulos de entre 1 a 3 kilos
despachogramaje[11,3]=9600 // Para articulos de entre 3 a 6 kilos
despachogramaje[11,4]=11300 // Para articulos de más de 6 kilos
	
// Despachos a la región de Los Rios
despachogramaje[12,1]=4100 // Para articulos de entre 0 a 1 kilo
despachogramaje[12,2]=7400 // Para articulos de entre 1 a 3 kilos
despachogramaje[12,3]=9600 // Para articulos de entre 3 a 6 kilos
despachogramaje[12,4]=11300 // Para articulos de más de 6 kilos
	
// Despachos a la región de Los Lagos
despachogramaje[13,1]=4100 // Para articulos de entre 0 a 1 kilo
despachogramaje[13,2]=7400 // Para articulos de entre 1 a 3 kilos
despachogramaje[13,3]=9600 // Para articulos de entre 3 a 6 kilos
despachogramaje[13,4]=11300 // Para articulos de más de 6 kilos
	
// Despachos a la región de Aysen
despachogramaje[14,1]=7000 // Para articulos de entre 0 a 1 kilo
despachogramaje[14,2]=10300 // Para articulos de entre 1 a 3 kilos
despachogramaje[14,3]=12500 // Para articulos de entre 3 a 6 kilos
despachogramaje[14,4]=14800 // Para articulos de más de 6 kilos
	
// Despachos a la región de Magallanes
despachogramaje[15,1]=7000 // Para articulos de entre 0 a 1 kilo
despachogramaje[15,2]=10300 // Para articulos de entre 1 a 3 kilos
despachogramaje[15,3]=12500 // Para articulos de entre 3 a 6 kilos
despachogramaje[15,4]=14800 // Para articulos de más de 6 kilos
	

Escribir "Opciones de despacho a todo Chile:"
Para i=1 hasta x con paso 1 hacer
  Escribir "#",i," para la región de ", regiones[i]
FinPara
	
Escribir "Ingrese el número correspondiente a la región donde quiere que realizemos el despacho: "
Leer regioningresada
	
Escribir "---------------------------------------"
	
Escribir "Ingrese el peso total (en kilos) de los articulos agregados en su carrito: "
Leer m

Si m >= 0 y m < 1 Entonces
  pesoproducto<-1
FinSi
	
Si m >= 1 y m < 3 Entonces
  pesoproducto<-2
FinSi
	
Si m >= 3 y m < 6 Entonces
  pesoproducto<-3
FinSi
	
Si m >= 6 Entonces
  pesoproducto<-4
FinSi
	
Escribir "El valor del despacho de su compra para la región ingresada es de: $" despachogramaje[regioningresada,pesoproducto]
	
valordespacho <- despachogramaje[regioningresada,pesoproducto]
	
valortotal <- valordespacho+subtotal_producto
Escribir "---------------------------------------"
		
Escribir "¡Ya estas listo para ir al checkout! El valor total a pagar es de: $" valortotal
	
Escribir "---------------------------------------"

FinAlgoritmo
	
```

