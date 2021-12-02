Error 1:Uncaught TypeError: guessSubmit.addeventListener is not a function at index.html:87
Indica un error en la línea 87, es de sintaxis por que debe ser: addEventListener, la primera E debe ser mayúscula.

Error 2: index.html:79 Uncaught TypeError: Cannot set properties of null (setting 'textContent')
    at HTMLInputElement.checkGuess (index.html:79)

Es un error que está apuntando a a un selector de clase, sin embargo no lo reconoce porque las clases CSS se inician con un . por lo que la solución es:
escribir en la línea 49 lo siguiente: const lowOrHi = document.querySelector('.lowOrHi');	

Error 3: Uncaught TypeError: resetButton.addeventListener is not a function
    at setGameOver (index.html:95)
    at HTMLInputElement.checkGuess (index.html:72)
	
	aquí también hay un error de sintaxis en la línea 95: se corrige de la siguiente manera: resetButton.addEventListener('click', resetGame);
	

Error 4: El Sistema acepta valores decimales, lo que no es correcto según el caso de uso 1 y 2.


Error 5: El caso de uso indica que debe ser números del 1 al 100, sin embargo al realizar 
5 intentos utilizando valores mayores a 100, o un mismo número dentro del rango devuelve un mensaje de éxito, lo que no es correcto.
 
Error 6:   const ATTEMPS = 5;
Esta variable se usa como contador y el caso de uso dice que deben ser 10 intentos, está seteada con 5 por lo que se cambia a 10

Error 7: else if(guessCount === ATTEMPS) {
      lastResult.textContent = 'Felicitaciones! adivinaste el número!';

El error está en la línea 70	 
Aquí el fallo se da porque el sistema está entendiendo que después de los intentos que el usuario realiza debe desplegar un mensaje de error indicando que ha perdido
por lo que lo correcto es que se corriga la línea 64 en donde está este bloque de código que inicia en la línea 64 y termina en la :

if(userGuess === randomNumber) {
      lastResult.textContent = '!!!Pérdistes!!!';
      lastResult.style.backgroundColor = 'black';
      lowOrHi.textContent = '';
      setGameOver();
    } else if(guessCount === ATTEMPS) {
      lastResult.textContent = 'Felicitaciones! adivinaste el número!';
      lastResult.style.backgroundColor = 'green';
      setGameOver();
    } else {
      lastResult.textContent = 'Incorrecto! ';
      lastResult.style.backgroundColor = 'red';
      if(userGuess < randomNumber) {
        lowOrHi.textContent = 'El número es mayor!';
      } else if(userGuess > randomNumber) {
        lowOrHi.textContent = 'El número es menor!';
      }
    }
	
y debe quedar de la siguiente manera:

if(userGuess === ATTEMPS) {
      lastResult.textContent = '!!!Pérdistes!!!';
      lastResult.style.backgroundColor = 'black';
      lowOrHi.textContent = '';
      setGameOver();
    } else if(guessCount === randomNumber) {
      lastResult.textContent = 'Felicitaciones! adivinaste el número!';
      lastResult.style.backgroundColor = 'green';
      setGameOver();
} else {
      lastResult.textContent = 'Incorrecto! ';
      lastResult.style.backgroundColor = 'red';
      if(userGuess < randomNumber) {
        lowOrHi.textContent = 'El número es mayor!';
      } else if(userGuess > randomNumber) {
        lowOrHi.textContent = 'El número es menor!';
      }
    }

Error 8: en la línea 64 
if(userGuess === ATTEMPS)
 nunca saldrá del bucle porque la variable userGuess no tiene el total de intentos que se solicita, se debe cambiar por la siguiente:
 
 if(guessCount === ATTEMPS) {

Error 9:
Al momento de acertar, da la sensación de equivocarse debido a que el color utilizado es el rojo, y mientras se equivoca el color es el verde
como buena práctica para interactuar con el sistema se debe hacer un cambio en los colores utilizados por mera regla de negocio.
en las líneas:
66: lastResult.style.backgroundColor = 'black'; se cambia a red
71: lastResult.style.backgroundColor = 'red'; se cambia a 'green'
75: lastResult.style.backgroundColor = 'green'; se cambia a 'black'