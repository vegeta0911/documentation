# Plugin Mobile

Plugin permettant d’utiliser l’application Mobile Jeedom.

L’application mobile Jeedom nécessite l’installation de ce plugin afin que la Box puisse dialoguer avec l’application Mobile.

# Configuration du plugin Mobile pour Application V2

Après installation du plugin, il vous suffit de l’activer :

![mobile1](./images/mobile1.png)

# Première connexion à l'application V2

Pour connecter votre téléphone, il y a 2 méthodes possible.

<img src="./images/v2firstConnect.png" alt="v2firstConnect" width="40%" />

### **Méthode 1 :** CONNEXION VIA LE COMPTE MARKET

<img src="./images/v2connectMarket.png" alt="v2connectMarket" width="40%" />

Cette méthode permer de synchroniser, en une seule fois, toutes vos box sur l'application.<br>
Elle nécessite donc de vous identifier dans un premier temps a votre compte market.<br>
Il vous faut simplement entrer votre identifiant Market ainsi que votre mot de passe.<br>
Après avoir cliqué sur "Commencer" vous aurez accès a toutes les box de votre compte Market, et ainsi vous connecter par utilisateur / mot de passe ou par Qrcode.<br>

> **Qrcode **
>
> Pour la connection via Qrcode, reportez-vous a l'étape méthode 2 / choix 2 ci-dessous.


### **Méthode 2 :** CONNEXION VIA Box ID

2 choix possible sur cet écran :

<img src="./images/v22methods.png" alt="v22methods" width="40%" />

#### **Choix 1 :** VIA IDENTIFIANTS

Vous entrez l'url de votre Jeedom (interne ou externe), ainsi que les identifiants d'accès à celle-ci et vous confirmez avec le bouton "Connexion".

#### **Choix 2 :** VIA QRCODE

> **Info**
>
> Via le Qrcode, il vous faudra peut-être donner les droits à Jeedom App d'utiliser la caméra de votre téléphone lorsque celui-ci vous le demandera.

Cliquez sur QR Code, un nouvel écran apparait, scanner le Qrcode depuis le plugin Mobile de la Box que vous souhaitez ajouter, via l'onglet(*) QR Code du plugin.

<img src="./images/v2QRCodeConnect.png" alt="v2QRCodeConnect" width="40%" />

> (*) Onglet QR Code du plugin Mobile
>
> <img src="./images/v2ModalQrCode.png" alt="v2ModalQrCode" width="100%" />

Une fois cette première étape passée, vous êtes enregistré dans l'application.<br>
Si vous possédez le plugin Mobile, vous aurez accès via le menu aux Notifications, aux QR Codes, la customisation du Menu ....

Dans le menu, vous aurez un onglet Boxs, qui regroupe toutes les Box présentes sur ce compte Market

<img src="./images/v2MenuBoxs.png" alt="v2MenuBoxs" width="40%" />
<img src="./images/v2floutedBoxs.png" alt="v2floutedBoxs" width="40%" />

Il vous suffit de cliquer sur la Box où le plugin Mobile est installé, puis de vous identifier pour accéder à la Box.

La Box passera en haut de la liste, ayant validée son authentification.<br>
Vous pouvez faire ainsi pour plusieurs Boxs.

Vous pouvez aussi cliquer sur le bouton + en bas à droite pour accéder à différentes options;

<img src="./images/v2greenBtnAdd.png" alt="v2greenBtnAdd" width="40%" />

1) QR Code pour ajouter une Box à la liste via le plugin Mobile.<br>
2) Manuel pour ajouter manuellement une Box.<br>
3) Détection Atlas et Luna (si vous êtes en Wifi, détectera les Boxs sur le réseau).<br>
4) Synchronisation Market pour actualiser les informations du compte Market configuré.

Pour accéder aux fonctionnalités comme les Notifications, la Personnalisation du Menu ou la Géolocalisation, il faut au préalable avoir sélectionné au moins une Box 'actuelle'

