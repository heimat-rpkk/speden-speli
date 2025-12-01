# Speden speli

**Pseudokoodi**

```
lamput = []
painallukset[]
t-on = palamisaika
t-off = väliaika
pisteet = 0

funktio sytytä-lamppu():
  arvo satunnainen indeksi 0-3 -> i 
  lisää i taulukkoon lamput
  sytytä lamppu i
  käynnistä timer-on(i)


funktio timer-on(i):
  kun aika t-on on kulunut, sammuta lamppu i ja käynnistä timer-off()


funktio timer-off():
  kun aika t-off on kulunut, sytytä-lamppu()


tapahtumakuuntelija(nappi 0, 1, 2, 3):
  jos nappia on painettu:
    lisää nappi taulukkoon painallukset
  jos lamput ei ole tyhjä:
    ota painallukset[0] -> p
	jos p == lamput[pisteet]:
	  // oikein
	  pisteet++
      tulosta pisteet
	muuten:
	  // väärin
	  lopeta peli
      
timer-off()

```

---

## JavaScript Timer

Timer, joka ei blokkaa eli sillä aikaa muut toiminnot (esim. klikkaukset, animaatiot) toimivat normaalisti.

**`setTimeout()`**

Suorittaa tietyn funktion **kerran** tietyn ajan kuluttua, eikä pysäytä muuta koodia.

```js
setTimeout(() => {
  console.log("Aika loppui!");
  suoritaKunAikaLoppuu(); // funktiokutsu
}, 1000); // 1000 ms = 1s
```

**`setInterval()`**

Suorittaa funktion **toistuvasti** tietyin aikavälein.

```js
const id = setInterval(() => {
  console.log("Tick");
  suoritaToistuvasti(); // funktiokutsu
}, 500);

// Lopetus:
clearInterval(id);
```

---
## Tapahtumakuuntelija

Alla esimerkki, joka kuuntelee kaikkia `<button>`-elementtejä, ja kun nappia klikataan, sen id tallennetaan taulukkoon.

```js
const painallukset = [];

// Hae kaikki button-elementit
const napit = document.querySelectorAll('button');

// Lisää jokaiselle kuuntelija
napit.forEach(nappi => {
  nappi.addEventListener('click', () => {
    painallukset.push(nappi.id);
    console.log(painallukset);
  });
});

```


---

## JS ja css-tyylin muuttaminen
Miten yksittäisiä tyylejä voi muuttaa suoraan JavaScriptillä ja tarkistaa niitä if-lauseella

```js
const nappi = document.getElementById('nappi');
nappi.style.backgroundColor = 'green'; // taustaväri
nappi.style.color = 'black'; // tekstiin väri
if (nappi.style.color === 'black') {
    nappi.style.fontSize = '30px';
  } else {
    nappi.style.fontSize = '10px';
  }
nappi.style.border = '2px solid black';
```

`nappi.style.<ominaisuus>` käsittelee vain **inline**-tyylejä, ei **CSS-tiedostosta perittyjä** tyylejä.

Jos haluat tarkistaa **CSS-tiedostossa** määritellyn (perityn) tyylin, käytä `getComputedStyle`.

```js
const tyyli = getComputedStyle(nappi);
console.log(tyyli.backgroundColor); // esim. "rgb(255, 0, 0)"
```

---

## classList
JavaScriptillä voit lisätä, poistaa tai vaihtaa CSS-luokkia.

<button id="nappi">Klikkaa minua</button>

```html
<style>
  .punainen { background-color: red; color: white; }
  .vihrea  { background-color: green; color: white; }
</style>
```

**Lisää luokka**
```js
const nappi = document.getElementById('nappi');
nappi.classList.add('punainen'); // nappi muuttuu punaiseksi

```
**Poista luokka**
```js
nappi.classList.remove('punainen'); // nappi palautuu alkuperäiseksi
```
**Vaihda luokka**

```js
nappi.classList.replace('punainen', 'vihrea'); // punainen → vihreä
```
**Toggle (kytkee luokan päälle/pois)**

```js
nappi.addEventListener('click', () => {
  nappi.classList.toggle('punainen'); // klikkaus vaihtaa väriä
});
```

**Useita luokkia**
```js
nappi.classList.add('punainen', 'iso-nappi');
```

---

## CSS-animaatio

**Esimerkki 1**
```css
#result-container {
    background-color: #f8f4f4;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.7);
    width: 200px;
    margin: 0 auto;
    padding: 0px;
    /* Animaatiota varten */
    transition: transform 0.2s ease;
}

/* Lisäluokka pomppaukselle */
.pop {
    transform: scale(1.1); /* kasvaa 10% hetkellisesti */
}
```

```js
const result = document.getElementById('result-container');

function pompahtaa() {
    result.classList.add('pop');
    
    // Poistetaan luokka 200 ms kuluttua, niin div palaa normaaliksi
    setTimeout(() => {
        result.classList.remove('pop');
    }, 200);
}
```

**Selitys**

- `transform: scale(1.1);` → div kasvaa 10% hetkellisesti

- `transition: transform 0.2s ease;` → animointi on pehmeä

 - JS lisää ja poistaa .pop-luokan → div “pomppaa” lyhyesti
   



**Esimerkki 2**

```css
 /* Heilahdus */
@keyframes heilahtaa {
    0%   { transform: translateX(0); }
    25%  { transform: translateX(10px); }  /* oikealle */
    50%  { transform: translateX(-10px); } /* vasemmalle */
    75%  { transform: translateX(6px); }   /* oikealle pienempi liike */
    100% { transform: translateX(0); }     /* takaisin keskelle */
}

.swing {
    animation: heilahtaa 0.5s ease;
}
```

```js
const result = document.getElementById('result-container');

function heilahda() {
    result.classList.add('swing');
    
    setTimeout(() => {
        result.classList.remove('swing');
    }, 500); // sama kuin animaation kesto
}
```

**Selitys**

- `@keyframes` heilahtaa määrittelee heilahdusliikkeen X-akselilla

- `.swing` käynnistää animaation

- `setTimeout` poistaa luokan, jotta animaatio voidaan suorittaa uudelleen
