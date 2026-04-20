# Prompt d’installation/exécution (à donner à un assistant IA)

Copie-colle le texte ci-dessous dans ton assistant IA pour qu’il prépare l’environnement, récupère les modèles, puis démarre l’application.

---

Tu es un assistant de développement. Je viens de cloner ce projet Django de détection de deepfake. Les modèles PyTorch sont ignorés dans le dépôt et doivent être ajoutés manuellement dans le dossier `models/`.

Objectifs :

1. Créer un environnement virtuel Python `.venv` dans la racine du projet.
2. Installer les dépendances depuis `requirements.txt`.
3. Vérifier que les fichiers de modèles `.pt` sont bien présents dans `models/`.
   - Si le dossier `models/` est vide, demande-moi de fournir les fichiers de modèles.
4. Exécuter les migrations Django.
5. Lancer le serveur local.
6. Me donner l’URL locale à ouvrir (par défaut http://127.0.0.1:8000/).

Contraintes importantes :

- Utiliser Windows PowerShell.
- Ne pas créer de sous-shell (pas de `python -c` ou `powershell -c`).
- Si des erreurs surviennent (ex. dlib), proposer la solution la plus simple.

Étapes attendues (PowerShell) :

- `python -m venv .venv`
- `./.venv/Scripts/Activate.ps1`
- `pip install -r requirements.txt`
- Vérifier que `models/*.pt` existe, sinon demander les modèles
- `python manage.py migrate`
- `python manage.py runserver`

Résultat attendu :

- Le site démarre correctement et tu m’indiques le lien local.

---
