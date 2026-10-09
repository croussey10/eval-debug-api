# Diagnostic

Une section par test en échec : renseignez ses quatre champs.

## testAddingALineToAnUnknownOrderIsNotFound

**Symptôme** :

**Cause** :

**Règle du module en jeu** :

**Correctif** :

## testAddingALineToAPaidOrderIsAConflict

**Symptôme** : Un utilisateur peut ajouter une ligne dans une commande déjà payé

**Cause** : Oublie d'une condition dans la méthode addLine de l'OrderService 

**Règle du module en jeu** : Validation de profondeur / Service

**Correctif** : Vérifié si la le status de la commande est payé et si oui renvoyé une erreur de conflit
```php
if ($order->getStatus() == OrderStatus::Paid) {
            throw new OrderAlreadyPaidException();
        }
```

## testAddingALineToMyOrder

**Symptôme** :

**Cause** :

**Règle du module en jeu** :

**Correctif** :

## testAddingALineWithAZeroQuantityIsUnprocessable

**Symptôme** : Lorsqu'on ajoute une ligne de commande avec un plat mais 0 en quantité de plat, le plat est ajouter dans notre panier avec 0 en quantité alors que cela ne devrait pas être possible

**Cause** : DTO d'input mal configuré

**Règle du module en jeu** : Validation de surface

**Correctif** : Modification de la DTO OrderAddLineInput pour le champ quantity : 
- Assert\Positive
- 'minimum' => 1

## testListingKitchenTicketsReturnsMine

**Symptôme** :

**Cause** :

**Règle du module en jeu** :

**Correctif** :

## testListingKitchenTicketsWithoutTokenIsUnauthorized

**Symptôme** : Un user non connecté peux récupéré la liste des tickets d'une cuisine

**Cause** : ApiResource de l'Entity KitchenTicket 

**Règle du module en jeu** : Sécurité

**Correctif** : Ajout de "security: 'is_granted("ROLE_USER")'" dans les operations ApiResource

## testOpeningAnOrderIgnoresAnAbandonedOne

**Symptôme** :

**Cause** :

**Règle du module en jeu** :

**Correctif** :

## testPayingMyOrderMarksItPaid

**Symptôme** :

**Cause** :

**Règle du module en jeu** :

**Correctif** :

## testRefreshingTwiceWithTheSameTokenIsUnauthorized

**Symptôme** : Une fois le refresh token utilisé, il reste le même alors qu'il devrait changer

**Cause** : Config Packages gesdinet_jwt_refresh_token

**Règle du module en jeu** : Token JWT

**Correctif** : passer la variable single_use: false à true

## testRemovingALineFromSomeoneElsesOrderIsForbidden

**Symptôme** : Un user peut supprimer une ligne d'une commande d'une autre personne

**Cause** : Méthode Delete de l'ApiResource de l'entity Order

**Règle du module en jeu** : Sécurité

**Correctif** : Modifier dans l'operation security le "or" par un "and" car le or dit que si une personne est connecté ou qu'elle est sur son compte elle peut delete une commande alors qu'il faut que les 2 conditions soient remplie : : 
- security: "is_granted('ROLE_USER') and object.getCreatedBy() == user",
