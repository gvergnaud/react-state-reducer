## React

### Data flow, State et effets

<p style="font-size:.7em">Slides: https://gvergnaud.github.io/react-state-effect</p>

Note:

Plan
- Qui suis je ?
  - gabriel vergnaud
  - Heticien P2017
  - developer à Sketchfab.com (On recrute!)
  - gvergnaud on github
  - GabrielVergnaud on twitter

- Recap sur react
  - une application react est un arbre de composants

          Component
           /      \
         /          \
    Component     Component
      /                \
    /                    \
Component              Component

  - Chaque component contiens un state
    - Le state est de la data qu'il peut muter au cours du temps
    - L'UI est défini par le state (view = f(state))
  - a chaque fois qu'un component update son state, tous les components enfants sont re-render
    pour updater le DOM
  - Le data flow est **unidirectionnel**. Il se dirige toujours du haut vers le bas
  - Les props d'un component enfant est (presque) toujours le state d'un component parent.

- Cool

- Vous avez appris `useState()` qui permet de déclarer un state updatable
```js
const [count, setCount] = React.useState(0)
console.log(count) // => 0
setCount(1)
setCount(x => x + 1)
```

C'est cool, ça marche bien, mais, lorsque le component se complexifie, ça a des limitations
  - quand on a beaucoup de state
```js
const [isOpen, setIsOpen] = React.useState(false)
const [search, setSearch] = React.useState('')
const [sortBy, setSortBy] = React.useState('createdAt')
const [category, setCategory] = React.useState('all')
const [date, setDate] = React.useState('31')
// ...

const reset = () => {
  setIsOpen(false)
  setSearch('')
  setSortBy('createdAt')
  setCategory('all')
  setDate('31')
}
```
  - Dans une grande application on veut pouvoir refacto facilement, travailler à plusieur facilement et ajouter des fonctionnalité à notre projet sans complexifier le projet. cette version naive du state management est pratique pour les petit truc stateful isolé (genre un menu qui peut être ouvert ou fermé), mais est limité quand on veut construire quelque chose de complexe (comme notion!)


- State reducer pattern
  - concept abstrait:
    - (a, b) => a
    - (state, action) => state

  - la forme des actions
    - leur caractéristique principale: c'est de la data! ca permet de:
      - serialiser les actions pour les envoyés sur un reseau (websocket, http, echange entre plusieurs process, electron...)
    - les transformer à la volé grace à des **middlewares**
      - action
        -> |middleware| -> action modifiée
        -> |middleware| -> action remodifiée
        -> |reducer| -> state
    
  - Le type des actions
    - souvent des string
    - permet au reducer de savoir de quel action il s'agit
    - (Parenthese) en TypeScript on peut le représenter comme un type union, ce qui permet de s'assurer que son code est valide (pas d'action oubliée, pas de typo dans le nom)

  - structurer son state grace au `state reducer pattern` permet de:
    - avoir toutes les modifications de state **au même endroit**.
    - ne pas pouvoir seter le state de manière arbitraire
    - lire le state seulement par des accesseurs
    - découpler l'UI de la gestion du state
  - Toutes ces caractéristiques rendent le code plus facile à faire évoluer, ajouter des features, refacto, etc tout en gardant une complexité basse.

  - Un mot sur la complexité
    - analogie avec la géométrie
    - comment évaluer si un bout de code est simple ou complexe

  - vous avez peut être entendu parlé de redux ?
    - une lib de state management qui permet de **composer** plusieurs reducers les uns avec les autres pour avoir un **arbre de reducers**
            Reducer
            /      \
          /          \
        Reducer     Reducer
        /                \
      /                    \
  Reducer                 Reducer

    - ou mobx
    - ou vuex
    je les connais pas, mais ces plus ou moins la même chose.

// PETIT EXO CODE SANDBOX, utiliser React.useReducer

- les selectors
  - l'idée c'est d'avoir le plus petit state possible. 
  - Des que quelque chose dans notre state peut être dérivé d'autre chose, alors il n'a plus sa place dans le state.
  - les selectors sont des functions qui permettent de dériver une valeur du state.
  - un peu comme les computed properties en vue.

- (Parenthese) Slide sur Make impossible state impossible
  - Les datastructures utilisées dans le state doivent être en accord avec ce qu'elle représente.
    - si vous avez pas le droit d'avoir deux fois le même élément dans une liste, utiliser un Set plutot qu'un Array
    - Si deux boolean sont mutuellement exclusifs, utiliser soit un boolean, soit un union de string
    - Si vous avez de la data qui correspond à un element, stockez par ID
  - Know your data structures! 
    - List vs Set vs Map vs Queue vs Stack vs Trees vs Graphs vs Binary Trees ...
    - [Itsy Bitsy Data Structures](https://github.com/jamiebuilds/itsy-bitsy-data-structures)

- Recapitulons: Le state reducer pattern
  - un module de state contient
    - un reducer
    - des actions
    - des selectors
    - des types

  - ce pattern permet de réduire la complexité du code, et d'**optimiser le code pour le changement**
  - (Parenthese) La pire erreur qu'on peut faire en temps que developer c'est de croire que l'on sait comment le produit va évoluer. Les business requirement peuvent changer, votre produit peut pivoter... On ne peut pas deviner ce qu'il faudra changer dans le future. Il faut mettre cette incertitude au coeur de nos choix de design, et garder la plus grande flexibilité possible dans notre codebase.
  - [Dan abramov — Optimized for change](https://overreacted.io/optimized-for-change/)
---

---


##  Objectifs




---

## Petites questions


---

## Merci

#### de votre attention


---

## Ressources

- [Make impossible state impossible, par Richard Feldman](https://www.youtube.com/watch?v=IcgmSRJHu_8)
- [Itsy Bitsy Data Structures, par @jamibuilds](https://github.com/jamiebuilds/itsy-bitsy-data-structures)
- [Dan abramov — Optimized for change](https://overreacted.io/optimized-for-change/)
---

Mon ptit nom c'est **Gabriel Vergnaud**

- [@gvergnaud on Github](https://github.com/gvergnaud)
- [@gabrielvergnaud on Twitter](https://twitter.com/GabrielVergnaud)
- [LinkedIn](https://www.linkedin.com/in/gabriel-vergnaud-09446199)
