### Event Sourcing

 - Source de données immutable
 - Stockage de l'historique des événements (du domaine)


### Event Sourcing

| idPotAuFeu | nbCarottes | nbChoux |    etat    |
|:----------:|:----------:|:-------:|:----------:|
|     42     |      0     |    0    |  en prépa  |
|     43     |      2     |    3    | en cuisson |
|     44     |      5     |    3    |    prêt    |


### Event Sourcing

Commande: "_Ajouter une carotte au pot au feu **42**_"

| idPotAuFeu | nbCarottes | nbChoux |    etat    |
|:----------:|:----------:|:-------:|:----------:|
|     42     |      0     |    0    |  en prépa  |
|     43     |      2     |    3    | en cuisson |
|     44     |      5     |    3    |    prêt    |


### Event Sourcing

Commande: "_Ajouter une carotte au pot au feu **42**_"

| idPotAuFeu | nbCarottes | nbChoux |    etat    |
|:----------:|:----------:|:-------:|:----------:|
|     42     |    **1**   |    0    |  en prépa  |
|     43     |      2     |    3    | en cuisson |
|     44     |      5     |    3    |    prêt    |


### Event Sourcing

Commande: "_Ajouter 2 choux au pot au feu **42**_"

| idPotAuFeu | nbCarottes | nbChoux |    etat    |
|:----------:|:----------:|:-------:|:----------:|
|     42     |      1     |  **2**  |  en prépa  |
|     43     |      2     |    3    | en cuisson |
|     44     |      5     |    3    |    prêt    |


### Event Sourcing

Commande: "_Ajouter une carotte au pot au feu **42**_"

| idPotAuFeu | nbCarottes | nbChoux |    etat    |
|:----------:|:----------:|:-------:|:----------:|
|     42     |    **2**   |    2    |  en prépa  |
|     43     |      2     |    3    | en cuisson |
|     44     |      5     |    3    |    prêt    |


### Event Sourcing

Commande: "_Retirer une carotte du pot au feu **42**_"

| idPotAuFeu | nbCarottes | nbChoux |    etat    |
|:----------:|:----------:|:-------:|:----------:|
|     42     |    **1**   |    2    |  en prépa  |
|     43     |      2     |    3    | en cuisson |
|     44     |      5     |    3    |    prêt    |


### Event Sourcing

| Aggregate | Id |        Event       |  Data  | Version |
|:---------:|:--:|:------------------:|:------:|:-------:|
|  PotAuFeu | 42 | préparation_lancée |  null  |    1    |


### Event Sourcing

Commande: "_Ajouter une carotte au pot au feu **42**_"

| Aggregate | Id |        Event       |  Data  | Version |
|:---------:|:--:|:------------------:|:------:|:-------:|
|  PotAuFeu | 42 | préparation_lancée |  null  |    1    |
|  PotAuFeu | 42 |   carotte_ajoutée  | {nb:1} |    2    |


### Event Sourcing

Commande: "_Ajouter 2 choux au pot au feu **42**_"

| Aggregate | Id |        Event       |  Data  | Version |
|:---------:|:--:|:------------------:|:------:|:-------:|
|  PotAuFeu | 42 | préparation_lancée |  null  |    1    |
|  PotAuFeu | 42 |   carotte_ajoutée  | {nb:1} |    2    |
|  PotAuFeu | 42 |     chou_ajouté    | {nb:2} |    3    |


### Event Sourcing

Commande: "_Ajouter une carotte au pot au feu **42**_"

| Aggregate | Id |        Event       |  Data  | Version |
|:---------:|:--:|:------------------:|:------:|:-------:|
|  PotAuFeu | 42 | préparation_lancée |  null  |    1    |
|  PotAuFeu | 42 |   carotte_ajoutée  | {nb:1} |    2    |
|  PotAuFeu | 42 |     chou_ajouté    | {nb:2} |    3    |
|  PotAuFeu | 42 |   carotte_ajoutée  | {nb:1} |    4    |


### Event Sourcing

Commande: "_Retirer une carotte du pot au feu **42**_"

| Aggregate | Id |        Event       |  Data  | Version |
|:---------:|:--:|:------------------:|:------:|:-------:|
|  PotAuFeu | 42 | préparation_lancée |  null  |    1    |
|  PotAuFeu | 42 |   carotte_ajoutée  | {nb:1} |    2    |
|  PotAuFeu | 42 |     chou_ajouté    | {nb:2} |    3    |
|  PotAuFeu | 42 |   carotte_ajoutée  | {nb:1} |    4    |
|  PotAuFeu | 42 |   carotte_retirée  | {nb:1} |    5    |


### Event Sourcing

 <img src="slides/img/es/decision.png" alt="decision"/>

```
f(history, command) => events
```


### Event Sourcing

 <img src="slides/img/es/decision-focus.png" alt="focus decision" style="height:300px;"/>

```
f(history) => state
f(state, command) => events
```


### Event Sourcing et DDD

 <img src="slides/img/es/compiled.png" alt="event sourcing compiled" style="height:400px;"/>

 <span style="font-size:12pt;">_source: http://thinkbeforecoding.com/post/2014/01/04/Event-Sourcing.-Draw-it_</span>


### CQRS/ES

 <img src="slides/img/es/cqrs-es.png" alt="CQRS and Event Sourcing together" style="height:450px;"/>

```
f(state, event) => state
```


### Event Sourcing

 - Protection/Decision

```
f(history) => state
f(state, command) => events
```

 - Interpretation/Projection

```
f(events) => state
```
Ou pour traiter chaque événement
```
f(state, event) => state
```
<span style="font-size:12pt;">_source: http://verraes.net/2014/05/functional-foundation-for-cqrs-event-sourcing/_</span>


### CQRS/ES

<img src="slides/img/backend.png" alt="backend architecture" style="height:500px;"/>