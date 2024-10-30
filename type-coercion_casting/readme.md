![Texte alternatif](https://github.com/yamsdmc/formation-javascript/blob/main/type-coercion_casting/image.png?raw=true)

Vidéo Youtube: [JavaScript : Type Coercion et Casting, L’Art de Manipuler Les Types Sans Erreur !
](https://www.youtube.com/watch?v=cts57eMLDMc&t=655s)

# Coercion de type et Type casting

#### Définition :

- **Type coercion -> Coercition de type →  conversion Implicite**
    - C'est quand JavaScript change automatiquement le type d'une valeur en un autre type
- **Type Casting → conversion explicite**
    - la conversion explicite en JavaScript consiste à utiliser des fonctions native (comme `Number()`, `String()`, `Boolean()`) pour transformer intentionnellement une valeur d'un type à un autre.

**Analogie :**

- C'est comme si vous essayez de mélanger de l'huile et de l'eau dans une recette - JavaScript va essayer automatiquement de les rendre compatibles pour que ça marche ensemble

**A quoi ça sert:**

- Permet de mieux manipuler et contrôler comment vos données se transforment.

# Mécanismes de conversion

### **Conversions IMPLICITES (**Coercion de type**) :**

```jsx
console.log(123 + '') -> '123' (string)
console.log(+"123") -> 123 (number)
```

**Les opérateurs de conversion rapide :**

- `+"42"`
    - *42 (convertit en number)*
- `"" + 42`
  - *"42" (convertit en string)*
- `!!42`
    - *true (convertit en boolean)*

- `"5" + 2 = "52”`
    - Le + avec une string déclenche la concaténation
- `"5" - 2 = 3`
    - Pourquoi ? Le - n’effectue pas de concaténation, le 5 est donc transformé en number.
- `true + 1 = 2`
    - Pourquoi ? true est converti en 1
    - false est converti en 0

**Les opérateurs qui déclenchent des conversions implicites** :

- Comparaisons ordinale (>, <, <=, >=)
- Opérateurs binaires (|, &, ^, ~)
- Opérateurs arithmétiques (-, +, *, /, %)
- comparateur d’égalité (`==`, `!=`, `===`, `!==`)

### **Conversions EXPLICITES (**Type casting**) :**

- "5" + String(2) = "52”
- Number(“5”) + 2 = 7
- String(123)
- Number("123")
- Boolean(123)

**Les conversions EXPLICITES sont uniquement quand on utilise délibérément :**

- Number()
    - **parseInt()** et **parseFloat()**
- BigInt(123)
- String()
- toString()
    - A utiliser avec une instance existante
        - null.toString();       // Erreur : Cannot read properties of null
        - undefined.toString();  // Erreur : Cannot read properties of undefined
- Boolean()
- JSON.stringify()

`il existe encore d’autres méthodes`

**Objets** : Lorsqu'on essaie de convertir un objet, JavaScript appelle ses méthodes `toString()` ou `valueOf()` pour obtenir une valeur primitive.

```jsx
const monObjet = {
	nom: "ChatGPT",
	toString() {
		return `Objet: ${this.nom}`;
	},
	valueOf() {
		return 42;
	}
};
console.log(String(monObjet)) -> 'Objet: ChatGPT' (string);
console.log(Number(monObjet)) -> 42 (number);
console.log(monObjet + " est génial !") -> '42 est génial !' (string);
```

**Sans méthodes toString() ou valueOf() personnalisées :**

- Un objet devient "[object Object]" en chaîne.
- Un objet devient NaN en nombre.
    - NaN, c’est une valeur pour indiquer qu'un résultat mathématique est indéfini ou invalide, par exemple lors de divisions par zéro ou de calculs impossibles.

**Opérateurs de comparaison**

- `"5" == 5 // true`
    - == convertit les types et vérifie uniquement les valeurs
- `"5" === 5 // false`
    - === vérifie aussi les valeurs et les types et ne fait pas de conversion implicite (coertion).

**Toujours préférer === !!!**

## Boolean et conditions :

### **Quand JavaScript évalue une condition (if), il convertit automatiquement la valeur en Boolean.**

- String vide "" → false
- String non-vide "abc" → true
- 0 → false
- Nombres non-nuls → true
- null → false
- undefined → false
- objets → true

- ```
  const person = {
    name: ‘Yamin’,
    age: 27
  }
  ```

  if(person.name) {}


Donc [person.name](http://person.name/) ('Yamin') est converti implicitement en true car c'est une string non-vide.

# Règles spéciales

### **Les règles de priorité :**

- 1 + 2 + "3"
    - *"33" (les opérations se font de gauche à droite)*
- "1" + 2 + 3
    - *"123" (une fois en string, tout devient string)*
- 1 + ”2” + 3
    - “123”

### **Les cas piégeux fréquents :**

- [] + []
    - *""*
- [] + {}
    - *"[object Object]"*
- {} + []
    - *0*
- null + 1
    - *1*
- undefined + 1
    - *NaN*

**Cas importantes** :

- *null n'est égal qu'à null ou undefined*
    - null == 0
        - *false*
    - null == null
        - *true*
    - null == undefined
        - *true*
- *NaN n'est égal à rien, même pas à lui-même*
    - NaN == NaN
        - *false*

### **Bonne pratique :**

- Toujours utiliser === au lieu de ==
    - *Plus sûr et prévisible*
- Préférer les conversions explicites dans le code critique
    - `Number("42")` plutôt que `+"42"`
- Utiliser typeof pour debugger les valeurs
    - `typeof "42"`