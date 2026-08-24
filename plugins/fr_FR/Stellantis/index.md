# Plugin Stellantis

## Description

Le plugin **Stellantis** connecte votre compte constructeur (**Peugeot / MyPeugeot**, **Citroën / MyCitroën**, **Opel / MyOpel**, **DS / MyDS**, **Vauxhall / MyVauxhall**) pour superviser et piloter votre véhicule connecté depuis Jeedom.

Un démon Python interroge en tâche de fond l'API cloud Stellantis et met à jour dans Jeedom :

- Les informations du véhicule (niveau de batterie, autonomie électrique, niveau et autonomie carburant, kilométrage, état de charge, prise branchée ou non, climatisation, dernière connexion...).
- Des commandes d'action à distance (démarrer/arrêter la charge, démarrer/arrêter la climatisation,  heure de charge différée...), sous réserve que votre véhicule les supportes.

>**IMPORTANT**
>
>Toutes les fonctionnalités ne sont pas disponibles sur tous les véhicules : le plugin détecte automatiquement les capacités réelles de votre véhicule (électrique, thermique, hybride, climatisation à distance...) et n'affiche que les commandes pertinentes.

# Configuration

## Ajouter un compte / véhicule

Depuis **Plugins > Objects connectés > Stellantis** :

1. Cliquez sur **Ajouter un compte**.
2. Renseignez :
   - **Marque de l'application** : celle utilisée sur votre téléphone (MyPeugeot, MyCitroën, MyOpel, MyDS ou MyVauxhall).
   - **Identifiant / Email** et **Mot de passe** : les mêmes que sur l'application mobile officielle.
   - **Pays / Région**.
3. **Sauvegardez** l'équipement.
4. Cliquez sur **Démarrer l'authentification**. Stellantis envoie alors un SMS de sécurité sur le téléphone associé au compte.
5. Dans le bloc **Validation de la sécurité (Double Authentification)** :
   - Renseignez le **Code reçu par SMS**.
   - Renseignez le **Code PIN de l'application** (celui utilisé pour valider les actions dans à distance, 4 ou 6 chiffres).
   - Cliquez sur **Valider et lier mon compte**.

>**INFORMATION**
>
>Si le SMS n'arrive pas ou que le code a expiré, utilisez le bouton **Renvoyer le code SMS** plutôt que de relancer toute l'authentification.

## Configuration générale du plugin

Accessible via **Configuration** sur la page d'accueil du plugin :

- **Port Socket Daemon** : port d'échange interne entre le démon et Jeedom (à ne changer qu'en cas de conflit de port).

# Utilisation

## Widget du tableau de bord

Chaque véhicule dispose d'un widget dédié affichable sur le tableau de bord Jeedom, avec :

- La photo du véhicule et son kilométrage.
- Les informations pertinentes selon la motorisation (batterie/autonomie électrique pour un véhicule électrique, niveau/autonomie carburant pour un thermique, les deux pour un hybride), l'état de la prise, l'état et le mode de charge, l'heure de charge différée programmée, l'état de la climatisation, la batterie 12V.
- Une rangée de boutons d'actions : démarrer / arrêter la climatisation, démarrer / arrêter la charge,  et **Heure de charge différée**.
- La date de dernière connexion avec le véhicule.

Après chaque action, un message s'affiche indiquant si la commande a été transmise, refusée, ou si le véhicule était injoignable (endormi).

## Heure de charge différée

Le bouton **Heure de charge différée** (icône horloge) ouvre une fenêtre avec deux curseurs :

- **Heure** (0-23h)
- **Minute** (0-59min)

Ajustez les curseurs puis cliquez sur **Valider** pour envoyer la nouvelle heure de départ de charge différée au véhicule.

## Liste des commandes disponibles

Selon les capacités détectées pour votre véhicule, tout ou partie des commandes suivantes sont créées automatiquement (visibles dans l'onglet **Commandes / Véhicules** de l'équipement) :

**Informations**

| Commande | Description |
|---|---|
| Niveau batterie / Autonomie / Santé batterie | Véhicules électriques |
| Batterie 12V | Tous véhicules |
| Niveau carburant / Autonomie carburant / Consommation instantanée | Véhicules thermiques/hybrides |
| Véhicule branché | Véhicules électriques |
| État recharge / Mode recharge / Puissance recharge / Temps restant | Véhicules électriques |
| Départ différé | Heure de charge différée programmée |
| Kilométrage / Contact / Dernière mise à jour | Tous véhicules |
| Température extérieure | Tous véhicules |
| Préconditionnement / Cause échec préconditionnement | Véhicules avec climatisation à distance |

**Actions**

| Commande | Description |
|---|---|
| Démarrer / Arrêter la recharge | Véhicules électriques |
| Démarrer / Arrêter la climatisation | Véhicules avec climatisation à distance |
| Heure de charge différée / Minute de charge différée | Curseurs utilisés par le bouton du widget |
| Réveiller le véhicule | Force le véhicule à se reconnecter au réseau |

# FAQ / Dépannage

>**"OTP indisponible le compte a atteint la limite d'appareils sur le serveur stellantis"**
>
>Le compte Stellantis a atteint le nombre maximum d'appareils autorisés (SMS/OTP) côté serveur. Ce n'est pas un problème du plugin : il faut réinitialiser les appareils autorisés depuis l'application mobile officielle (ou le support Stellantis) avant de pouvoir relier un nouvel appareil.
>Et pour réinitialiser il faut désinstaller l'application officiel sur votre mobile, puis vous reconnecter sur l'application officiel et suivre les l'étapes de connexion.

>**"Code SMS invalide ou expiré"**
>
>Le code SMS saisi a été refusé par le serveur (faux, déjà utilisé, ou expiré au bout de quelques minutes). Utilisez **Renvoyer le code SMS** puis validez rapidement le nouveau code.

>**"Refresh token rejeté par Stellantis (invalid_grant)" dans les logs du démon**
>
>Le jeton d'accès stocké n'est plus valide côté serveur Stellantis (session expirée ou invalidée). Il faut ré-authentifier le véhicule : relancez **Démarrer l'authentification** puis, si nécessaire, revalidez le code OTP (SMS + PIN) comme lors du premier appairage.

>**"Véhicule injoignable (endormi) après 45s d'attente"**
>
>Le véhicule est en veille et ne répond pas immédiatement. Utilisez la commande **Réveiller le véhicule** puis réessayez l'action quelques instants après.
