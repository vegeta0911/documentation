<a href="../">Aide</a> → <a href="./download">Téléchargement d'un widget</a> → ***Application d'un widget***

# Application d'un widget

> Dans cet exemple, nous allons appliquer le widget a une commande d'un virtuel.<br>
> En fonction du widget, il n'est pas obligatoire de créer un virtuel. Il est tout a fait possible d'appliquer un widget directement sur une commande d'un plugin tiers si celui-ci l'autorise.

> Exemple pour appliquer le widget [cmd.action.slider.Widget_Switch1]({{site.url}}/documentation/{{site.widget}}/fr_FR/action/slider/cmd.action.slider.Widget_Switch1).

## Création d'un virtuel
- Créer un nouvel équipement 'virtuel' *(Widget_Switch1)*
  - Activer et rendre visible puis sauvegarder.
- Ajouter une 'Action virtuel' *(1)*.
- Nommer votre commande *(2)*.
- Choisir le sous-type *(3)* pour l'exemple, le widget étant de type slider, nous allons selectionner le sous-type 'Curseur'
- Choisir le nom de la commande info *(4)*. Celle-ci sera automatiquement créer après la sauvegarde de l'équipement.
- Sauvegarder l'équipement.

<img src="../{{site.img}}/virtuel_1.png" alt="Virtuel_1" />

> Une nouvelle commande info a été créer automatiquement, vous pouvez masquer celle-ci, elle ne sera pas utile dans notre exemple.

- Lier votre commande 'Action' *(5)* en selectionnant la commande 'Info' qui a précédemant été créée puis sauvegarder.

<img src="../{{site.img}}/virtuel_2.png" alt="Virtuel_2" />

## Application du widget sur une commande

- Ouvrer la configuration avancée de la commande action.

<img src="../{{site.img}}/application_1.png" alt="application_1" />

- Selectionner l'onglet 'Affichage'. *(6)*
- Selectionner le widget que vous voulez appliquer a la commande. *(7)*

<img src="../{{site.img}}/application_2.png" alt="application_2" />

> Si ils sont disponible dans le widget, la liste des paramètres optionnels seront affichés *(8)* après selection du widget.

## Paramètres optionnels

Sur certains widget, il est possible d'ajouter des paramètres optionnels.<br>
Pour notre exemple [cmd.action.slider.Widget_Switch1]({{site.url}}/documentation/{{site.widget}}/fr_FR/action/slider/cmd.action.slider.Widget_Switch1), il est possible de modifier la longueur (width) du widget.

- Ajouter un paramètre *(9)*.
- Nommer le paramètre *(10)* en fonction de ceux disponible dans le widget.
- Renseigner la valeur souhaitée *(11)*.

> Oublier pas de sauvegarder après toutes modifications.<br>
> Et actualiser le résultat (dashboard) si vous travaillez avec plusieurs onglets sur votre navigateur.

<img src="../{{site.img}}/parametre_1.png" alt="parametre_1" />

# Troubleshotting

## Statistiques

### Je n'est pas de statistique affichée sur le widget.
Vérifiez que l'option *Afficher les statistiques* est bien active dans la configuration de la commande.

<img src="../{{site.img}}/stat_2.png" alt="stat_2" />

### l'option *Afficher les statistiques* n'existe pas dans la configuration de la commande.

Il faut vérifier que l’option "Afficher les statistiques sur les widgets" est active.<br>
**Réglages→Système→Configuration** onglet **Equipements**.

<img src="../{{site.img}}/stat_1.png" alt="stat_1" />

## Couleurs

### Les couleurs ne sont pas appliquées sur les widgets.
Il faut vérifier que l’option "Icônes widgets colorées" est active.<br>
**Réglages→Système→Configuration** onglet **Interface**.

<img src="../{{site.img}}/interface_1.png" alt="interface_1" />

<hr />

<a href="../">Aide</a> → <a href="./download">Téléchargement d'un widget</a> → ***Application d'un widget***