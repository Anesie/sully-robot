# 🤖 Projet Sully : Robot Collecteur Autonome (LeJOS EV3)

## 📖 Présentation
**Sully** est un robot autonome développé en **Java** avec la bibliothèque **LeJOS** pour la brique LEGO Mindstorms EV3. 
L'objectif principal de Sully est d'explorer son environnement pour détecter, attraper et ramener le maximum de palets dans une zone de départ, le tout dans un temps imparti.

Ce projet met en œuvre des concepts avancés de robotique logicielle : machine à états finis, contrôle de châssis différentiel, odométrie basique (système de boussole interne) et traitement de données sensorielles en temps réel.

## ⚙️ Architecture du Projet
Le code est structuré en trois classes principales pour séparer la logique décisionnelle, les actions mécaniques et l'acquisition de données :

*   **`SullyMain.java` (Le Cerveau) :** Contient la boucle principale du programme structurée sous forme de **Machine à États** (`Debut`, `RechercherPalet`, `PrendrePalet`, `RamenerPalet`, `Fin`). Elle gère les transitions logiques de Sully en fonction des retours des capteurs.
*   **`Actions.java` (La Motricité) :** Encapsule toute la logique de déplacement (via `MovePilot` et `WheeledChassis`). Elle gère le contrôle des moteurs des roues (vitesses modulables), le système d'ouverture/fermeture des pinces, et intègre une "boussole" interne basée sur le temps de rotation pour traquer l'orientation du robot.
*   **`Capteurs.java` (Les Sens) :** Gère l'interface matérielle avec l'environnement. Elle initialise et interroge :
    *   Le capteur à **Ultrasons** (détection des palets au loin).
    *   Le capteur **Tactile / Pression** (confirmation que le palet est bien dans la pince).
    *   Le capteur de **Couleur** (pour l'analyse du sol).

## ✨ Fonctionnalités Principales
1.  **Recherche Intelligente (Balayage) :** Sully effectue des rotations sur lui-même à vitesse réduite. Il surveille les variations brusques de distance (calcul du `seuil`) via l'ultrason pour isoler la position d'un palet.
2.  **Préhension Sécurisée :** Une fois le palet repéré, Sully avance. Les pinces ne se ferment que lorsque le capteur de pression confirme le contact physique avec l'objet.
3.  **Odométrie et Retour à la Base :** Le robot traque son angle de rotation via une variable `boussole` incrémentée lors de ses mouvements. Une fois le palet attrapé, Sully calcule l'angle de retour exact (`getAnglePoints`) pour le ramener à son point de départ.
4.  **Mouvements Aléatoires & Évitement :** Si aucun palet n'est détecté lors d'un balayage, Sully se déplace aléatoirement pour changer de point de vue et relancer une recherche.

## 🛠️ Technologies Utilisées
*   **Langage :** Java (Orienté Objet)
*   **Framework Robotique :** [LeJOS EV3](http://www.lejos.org/ev3.php)
*   **Matériel :** LEGO Mindstorms EV3 (2 Moteurs larges pour les roues, 1 Moteur pour la pince, Capteurs Ultrason, Tactile et Couleur).

## 🚀 Prérequis et Exécution
Pour compiler et exécuter ce projet sur votre propre robot EV3 :
1. Assurez-vous que votre brique EV3 est flashée avec une carte SD contenant l'OS **LeJOS**.
2. Installez le plugin LeJOS sur votre IDE (Eclipse recommandé).
3. Importez ce dépôt comme un projet Java/LeJOS.
4. Connectez le robot via Bluetooth ou Wi-Fi.
5. Lancez la compilation et l'exécution directement depuis l'IDE.
6. Appuyez sur n'importe quel bouton de la brique EV3 pour démarrer le cycle (`Button.waitForAnyPress()`).
