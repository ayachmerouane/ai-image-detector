# 🖼️ Détecteur d'images générées par IA

Application web qui détermine si une image (visage) est **réelle** ou **générée par IA**, en laissant l'utilisateur comparer **4 modèles de Deep Learning** entraînés sur le même jeu de données.

🔗 **Démo en ligne : [Hugging Face Space](https://huggingface.co/spaces/merouane02/DL1)**

<!-- Ajoute une capture d'écran de l'application : -->
<!-- ![Aperçu de l'application](docs/apercu.png) -->

## ✨ Fonctionnalités

- Chargement d'une image (PNG, JPG, JPEG, WEBP)
- Choix du modèle parmi 4 architectures
- Prédiction **Réelle / IA** avec le niveau de confiance et la probabilité de chaque classe
- Téléchargement automatique des poids des modèles au premier lancement

## 🧠 Modèles comparés

| Modèle | Type | Détails |
|---|---|---|
| **DenseNet121** | Transfer learning | Backbone DenseNet121 + classifieur personnalisé (Dropout → Linear 512 → ReLU → Dropout → Linear 2) |
| **VGG16 Custom** | Réimplémentation | Architecture VGG16 avec BatchNorm, entraînée from scratch |
| **AlexNet Inspo** | Réimplémentation | Architecture inspirée d'AlexNet |
| **FiveBlockCNN** | CNN maison | 5 blocs Conv → ReLU → MaxPool, couche dense 256, sortie sigmoïde |

📈 **Meilleur résultat : 87,06 % d'accuracy sur le jeu de test avec FiveBlockCNN**, dans le cadre expérimental du dataset utilisé.

<!-- Si tu as les scores des 3 autres modèles, ajoute une colonne « Accuracy test » au tableau. -->

## 🗂️ Préparation des données

1. **Nettoyage** (`script_nettoyage.py`) : fusion de deux datasets, suppression des doublons par hash MD5, détection et recadrage du visage (OpenCV Haar Cascade, avec recadrage central en secours), redimensionnement en 224×224
2. **Découpage** (`split_dataset.py`) : train 70 % / validation 15 % / test 15 % pour les classes `real` et `fake`
3. **Entraînement** : notebooks `deeplearnintraining.ipynb` et `densenet.ipynb`, script `FiveBlockCNN.py` (augmentation : flip horizontal, rotation)

## 🛠️ Stack technique

Python · PyTorch · torchvision · OpenCV · Streamlit · Hugging Face Spaces

## 🚀 Lancer le projet en local

```bash
git clone https://github.com/ayachmerouane/ai-image-detector.git
cd ai-image-detector
pip install -r requirements.txt
streamlit run app.py
```

Les poids des modèles se téléchargent automatiquement depuis Hugging Face au premier lancement.

## 📁 Structure

```
ai-image-detector/
├── app.py                      ← Application Streamlit (4 modèles)
├── FiveBlockCNN.py             ← Entraînement du CNN maison
├── deeplearnintraining.ipynb   ← Entraînement VGG16 / AlexNet
├── densenet.ipynb              ← Transfer learning DenseNet121
├── script_nettoyage.py         ← Nettoyage et recadrage des visages
├── split_dataset.py            ← Découpage train / val / test
└── requirements.txt
```

## 👤 Auteur

**Merouane Ayach** — [GitHub](https://github.com/ayachmerouane)
