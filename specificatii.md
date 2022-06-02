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

### Conexiunile pentru LCD- explicații
În circuit puteți vedea că am folosit comunicarea pe 8 biți (D0-D7), dar aceasta nu este obligatorie, putem folosi comunicarea pe 4 biți (D4-D7), dar cu comunicarea pe 4 biți, programul devine puțin complex, așa că am ales pe 8 biți. comunicare.

Deci, din simpla observație din tabelul de mai sus, conectăm 10 pini ai LCD-ului la controler, în care 8 pini sunt pini de date și 2 pini pentru control. Tensiunea de ieșire furnizată de senzor nu este complet liniară; va fi unul zgomotos. Pentru a filtra zgomotul, trebuie plasat un condensator la ieșirea senzorului, așa cum se arată în figură.

Înainte de a merge mai departe, trebuie să vorbim despre ADC al ATMEGA32A. În ATMEGA32A, putem da intrare analogică la oricare dintre cele opt canale ale PORTA, nu contează ce canal alegem, deoarece toate sunt la fel. Vom alege canalul 0 sau PIN0 al PORTA. În ATMEGA32A, ADC-ul are o rezoluție de 10 biți, astfel încât controlerul poate detecta o schimbare minimă a Vref/2^10, deci dacă tensiunea de referință este de 5V, obținem un increment de ieșire digitală pentru fiecare 5/2^10 = 5mV . Deci, pentru fiecare creștere de 5 mV în intrare, vom avea o creștere de unu la ieșirea digitală.

Acum trebuie să setăm registrul ADC pe baza următorilor termeni:

1. În primul rând, trebuie să activăm funcția ADC în ADC.

2. Deoarece măsurăm temperatura camerei, nu avem nevoie de valori mai mari de o sută de grade (ieșire de 1000 mV a LM35). Deci putem seta valoarea maximă sau referința ADC la 2,5V.

3. Controlerul are o funcție de conversie a declanșatorului, ceea ce înseamnă că conversia ADC are loc numai după un declanșare extern, deoarece nu dorim să fie nevoie să setăm registrele pentru ca ADC să ruleze în modul de rulare liberă continuă.

4. Pentru orice ADC, frecvența de conversie (valoare analogică în valoare digitală) și acuratețea ieșirii digitale sunt invers proporționale. Deci, pentru o mai bună acuratețe a ieșirii digitale, trebuie să alegem o frecvență mai mică. Pentru un ceas ADC mai mic, setăm prevânzarea ADC la valoarea maximă (128). Deoarece folosim ceasul intern de 1MHZ, ceasul ADC va fi (1000000/128).

Acestea sunt singurele patru lucruri pe care trebuie să le știm pentru a începe cu ADC. Toate cele patru caracteristici de mai sus sunt setate de două registre.
