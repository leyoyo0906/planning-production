# 🏭 Planning de Production — NC-MX & TE-ME

Dashboard interactif avec **synchronisation temps réel** entre tous les utilisateurs.  
Aucun serveur, aucune installation. Juste un lien.

---

## 🚀 Mise en place complète (10 minutes)

### PARTIE 1 — Firebase (base de données gratuite)

#### 1.1 Créer un projet Firebase
1. Allez sur **[console.firebase.google.com](https://console.firebase.google.com/)**
2. Connectez-vous avec votre compte Google
3. Cliquez **"Créer un projet"**
4. Nom du projet : `planning-production`
5. Décochez Google Analytics (pas besoin) → **Créer le projet**
6. Attendez 30 secondes → **Continuer**

#### 1.2 Créer la base de données
1. Dans le menu gauche, cliquez **"Realtime Database"**
2. Cliquez **"Créer une base de données"**
3. Emplacement : **europe-west1** (Belgique)
4. Sélectionnez **"Mode test"** → **Activer**

#### 1.3 Récupérer la configuration
1. Cliquez l'icône **⚙️ engrenage** en haut à gauche → **"Paramètres du projet"**
2. Descendez jusqu'à **"Vos applications"**
3. Cliquez l'icône **`</>`** (Web)
4. Nom : `planning` → **Enregistrer l'application**
5. Vous voyez un bloc de code avec `apiKey`, `authDomain`, etc.
6. **Copiez ces 4 valeurs** :
   - `apiKey`
   - `authDomain`
   - `databaseURL`
   - `projectId`

#### 1.4 Coller dans index.html
Ouvrez `index.html` dans un éditeur de texte (Bloc-notes) et trouvez ces lignes en haut du script :

```javascript
var FIREBASE_CONFIG = {
  apiKey: "COLLER_ICI",
  authDomain: "VOTRE-PROJET.firebaseapp.com",
  databaseURL: "https://VOTRE-PROJET-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "VOTRE-PROJET"
};
```

Remplacez les valeurs par celles copiées depuis Firebase. Exemple :

```javascript
var FIREBASE_CONFIG = {
  apiKey: "AIzaSyB1234567890abcdef",
  authDomain: "planning-production-abc12.firebaseapp.com",
  databaseURL: "https://planning-production-abc12-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "planning-production-abc12"
};
```

Sauvegardez le fichier.

---

### PARTIE 2 — GitHub Pages

#### 2.1 Créer le dépôt GitHub
1. Allez sur **[github.com/new](https://github.com/new)**
2. Nom : `planning-production`
3. Cliquez **Create repository**

#### 2.2 Uploader les fichiers
1. Cliquez **"uploading an existing file"**
2. Glissez les 3 fichiers :
   - `index.html` (modifié avec la config Firebase)
   - `README.md`
   - `production.xlsx` (votre fichier Excel renommé)
3. Cliquez **Commit changes**

#### 2.3 Activer GitHub Pages
1. **Settings** → **Pages**
2. Source : `main` / `/ (root)`
3. **Save** → attendez 2 minutes

#### 2.4 C'est en ligne ! 🎉
`https://votre-pseudo.github.io/planning-production/`

---

## 📊 Mise à jour hebdomadaire de l'Excel

1. Renommez votre fichier en **`production.xlsx`**
2. Sur GitHub : **Add file** → **Upload files**
3. Glissez le nouveau fichier → **Commit changes**
4. Les utilisateurs cliquent **🔄 Actualiser** (ou rechargent la page)

---

## 🔄 Synchronisation temps réel

- Quand un utilisateur modifie le suivi → **tous les autres voient le changement en 1-2 secondes**
- L'indicateur vert **🟢 Synchronisé** confirme la connexion
- Si hors ligne → **🔴 Hors ligne** (les données sont sauvées localement et synchronisées au retour)
- **Aucune manipulation nécessaire** — c'est 100% automatique

---

## ⚠️ Sécurité Firebase

La base de données est en **mode test** (lecture/écriture ouverte).
Pour un usage long terme (> 30 jours), mettez à jour les règles de sécurité :

Dans Firebase Console → Realtime Database → Règles :
```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

Cela garde l'accès ouvert (suffisant pour un outil interne).
