# querySelector ja querySelectorAll

Näillä voidaan hakea HTML-elementtejä CSS-valitsimilla.

### querySelector 
- hakee **ensimmäisen** osuman
  
**ID**
```js
const elementti = document.querySelector('#my-id');
```

**Luokka**
```js
const kortti = document.querySelector('.card');
```

**Elementtityyppi**
```js
const ekaPainike = document.querySelector('button');
```

**Sisäkkäinen haku**
```js
const otsikko = document.querySelector('.card h2');
```

**Attribuutiovalitsin**
```js
const tarkeä = document.querySelector('input[type="checkbox"]');
```

**Pseudo-class** :hover / :focus (vain valinta, ei “tilan” asettamista)
```js
const valittu = document.querySelector('li:first-child');
```

### querySelectorAll 
- hakee **kaikki** osumat

- Palauttaa **NodeList**-kokoelman.

**Kaikki tietyt elementit**
```js
const painikkeet = document.querySelectorAll('button');
painikkeet.forEach(btn => {
  btn.style.background = 'yellow';
});
```

**Kaikki tietyn luokan elementit**
```js
const kortit = document.querySelectorAll('.card');
```

### NodeList

NodeList on eräänlainen lista (kokoelma) DOM-elementeistä, joka saadaan esimerkiksi hakemalla elementtejä:

```js
const napit = document.querySelectorAll('button');
console.log(napit); // NodeList(3) [button, button, button]
```

**- Ominaisuuksia**

- Ei aivan tavallinen array

- Voit käyttää forEach:

```js
napit.forEach(btn => console.log(btn.id));
```


- Mutta et voi suoraan käyttää push, pop jne.

**- Elävä vs. staattinen NodeList**

- Staattinen (`querySelectorAll`) → sisältö ei muutu, vaikka DOM muuttuu

- Elävä (`getElementsByClassName`, `getElementsByTagName`) → päivittyy automaattisesti, jos elementtejä lisätään tai poistetaan

**- Indeksit**

- NodeList toimii kuin taulukko:

```js
console.log(napit[0]); // ensimmäinen button
```

**- Muuntaminen tavalliseksi taulukoksi**

- Jos haluat käyttää kaikkia array-funktioita (map, filter, reduce):

```js
const arr = Array.from(napit);
const ids = arr.map(btn => btn.id);
```


- Tai modernilla spread-operaattorilla:

```js
const arr = [...napit];
```
