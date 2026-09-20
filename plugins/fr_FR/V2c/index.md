# Plugin V2C Trydan

Ce plugin connecte Jeedom à votre borne de recharge de véhicule électrique **V2C Trydan**. Il communique directement avec la borne sur votre réseau local (aucun compte cloud, aucune clé API) : aucune donnée ne transite par Internet.

Il permet de :

- suivre la puissance, l'intensité et l'énergie de charge en temps réel ;
- suivre la production photovoltaïque et la puissance de la maison si votre installation le permet ;
- mettre en pause, reprendre, verrouiller ou déverrouiller la charge ;
- activer le mode dynamique (charge pilotée par le surplus solaire) et choisir son mode de fonctionnement ;
- régler les intensités minimale et maximale de charge ;
- consulter le mode de charge (monophasé / triphasé / mixte) et, à partir du firmware 2.5.0, les mesures par phase.

## Prérequis

- Une borne V2C Trydan connectée à votre réseau local (Wi-Fi ou Ethernet).
- Connaître l'**adresse IP locale** de la borne (visible dans l'application V2C, ou dans la liste des appareils de votre routeur/box).

## Installation du plugin

1. Dans Jeedom, allez dans **Plugins > Gestion des plugins**.
2. Recherchez **V2C Trydan** et cliquez sur **Installer**.
3. Une fois l'installation terminée, activez le plugin.

Un cron interne au plugin s'occupe automatiquement d'interroger vos chargeurs à intervalle régulier ; vous n'avez rien à configurer côté planification.

## Ajouter un chargeur

1. Allez dans **Plugins > Énergie > V2C Trydan**.
2. Cliquez sur **Ajouter un chargeur**.
3. Renseignez :
   - **Nom du chargeur** : le nom qui apparaîtra dans Jeedom (ex : « Chargeur garage »).
   - **Objet parent** / **Catégorie** : classement optionnel dans votre arborescence Jeedom.
   - **Adresse IP** : l'adresse IP locale de votre Trydan (ex : `192.168.1.50`).
   - **Port** : laissez `80` sauf configuration réseau particulière.
   - **Timeout** : délai maximum d'attente d'une réponse, en secondes (`5` par défaut convient dans la plupart des cas).
   - **Intervalle de rafraîchissement** : à laisser vide pour utiliser la valeur par défaut du plugin (réglable dans **Configuration du plugin**), ou à renseigner en secondes pour ce chargeur uniquement.
4. Cliquez sur **Tester la connexion** : le plugin interroge la borne et affiche sa version de firmware, l'état de charge et la puissance actuelle. Un message « Connexion réussie » confirme que tout est correctement configuré.
5. Cliquez sur **Sauvegarder**.

Si le test échoue, vérifiez l'adresse IP, que la borne est bien allumée et connectée au réseau, et qu'aucun pare-feu ne bloque la communication entre Jeedom et la borne.

## Configuration générale du plugin

Dans **Configuration du plugin**, vous pouvez régler la **fréquence de rafraîchissement par défaut** (en secondes), utilisée pour tous les chargeurs qui n'ont pas d'intervalle spécifique défini sur leur propre fiche.

## Utiliser le widget du tableau de bord

Chaque chargeur ajoute un widget sur votre tableau de bord Jeedom, avec :

- **Visuel de la borne** : change de couleur selon l'état (câble débranché / branché en attente / en charge).
- **Bandeau d'en-tête** : tension d'installation, durée de charge en cours, indicateur de connexion (« Connecté » / « Injoignable »), et mode de charge (monophasé/triphasé/mixte).
- **Interrupteur « Bloquer »** : verrouille ou déverrouille la borne à distance.
- **Bouton pause/lecture** : met en pause ou reprend la charge en cours.
- **Section « Charge dynamique »** : active/désactive le pilotage solaire, et choisit le mode de puissance dynamique (Boost, Minuterie désactivée, Charge exclusive, Puissance minimale, Réseau + Solaire, Arrêt).
- **Section « Mode de charge »** : sélectionne le câblage utilisé par la borne (Monophasé / Triphasé / Mixte).
- **Jauge de puissance** : affiche la puissance de charge instantanée.
- **Curseurs « Intensité minimale »** et **« Intensité maximale »** : définissent la plage d'intensité (en ampères) utilisée par la borne, notamment en mode dynamique.
- **Bloc « Mesures par phase »** (visible uniquement en triphasé, à partir du firmware 2.5.0) : intensité et tension mesurées sur chacune des phases L1, L2, L3.
- **Version de firmware** installée sur la borne, affichée en bas du widget.

Toutes les actions du widget (pause, verrouillage, mode dynamique, mode de charge, intensités) agissent directement sur la borne physique, quasi instantanément.

## Commandes disponibles pour vos scénarios

Toutes les informations et actions du widget existent aussi comme des commandes Jeedom classiques, utilisables dans vos scénarios : état de charge, puissance, énergie de session, intensité, tensions par phase, mode de charge, ainsi que les actions pause/reprise, verrouillage, mode dynamique, réglage d'intensité, etc.

## Dépannage

| Problème | Piste de résolution |
|---|---|
| Widget affiche « Injoignable » | Vérifiez que la borne est allumée, connectée au réseau, et que l'adresse IP configurée est toujours correcte (une IP peut changer si elle n'est pas fixe/réservée sur votre routeur). |
| « Tester la connexion » échoue | Vérifiez l'adresse IP et le port ; augmentez le timeout si votre réseau est lent. |
| Le bloc « Mesures par phase » n'apparaît jamais | Il ne s'affiche qu'en mode triphasé et nécessite un firmware Trydan ≥ 2.5.0. Vérifiez la version de firmware affichée en bas du widget. |
| Les curseurs d'intensité ne bougent pas comme attendu | Ils reflètent la valeur mémorisée par la borne elle-même ; un rafraîchissement (cron) peut prendre quelques secondes après un changement. |

## Support

Pour toute question ou suggestion, consultez le changelog et la documentation en ligne du plugin, ou contactez l'auteur via le forum Jeedom.
