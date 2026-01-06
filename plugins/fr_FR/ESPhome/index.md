# 📘 Documentation du Plugin ESPhome


## Présentation

### Le plugin ESPHome permet de gérer facilement des appareils ESP32 / ESP8266 depuis Jeedom, sans passer par la ligne de commande.

  Il permet de :

  - Créer des équipements ESPHome

  - Générer automatiquement la configuration ESPHome (YAML)

  - Valider la configuration

  - Installer ou mettre à jour le firmware (USB ou OTA)

  - Administrer les ESP à distance

## Prérequis

### Matériel

  Un ESP compatible :

  - ESP32

  - ESP8266

  - Connexion réseau fonctionnelle (Wi-Fi)

> [!IMPORTANT]
> Pour les autres cartes que ESPhome peut gérer, je n'ai pas pu les tester. Merci de m'informer si vous avez d'autres cartes que ESPhome (Officiel) peut gérer.

### Logiciel

  - Jeedom ≥ 4.4

  - Plugin ESPHome installé et actif

  - ESPHome installé automatiquement par le plugin

### Renseignement du compte et mot de passe wifi
Il faut renseigner le compte et le mot de passe dans le panneau de configuration du plugin ESPhome.
![enter image description here](../../images/ESPhome/wifi.PNG)

## Création d’un équipement ESPHome
Aller dans Plugin->Protocole domotique->ESPhome puis cliquer sur **Ajouter**.
Renseiger:
- **Nom du ESPhome**
- **Obget parent**
- **Catégorie**
- **Activer l'equipement**

## Configuration de la carte

### Platforme
Sélectionnez la plateforme correspondant à votre matériel :

|  Plateforme	  |    Exemple          |
|-------------- | --------------      |
|    ESP32	    |   ESP32 Dev Module  |
|   ESP8266	    |      NodeMCU        |

### Carte (Board)
Après avoir choisi la plateforme, la liste des cartes disponibles apparaît automatiquement.

Exemples :

- esp32dev

- nodemcuv2

- d1_mini

### Port série (USB)
- Branchez votre ESP au Jeedom

- Sélectionnez le port (/dev/ttyUSB0, /dev/ttyACM0, etc

> [!WARNING]
> Obligatoire uniquement pour une première installation USB.

### Génération du fichier YAML
Le fichier ESPHome est généré automatiquement lors de la sauvegarde de l’équipement.

### Règles importantes sur le nom

- ❌ Pas d’accent

- ❌ Pas de caractères spéciaux

## Onglet YAML
### Visualisation
Dans l’onglet YAML, vous pouvez :

- Voir la configuration générée

- Modifier manuellement le YAML si nécessaire

> [!NOTE]
> **Exemple**.
> 
> ![enter image description here](../../images/ESPhome/config_yaml.PNG)


Vous pouver modifier ou rajouter que entre **# === USER CODE BEGIN ===** et **# === USER CODE END ===**.
Puis cliquer sur sauvegarder pour que les paramètres soit pris en compte.

> [!WARNING]
> Il ne faut sur tous pas supprimer **# === USER CODE BEGIN ===** et **# === USER CODE END ===** au moment de la sauvegarde.

## Validation de la configuration
### Vérifier le YAML

- Cliquez sur Validation YAML

- Le plugin analyse la configuration
### Résultat attendu
- ✅ Succès : **INFO Configuration is valid!**
- ❌ Erreur : **ERROR Error while reading configuration**

>[!important]
>Tant que la validation échoue, l’installation YAML USB est bloquée.

## Installation YAML USB
### Première installation (USB)

- Branchez l’ESP en USB

- Sélectionnez le port série

- Cliquez sur Installation YAML USB

- Suivez la progression

## Mise à jour OTA (sans fil)
Si l’ESP est déjà installé :

- Le plugin détecte automatiquement le mode OTA

- Aucune action USB requise

- Le configuration yaml est envoyé par Wi-Fi
- ✅ Succès : **INFO OTA successful**

## API sécurisée ESPHome

Le plugin utilise l’API native ESPHome chiffrée.

### Clé d’encryption

- Générée automatiquement

- Unique par équipement

- Protège la communication Jeedom ↔ ESP


