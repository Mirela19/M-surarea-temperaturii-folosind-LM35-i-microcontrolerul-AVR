## Componente utilizate
- microcontroller ATMEGA328
- 2x condensator 100uF
- condensator 100nF
- senzor de temperatură LM35
- alimentare 5V
- programator AVR-ISP
- afișaj LCD 16x2
- breadboard
- fire

### Senzorul de temperatură LM35
LM35 este un senzor de temperatură cu o calibrare de 1 ° C de variație. 
Desigur, acest lucru nu înseamnă că toți senzorii de temperatură sunt pregătiți pentru grade Celcius, dar în acest caz se întâmplă. De fapt, este ceva ce trebuie 
adaptat ulterior pentru a-l calibra și a-l face să măsoare în funcție de cerințele fiecărui proiect.
La ieșire generează un semnal analogic de tensiune diferită în funcție de temperatura pe care o captează la un moment dat.

De obicei acoperă temperaturile de măsurare între -55ºC și 150ºC. Gama de temperatură este limitată de cantitatea de tensiuni variabile pe care 
o poate avea la ieșire, variind de la -550mV la 1500mV.

Măsurarea unei temperaturi 150ºC știm deja că va da 1500mV la ieșire. În timp ce dacă avem -550mV înseamnă că măsoară -55ºC.
Nu toți senzorii de temperatură au aceleași domenii de tensiune, unii pot varia. Temperaturile intermediare vor trebui să fie calculate folosind formule 
simple cunoscând aceste două limite. De exemplu, cu o regulă de trei.


### Caracteristici tehnice
-Tensiunea de ieșire proporțională cu temperatura: de la -55ºC la 150ºC cu tensiuni de la -550mV la 1500mV
-Calibrat pentru grade Celcius
-Tensiune de precizie garantată de la 0.5ºC la 25ºC
-Impedanță scăzută de ieșire
-Curent redus de alimentare (60 μA).
-Cost scăzut
-Pachet SOIC, TO-220, TO-92, TO-CAN etc.
-Tensiune de lucru între 4 și 30v

![caract si fisa tehnica](https://user-images.githubusercontent.com/56684731/171592577-0d84909d-c9b6-4389-9811-e98b026a529a.PNG
