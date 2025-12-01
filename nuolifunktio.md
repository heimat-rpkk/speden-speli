# Nuolifunktio

Nuolifunktio (arrow function) on lyhyempi tapa kirjoittaa funktio JavaScriptissä.


### Perusmuoto

**- Perinteinen funktio:**

```js
function tervehdi(nimi) {
  return "Hei " + nimi;
}
```


**- Sama nuolifunktiona:**

```js
const tervehdi = (nimi) => {
  return "Hei " + nimi;
};
```

**- Vielä lyhyempi versio**

- Jos on vain yksi parametri → sulkeet voi jättää pois.
- Jos on vain yksi lause → return tulee automaattisesti.

```js 
const tervehdi = nimi => "Hei " + nimi;
```

**- Ilman parametreja**
```js 
const terve = () => "Moi!";
```

**- Jos palautetaan objekti** 
→ pitää laittaa sulkeet (objektin ympärille)
```js 
const luoObjekti = () => ({ pisteet: 10 });
```

**- Käyttö esimerkkinä taulukko-funktioissa**
```js
const numerot = [1, 2, 3];
const tuplana = numerot.map(n => n * 2);
console.log(tuplana); // [2, 4, 6]
```

**- Tärkeä ero normaalifunktioon**

Nuolifunktiolla ei ole omaa:

```
this

arguments

super
```

→ Siksi se sopii erityisesti **lyhyisiin callbackeihin ja eventteihin**, mutta ei metodeihin olioissa, joissa käytetään `this`-viittausta.

