### Introduction à ce qu'est une variable

Imaginons cette analogie :

- La boîte : C'est un espace dans la mémoire de l'ordinateur.
- L'étiquette : C'est le nom que vous donnez à votre variable.
- Le contenu : C'est la valeur stockée dans la variable.

## 2 choses à savoir sur les variables en javascript

### La portée

C'est la zone de ton code où elle peut être utilisée.


`var` a une portée de function.
-   une variable déclarée avec `var` est accessible dans toute la function où elle est déclarée.

`let` & `const` ont une portée de bloc. Elles sont accessibles uniquement à l'intérieur du bloc ou elles sont déclarées entre accolades {}

### Le hosting
#### Le hoisting est le comportement de JavaScript qui 'remonte' les déclarations de variables en haut de leur portée, avant l'exécution du code.
#### Par exemple, une variable var déclarée en bas d'une fonction sera considérée comme déclarée en haut de celle-ci, avec une valeur initiale de undefined.
- `var`: hoistées avec une valeur initiale `undefined`
- `let` & `const`: sont techniquement hoistées, mais restent dans une temporal dead zone (TDZ) jusqu'à leur déclaration. Cela signifie que si vous essayez d'accéder à ces variables avant leur déclaration, cela provoque une ReferenceError.

`var` peut être réassigné et redéclaré sans erreur

`let` peut être réassigné mais pas redéclaré dans le même bloc

`const` ne peut ni être réassigné ni redéclaré
-   PARTICULARITÉ ICI: si c'est un objet, on peut modifier ses propriétés, un tableau, on peut ajouter des éléments, mais on ne peut pas réassigner la variable elle-même

#### Temporal Dead Zone (TDZ) :

- C'est la période entre le début du bloc et la déclaration de la variable.
  Pendant cette période, accéder à une variable `const` | `let` provoque une ReferenceError.

#### var
- Portée : fonction ou globale
- Hoisting : oui, avec la valeur undefined
- Réassignable : oui
- Redéclarable : oui


#### let:
- Portée : bloc
- Hoisting : oui, mais dans la "temporal dead zone" qui provoque une ReferenceError.
- Réassignable : oui
- Redéclarable : non


#### const:
- Portée : bloc
- Hoisting : oui, mais dans la "temporal dead zone" qui provoque une ReferenceError.
- Réassignable : non
- Redéclarable : non
