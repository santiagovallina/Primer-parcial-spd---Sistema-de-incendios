# Primer parcial spd - Sistema de incendios

------------

![](https://canaltic.com/blog/wp-content/uploads/2020/08/pc17.jpg)


------------

### Alumno
- Santiago Julián Vallina


------------
## Proyecto: Sistema de incendios

![](https://scontent.feze10-1.fna.fbcdn.net/v/t39.30808-6/446934684_8051461558197640_9100358084030248672_n.jpg?stp=dst-jpg_p180x540&_nc_cat=108&ccb=1-7&_nc_sid=5f2048&_nc_eui2=AeGnjpC90CBe4GIAsB2WzrbGKnoqg0kN-MUqeiqDSQ34xZJChw5j5_kEsgxWanX5pMDhdoyP6B0SitHHrtmF7zDY&_nc_ohc=HFi3hPURU-kQ7kNvgFYwg3r&_nc_ht=scontent.feze10-1.fna&oh=00_AYAvmvOIYiuy0qkUWAxuUq4eraxFzGY8iMxxIwYx9jC7Nw&oe=665E6291)


------------

### Descripción

Mide la temperatura mediante el sensor de temperatura. Muestra el nivel de temperatura con el display de 7 segmentos. En caso de estar en altos niveles de temperatura, enciende los leds en forma de alarma diciendo que hay un incendio. Si hay un incendio prende el servo motor para abrir una válvula de agua.


------------

## Funciones 

#### Void loop
```cpp
void loop()
{
	bool nuevoEstadoBotonUno = digitalRead(BOTON_UNO);
    bool nuevoEstadoBotonDos = digitalRead(BOTON_DOS);

    if (nuevoEstadoBotonUno == HIGH && estadoBotonUno == LOW) 
    {
      contador++;
      delay(200); 
    }
    estadoBotonUno = nuevoEstadoBotonUno;

    if(nuevoEstadoBotonDos == HIGH && estadoBotonDos == LOW) 
    {
      contador = 0;
      ApagarTodos(200);
      delay(200);
    }
    estadoBotonDos = nuevoEstadoBotonDos;

    if (contador > 0) 
    {
       lecturaDelSensor = analogRead(A0);
       temperatura = map(lecturaDelSensor, 20, 358, -40, 125);
        
       if (temperatura < 30) 
        {
           EncenderCero(1000);
        } 
      	else if (temperatura > 29 && temperatura < 35) 
        {
           EncenderUno(1000);
        } 
      	else if (temperatura > 34 && temperatura < 40) 
        {
           EncenderDos(1000);
        } 
      	else if (temperatura > 39 && temperatura < 45) 
        {
           EncenderTres(1000);
        } 
      	else if (temperatura > 44 && temperatura < 50) 
        {
           EncenderCuatro(1000);
        } 
      	else if (temperatura > 49 && temperatura < 55) 
        {
           EncenderCinco(1000);
        } 
      	else if (temperatura > 54 && temperatura < 60) 
        {
           EncenderSeis(1000);
        } 
      	else if (temperatura > 59 && temperatura < 65) 
        {
           EncenderSiete(500);
           EncenderLed(500);
           MoverServo(90);          	
        } 
      	else if (temperatura > 64 && temperatura < 70) 
        {
           EncenderOcho(500);
           EncenderLed(500);
           MoverServo(90);
        } 
      	else 
        {
           EncenderNueve(500);
           EncenderLed(500);
           MoverServo(90);
        }
    }
  if (contador == 0) 
  {
    ApagarTodos(500);
  }
  
}
```

------------

#### Mover servo

```cpp
void MoverServo(int posicion)
{
  for (posicion = 0; posicion <= 180;)
  {
  	servo1.write(posicion);
    delay(30);
  }
}
```


------------

#### Prender y apagar leds 
```cpp
void EncenderLed(int tiempo)
{
  digitalWrite(13, HIGH);
  digitalWrite(12, HIGH);
  delay(tiempo);
  digitalWrite(13, LOW);
  digitalWrite(12, LOW);
  delay(tiempo);
}
```


------------

#### Encender números del display

```cpp
void EncenderCero(int tiempo)
{
  digitalWrite(F, HIGH);
  digitalWrite(A, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(E, HIGH);
  digitalWrite(D, HIGH);
  digitalWrite(C, HIGH);
  delay(tiempo);
  digitalWrite(F, LOW);
  digitalWrite(A, LOW);
  digitalWrite(B, LOW);
  digitalWrite(E, LOW);
  digitalWrite(D, LOW);
  digitalWrite(C, LOW);
}

void EncenderUno(int tiempo)
{
  digitalWrite(C, HIGH);
  digitalWrite(B, HIGH);
  delay(tiempo);
  digitalWrite(C, LOW);
  digitalWrite(B, LOW);
}

void EncenderDos(int tiempo)
{
  digitalWrite(G, HIGH);
  digitalWrite(A, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(E, HIGH);
  digitalWrite(D, HIGH);
  delay(tiempo);
  digitalWrite(G, LOW);
  digitalWrite(A, LOW);
  digitalWrite(B, LOW);
  digitalWrite(E, LOW);
  digitalWrite(D, LOW);
}

void EncenderTres(int tiempo)
{
  digitalWrite(A, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(G, HIGH);
  digitalWrite(C, HIGH);
  digitalWrite(D, HIGH);
  delay(tiempo);
  digitalWrite(A, LOW);
  digitalWrite(B, LOW);
  digitalWrite(G, LOW);
  digitalWrite(C, LOW);
  digitalWrite(D, LOW);
}

void EncenderCuatro(int tiempo)
{
  digitalWrite(C, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(G, HIGH);
  digitalWrite(F, HIGH);
  delay(tiempo);
  digitalWrite(C, LOW);
  digitalWrite(B, LOW);
  digitalWrite(G, LOW);
  digitalWrite(F, LOW);
}

void EncenderCinco(int tiempo)
{
  digitalWrite(C, HIGH);
  digitalWrite(D, HIGH);
  digitalWrite(G, HIGH);
  digitalWrite(F, HIGH);
  digitalWrite(A, HIGH);
  delay(tiempo);
  digitalWrite(C, LOW);
  digitalWrite(D, LOW);
  digitalWrite(G, LOW);
  digitalWrite(F, LOW);
  digitalWrite(A, LOW);
}

void EncenderSeis(int tiempo)
{
  digitalWrite(C, HIGH);
  digitalWrite(D, HIGH);
  digitalWrite(G, HIGH);
  digitalWrite(F, HIGH);
  digitalWrite(A, HIGH);
  digitalWrite(E, HIGH);
  delay(tiempo);
  digitalWrite(C, LOW);
  digitalWrite(D, LOW);
  digitalWrite(G, LOW);
  digitalWrite(F, LOW);
  digitalWrite(A, LOW);
  digitalWrite(E, LOW);
}

void EncenderSiete(int tiempo)
{
  digitalWrite(C, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(A, HIGH);
  delay(tiempo);
  digitalWrite(C, LOW);
  digitalWrite(B, LOW);
  digitalWrite(A, LOW);
}

void EncenderOcho(int tiempo)
{
  digitalWrite(A, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(C, HIGH);
  digitalWrite(D, HIGH);
  digitalWrite(E, HIGH);
  digitalWrite(F, HIGH);
  digitalWrite(G, HIGH);
  delay(tiempo);
  digitalWrite(A, LOW);
  digitalWrite(B, LOW);
  digitalWrite(C, LOW);
  digitalWrite(D, LOW);
  digitalWrite(E, LOW);
  digitalWrite(F, LOW);
  digitalWrite(G, LOW);
}

void EncenderNueve(int tiempo)
{
  digitalWrite(C, HIGH);
  digitalWrite(B, HIGH);
  digitalWrite(G, HIGH);
  digitalWrite(F, HIGH);
  digitalWrite(A, HIGH);
  delay(tiempo);
  digitalWrite(C, LOW);
  digitalWrite(B, LOW);
  digitalWrite(G, LOW);
  digitalWrite(F, LOW);
  digitalWrite(A, LOW);
}
```


------------

#### Apagar display

```cpp
void ApagarTodos(int tiempo) 
{
    digitalWrite(F, LOW);
    digitalWrite(A, LOW);
    digitalWrite(B, LOW);
    digitalWrite(E, LOW);
    digitalWrite(D, LOW);
    digitalWrite(C, LOW);
    digitalWrite(G, LOW);
    digitalWrite(13, LOW);
    digitalWrite(12, LOW);
}
```


------------

## Link al proyecto
[Proyecto sistema de incendios](https://www.tinkercad.com/things/8gj3Lk94jtR-primer-parcial-sistema-de-incendios-santiago-vallina/editel "Proyecto sistema de incendios")