<img src="./images/v2ActualBoxFlouted.png" alt="v2ActualBoxFlouted" width="40%" />

# Fonctionnement de la Géolocalisation

Ajouter une zone de Géolocalisation en cliquant sur l'icône +

<img src="./images/v2AddZone.png" alt="v2AddZone" width="40%" />

Taper l'adresse recherchée, puis valider avec la touche Entrée, le curseur va alors se positionner sur l'adresse recherchée.
Vous pouvez ensuite ajouter un nom et sauvegarder la zone.

Cela créera une nouvelle commande sur votre équipement mobile, de type binaire, qui correspondra aux entrées et sorties de la zone si la géolocalisation est activée sur votre téléphone mobile.

Vous pouvez également changer le radius de la zone pour étendre la détection de la zone.

<img src="./images/v2ModifyBigRadius.png" alt="v2ModifyBigRadius" width="40%" />

# Paramètres spécifiques du plugin

Si vous voulez interdire la configuration de la géolocalisation ou du menu custom, par exemple, pour une utilisation sur un profil enfant/ado.<br>
Dans l'équipement de cet utilisateur, dans l'onglet mobile, activer l'option voulu.

<img src="./images/v2ParamSpecPlugin.png" alt="v2ParamSpecPlugin" width="80%" />

# Les commandes du plugin

Lorsque la connection de votre smartphone au plugin sera effectué, le plugin créera automatiquement ces commandes par défaut.

<img src="./images/v2TableCmdDefaut.png" alt="v2TableCmdDefaut" width="80%" />

### 1) Notification

Permet d'envoyer une notification du plugin vers le smartphone.

### 2) Notification Critiques

Permet d'envoyer une notification critique du plugin vers le smartphone, elle sera différencier sur l'app avec une bordure rouge.

### 3) Récupérer les informations du téléphone

Cette partie permet de recupérer des "extras" du smartphone, actuellement elle permet de récupérer :
- Batterie.
- Etat de charge.
- Géolocalisation.

> **Info**
>
> Lorsque vous exécuterez cette action, de nouvelles commandes seront créées sur le plugins.<br>
> Elles pourront ensuite être utilisées dans des scénarios par exemple.

### 4) Supprimer les notifications

L'app ne stock pas les notifications, elle fait simplement des requêtes vers le plugin pour les récupérer.<br>
Vous pouvez donc forcer la suppression avec cette commande.

> **Tips**
>
> Le plugin utilise déja un nettoyage automatique des notifications.<br>
celui-ci est exécuté une fois par jour.<br>
> La durée de rétention est paramètrable sur l'application dans le menu "Préférences".<br>
> Les choix possibles sont 7, 15 ou 30 jours (défaut 30 jours).
>
> <img src="./images/v2RetentionTime.png" alt="v2RetentionTime" width="40%" />

# BUG

Pour nous remonter un bug, vous avez plusieurs choix :<br>
1) En utilisant le bouton <img src="./images/v2Assistance.png" alt="v2Assistance" width="80px" /> disponible dans la configuration de plugin mobile, celui-ci ouvrira un post dédié sur le community avec toutes les informations nécessaires.

2) En utilisant notre <a href="https://discord.gg/WF5y2PXu" target="_blank">Discord</a>.

# FAQ

> **Le menu "Scénarios" n'est pas visible** ou **Le menu "Plugins" n'est pas visible** ou **Le menu "Message" n'est pas visible**
>
> Pour avoir accès a ces menus il faut que l'utilisateur connécté a la box est un profil Administrateur.<br>
> Reportez vous au <a href="https://doc.jeedom.com/fr_FR/core/4.5/user" target="_blank">manuel de configuration</a> de Jeedom.

> **J'ai des soucis avec les notifications**
>
> Cette partie est actuellement en cours d'amélioration et d'optimisation sur l'application beta.

> **J'ai des soucis d'affichage de ma webview**
>
> Sur votre Jeedom, dans les Préférences, vérifiez que la page d'accueil du mobile soit bien ACCUEIL.
