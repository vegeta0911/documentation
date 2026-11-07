# AlarmeMyfox

Plugin Jeedom pour les centrales d'alarme **Myfox / Somfy** (Evology Zen, Home Control 2...).

Somfy a annoncé l'arrêt des serveurs Myfox. Sans eux, l'application officielle, le site web et l'API
Myfox ne fonctionnent plus — et donc plus aucun pilotage à distance ni depuis Jeedom. Ce plugin
remplace entièrement ces serveurs par un petit programme (le « démon ») qui tourne directement sur
votre box Jeedom : votre centrale continue de fonctionner normalement, sans jamais repasser par
Somfy.

**Ce plugin ne nécessite aucun compte Myfox, aucun abonnement, et n'envoie rien sur internet.** Tout
reste sur votre réseau local.

## Ce que ça fait

- Armer / désarmer (total, partiel, desarmer).
- Récupérer l'état de l'alarme et les événements en temps réel (poussés directement par le démon,
  pas besoin d'interroger Jeedom en boucle).
- Commander les prises, modules et volets qui apparaissent sur le tableau de bord du démon
  (« Équipements ») : une commande Jeedom est créée automatiquement pour chacun.
- Récupérer les capteurs (température, luminosité, détecteurs de fumée/mouvement...) et surveiller les
  piles.
- Lancer des scénarios.
- Tout ça **sans dépendre d'un serveur Somfy**, et sans rien envoyer à l'extérieur de votre réseau.

Le plugin pilote un petit serveur Python (`myfox_local_server.py`) qui se fait passer, pour la
centrale, pour le vrai serveur Myfox. Il a sa propre interface web (le « tableau de bord MyFox
Local », voir plus bas) avec beaucoup plus de réglages fins que ce que Jeedom expose directement :
caméras, scénarios détaillés, notifications, sécurité...

## Prérequis

- Une centrale Myfox (Evology Zen ou Home Control 2) **sur le même réseau local** que Jeedom.
- Jeedom 4.6 ou plus récent.
- Un accès administrateur à votre routeur/box internet (pour l'étape de redirection DNS, voir
  plus bas) — ou, à défaut, la possibilité d'utiliser le serveur DNS intégré au plugin.

## Installation

1. Installez le plugin depuis le market Jeedom (ou en l'ajoutant manuellement si vous utilisez une
   version bêta/GitHub).
2. Jeedom installe automatiquement les dépendances Python nécessaires (barre de progression dans
   l'onglet du plugin). Cela peut prendre quelques minutes.
3. Activez le plugin.

À ce stade, le plugin est installé mais **la centrale ne parle pas encore à Jeedom** : il reste
l'étape réseau ci-dessous, obligatoire.

## Étape obligatoire : rediriger la centrale vers Jeedom

La centrale d'alarme cherche à joindre `core.steadyfox.com` (le serveur Myfox) sur le réseau. Il faut que ce
nom soit redirigé vers l'adresse IP de votre box Jeedom, pour qu'il arrive sur le démon au lieu
d'internet. Deux façons de faire :

### Option A — Vous avez déjà Pi-hole, dnsmasq, ou un routeur qui permet des redirections DNS

Ajoutez une entrée DNS locale :

```
core.steadyfox.com  ->  <adresse IP de votre box Jeedom>
```

C'est l'option la plus simple si vous avez déjà un de ces outils.

### Option B — Vous n'avez rien de tout ça : utilisez le serveur DNS intégré au plugin

Dans l'onglet de configuration du plugin, section **« Serveur DNS intégré »**, cochez **Activer**.
Le démon fera alors lui-même office de serveur DNS pour tout le réseau (il répond pour
`core.steadyfox.com`, et transfère toutes les autres requêtes vers un DNS public comme avant).

Il faut ensuite indiquer **à votre routeur/box internet** (dans ses réglages DHCP) d'utiliser
l'adresse IP de la box Jeedom comme serveur DNS pour tout le réseau.

> ⚠️ **Redémarrez la centrale** (coupure secteur ~10 secondes, sans toucher à sa batterie) après avoir
> mis en place la redirection : elle ne relit sa configuration réseau qu'à l'ouverture d'une nouvelle
> session.

Une fois la redirection active, redémarrez le démon depuis l'onglet du plugin. S'il reçoit bien la
connexion de la centrale, le tableau de bord passera à l'état « Centrale connectée ».

## Configuration du plugin

Dans l'onglet de configuration (icône de la clé à molette, ou l'onglet « Configuration ») :

- **Port web** — port de l'interface web MyFox Local (8081 par défaut).
- **Clé API locale Myfox** — à créer depuis le tableau de bord MyFox Local (onglet *Sécurité* →
  *Clés d'intégration*), puis à coller ici. Elle n'est utilisée que pour Armer total / Armer partiel /
  Désarmer. Les autres commandes (équipements, état) n'en ont pas besoin : elles arrivent toutes
  seules.
- **Serveur DNS intégré** — voir l'étape réseau ci-dessus. À activer seulement si vous n'avez pas déjà
  Pi-hole/dnsmasq/une redirection DNS sur votre routeur.
- **Garde TCP** — à activer si vous constatez que la centrale se déconnecte à chaque
  redémarrage du démon (et ne se reconnecte pas seule). Il maintient la connexion de la centrale
  ouverte pendant que le démon redémarre, de façon transparente.

Après chaque changement ici, **redémarrez le démon** pour qu'il en tienne compte.

## Utilisation au quotidien

- Les commandes **Armer total**, **Armer partiel**, **Désarmer**, **État alarme** et **Alarme armée**
  sont créées automatiquement sur l'équipement du plugin — rien à faire.
- Les prises, modules et volets visibles dans l'onglet « Équipements » du tableau de bord MyFox Local
  deviennent automatiquement des commandes Jeedom (ON/OFF pour une prise ou un module, Monter /
  Descendre / Arrêter pour un volet). Elles apparaissent et disparaissent toutes seules si vous ajoutez
  ou retirez un appareil côté MyFox Local.
- Les capteurs connus de la centrale (température, détecteurs...) remontent aussi comme des commandes,
  avec un nom lisible repris du tableau de bord.
- L'état remonte en temps réel : le démon prévient Jeedom lui-même à chaque changement, pas besoin
  d'attendre un cycle d'interrogation.

## Le tableau de bord « MyFox Local »

Le démon a sa propre interface web, accessible directement (lien dans l'onglet du plugin, ou
`http://<ip de Jeedom>:<port configuré>`). C'est là que se passe l'essentiel des réglages fins :

- Armement/désarmement, pilotage direct des équipements.
- Gestion des caméras (photo, flux en direct, détection de mouvement, vie privée).
- Création et modification des scénarios.
- Notifications (mail, SMS, ntfy, Telegram, Pushover...), indépendantes de Jeedom.
- Comptes et droits d'accès si plusieurs personnes doivent s'y connecter.
- Historique des événements.

Ce tableau de bord fonctionne seul, même sans Jeedom — le plugin ne fait qu'y relayer les commandes et
en récupérer l'état.

## Dépannage

**La centrale reste « hors ligne » après l'installation**
→ La redirection DNS n'est probablement pas en place, ou la centrale n'a pas encore redémarré depuis
qu'elle a été faite. Vérifiez avec `nslookup core.steadyfox.com` depuis un appareil du réseau : il doit
répondre l'adresse IP de la box Jeedom, pas une adresse Myfox.

**Tout le réseau perd internet après avoir activé le serveur DNS intégré**
→ Mettez à jour le plugin à la dernière version : une protection contre ce cas précis (la box Jeedom
qui se désigne elle-même comme son propre serveur DNS en boucle) a été ajoutée.

**La centrale se déconnecte à chaque redémarrage du démon**
→ Activez l'option « Garde TCP permanent » dans la configuration.

**Les commandes Armer/Désarmer ne répondent pas, mais l'état remonte bien**
→ Vérifiez la clé API locale : créez-en une depuis le tableau de bord MyFox Local (*Sécurité* → *Clés
d'intégration*) et collez-la dans la configuration du plugin, puis redémarrez le démon.

## Sécurité

La liaison entre la centrale et le démon n'est **ni chiffrée ni authentifiée** (c'est le protocole
d'origine de Myfox, pas une limite de ce plugin). Ne mettez jamais ce démon ou son port en accès
direct depuis internet ; gardez-le strictement sur votre réseau local.

## Pour aller plus loin

Le script du démon contient sa propre documentation technique très détaillée (protocole, tous les
ordres connus, historique des observations...), consultable directement sur le site web local.
