# projet_deep_learning

# Système d’Atterrissage Assisté par Vision – Projet Deep Learning
Ce projet implémente un système embarqué permettant d’évaluer en temps réel si une zone est sûre pour l’atterrissage à partir d’un flux vidéo. Il utilise un modèle YOLO entraîné pour détecter des zones d’intérêt et applique une logique décisionnelle basée sur la surface relative des objets détectés.

## Objectif
Le système doit :

1. Capturer un flux vidéo en temps réel via une webcam.

2. Exécuter une détection d’objets avec un modèle YOLO pré‑entraîné.

3. Analyser les bounding boxes détectées.

4. Déterminer si la zone est « SAFE TO LAND » ou « DO NOT LAND » selon un seuil d’aire.

5. Afficher le résultat directement sur l’image annotée.

## Fonctionnement
- Initialisation
Il est important de mettre le dataset ainsi que le poid dans le dossier ou se trouve les codes. 

- Acquisition vidéo  
Une webcam est ouverte via OpenCV. Chaque image est envoyée au modèle YOLO.

- Détection d’objets  
Le modèle YOLO (fichier best.pt) est chargé sur GPU si disponible, sinon sur CPU.

- Les paramètres principaux sont :

TAU_CONF : seuil minimal de confiance

TAU_AREA : seuil d’aire relative pour la décision

- Décision d’atterrissage  
La fonction decision_landing() calcule l’aire relative de chaque bounding box, retient la plus grande et la compare au seuil défini.
Elle renvoie un booléen indiquant si l’atterrissage est possible.

- Affichage  
Les bounding boxes et la décision finale sont affichées sur l’image en temps réel.

- Dépendances
Installer les bibliothèques nécessaires :

pip install torch ultralytics opencv-python

## Paramètres principaux 

MODEL_PATH = "./runs/detect/train/weights/best.pt"
TAU_CONF = 0.5
TAU_AREA = 0.05
CAMERA_INDEX = 0
Ils permettent d’ajuster :

- la confiance minimale des prédictions,

- la tolérance de décision,

- la source vidéo utilisée.

## Exécution
Lancer le script :

python main.py

Conditions :

- Une webcam doit être disponible.

- Le modèle YOLO doit être présent au chemin indiqué.

Pendant l’exécution :

- Une fenêtre affiche le flux annoté avec la camera active.

- Appuyer sur la touche « q » pour quitter.

Améliorations possibles
- Filtrage temporel des décisions (moyenne glissante).

- Optimisation du modèle pour systèmes embarqués.

- Ajout d’un retour sonore ou d’une interface plus complète.