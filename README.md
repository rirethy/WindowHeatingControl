# 🌡️ Window Heating Control (WHC) for Home Assistant

[![Ouvrir votre instance Home Assistant et importer ce blueprint.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Frirethy%2FWindowHeatingControl%2Fblob%2Fmain%2Fwindow_heating_control.yaml)

Une automatisation avancée et robuste pour Home Assistant qui gère intelligemment vos radiateurs selon l'état de vos fenêtres. Ne gaspillez plus d'énergie en aérant vos pièces !

## ✨ Fonctionnalités

- **💾 Sauvegarde & Restauration Précise** : Utilise une scène dynamique pour mémoriser l'état exact (température de consigne, mode, etc.) avant la coupure et le restaurer fidèlement à la fermeture.
- **🚨 Alerte Oubli** : Envoie une notification prioritaire (rouge) si une fenêtre est restée ouverte au-delà d'un délai défini.
- **🛡️ Sécurité Anti-Redémarrage** : Grâce à un flag (`input_boolean`) et une logique de "fallback", le chauffage redémarre en mode `auto` même si le serveur a redémarré pendant que la fenêtre était ouverte.
- **🍃 Mode Été Natif** : L'automatisation ignore l'ouverture des fenêtres si le chauffage est déjà éteint, évitant les notifications inutiles durant la belle saison.
- **📱 Notifications Interactives** : Alertes avec température extérieure, horodatage `(HH:MM)` et lien direct vers votre tableau de bord favori au clic sur le téléphone.

## ⚙️ Détails des Paramètres (Inputs)

| Paramètre | Description |
| :--- | :--- |
| **Capteur de fenêtre** | L'entité `binary_sensor` qui détecte l'ouverture. |
| **Thermostats** | Liste des entités `climate` à piloter dans la pièce. |
| **Nom de la pièce** | Utilisé pour personnaliser les notifications et nommer la scène de sauvegarde. |
| **Boolean d'état (Flag)** | Un `input_boolean` qui permet de mémoriser que l'automatisation a coupé le chauffage. |
| **Délai avant coupure** | Temps d'attente (secondes) avant d'éteindre pour ignorer les ouvertures rapides. |
| **Délai avant remise** | Temps d'attente (minutes) après fermeture avant de relancer le chauffage. |
| **Délai alerte Oubli** | Temps (minutes) après lequel une alerte "Urgence" est envoyée. |
| **Capteur de température** | Entrée météo ou sonde locale pour enrichir les notifications. |
| **Chemin au clic** | URL relative (ex: `/lovelace/thermostats`) ouvrant la page liée à la notification. |

## 🔧 Configuration des Entrées (Helpers)

Ce blueprint nécessite un **Flag (bouton d'état)** pour chaque pièce afin de garantir une reprise parfaite après redémarrage.

### Option A : Via l'interface (Simple)
1. Allez dans **Paramètres** > **Appareils et services** > **Entrées**.
2. Cliquez sur **+ Créer une entrée** > **Interrupteur (input_boolean)**.
3. Nommez-le, par exemple : `Flag Chauffage Salon`.

### Option B : Via le fichier `configuration.yaml` (Rapide)
```yaml
input_boolean:
  flag_chauffage_salon:
    name: "Flag Chauffage Salon"
    icon: mdi:window-open-variant
```

###🚀 Installation
Assurez-vous d'avoir créé votre input_boolean (voir section ci-dessus).

Cliquez sur le bouton Import Blueprint en haut de ce README.

Home Assistant vous proposera d'importer le fichier directement depuis GitHub.

Allez dans Paramètres > Automatisations et scènes > Créer une automatisation.

Sélectionnez Window Heating Control (WHC) dans la liste et remplissez vos entités.
