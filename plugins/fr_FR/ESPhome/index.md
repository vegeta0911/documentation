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
    
> [!WARNING]
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
