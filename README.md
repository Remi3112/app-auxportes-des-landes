# 🏡 CRM Conciergerie — Aux portes des landes

Application CRM complète single-file connectée à Airtable.  
Aucune installation, aucun build — un seul fichier HTML à déposer sur GitHub Pages.

---

## ✨ Fonctionnalités

### Interface Admin
- Toutes les tables Airtable chargées dynamiquement
- Toutes les vues disponibles (Grid, Kanban, Gallery…)
- Recherche, tri par colonne
- Création / modification / suppression de fiches
- Formulaires intégrés : Prospect · Propriétaire · Prestataire

### Portail Prestataire (accès limité)
- Interface séparée via lien unique
- Accès restreint : Logements · Réservations · Agents de ménage
- CRUD complet sur les tables autorisées
- Formulaire déclaration d'incident intégré

### Formulaires partageables
- Lien public : formulaire Prospect
- Lien public : formulaire Propriétaire (avec nom pré-rempli)
- Liens portail agent générés depuis la liste des agents

---

## 🚀 Déploiement GitHub Pages

### Étape 1 — Créer le repo
```
1. github.com → New repository
2. Nom : crm-portes-landes (ou votre choix)
3. Public ✓ → Create repository
```

### Étape 2 — Uploader le fichier
```
1. Upload files → glisser index.html
2. Commit changes
```

### Étape 3 — Activer GitHub Pages
```
Settings → Pages
Source : Deploy from a branch
Branch : main → / (root)
Save
```

### Étape 4 — Récupérer l'URL
```
Votre URL : https://VOTRE-USERNAME.github.io/NOM-DU-REPO/
```

> ⏱️ La mise en ligne prend 1 à 3 minutes après activation.

---

## 🔑 Configuration Airtable

### Créer un Personal Access Token
```
1. Aller sur : airtable.com/create/tokens
2. Cliquer : + Create new token
3. Nom : CRM Portes des Landes
4. Scopes à cocher :
   ✓ data.records:read
   ✓ data.records:write
   ✓ schema.bases:read
5. Access : sélectionner votre base
6. Cliquer : Create token
7. Copier le token (commence par "pat…")
```

> ⚠️ Le token n'est affiché qu'une seule fois — copiez-le immédiatement.

### Récupérer l'ID de votre base
```
Ouvrir votre base Airtable dans le navigateur
URL : https://airtable.com/appXXXXXXXXXXXXXX/...
                              ^^^^^^^^^^^^^^^^
                              C'est votre Base ID
```

---

## 📋 Structure Airtable recommandée

L'application détecte automatiquement les tables par leur nom.

### Tables détectées automatiquement

| Nom contient | Type | Icône |
|---|---|---|
| `logement`, `bien`, `annonce` | Logements | 🏡 |
| `réservation`, `reservation`, `booking` | Réservations | 📅 |
| `propriétaire`, `proprietaire` | Propriétaires | 👤 |
| `prospect` | Prospects | 🎯 |
| `agent`, `prestataire`, `ménage` | Agents | 🧹 |
| `litige` | Litiges | ⚖️ |
| `avis`, `voyageur` | Avis | ⭐ |
| `document`, `contrat` | Documents | 📄 |

### Champs recommandés — Table Litiges

| Champ | Type |
|---|---|
| Agent | Single line text |
| Date | Date |
| Logement | Single line text |
| Type d'incident | Single select |
| Description | Long text |
| Urgence | Single select |
| Propriétaire informé | Checkbox |

---

## 🌐 Modes d'accès — Paramètres URL

L'application supporte 3 modes selon les paramètres dans l'URL.

### Mode 1 — CRM Admin (par défaut)
```
https://votre-site.github.io/crm/
```
- Accès complet à toutes les tables
- Génération des liens partageables
- Formulaires de saisie

---

### Mode 2 — Portail Prestataire
```
https://votre-site.github.io/crm/?mode=prestataire&token=pat…&base=appXXX&name=Marie+Dupont
```

**Paramètres :**
| Paramètre | Description | Exemple |
|---|---|---|
| `mode` | Type d'accès | `prestataire` |
| `token` | Token Airtable | `pat1234567890` |
| `base` | ID de la base | `appacNAbGqdyi38xZ` |
| `name` | Nom de l'agent | `Marie+Dupont` |

**Accès inclus :**
- 🏡 Logements (lecture + modification + création)
- 📅 Réservations (lecture + modification + création)
- 🧹 Agents de ménage (lecture + modification + création)
- ⚖️ Formulaire déclaration d'incident

---

### Mode 3 — Formulaire public
```
https://votre-site.github.io/crm/?form=prospect&token=pat…&base=appXXX
https://votre-site.github.io/crm/?form=proprietaire&token=pat…&base=appXXX&nom=Jean+Dupont
```

**Paramètres :**
| Paramètre | Description | Valeurs |
|---|---|---|
| `form` | Type de formulaire | `prospect` ou `proprietaire` |
| `token` | Token Airtable | `pat…` |
| `base` | ID de la base | `appXXX…` |
| `nom` | Nom pré-rempli (optionnel) | `Jean+Dupont` |

---

## 🔗 Générer les liens depuis l'interface

Dans le CRM Admin :

```
Sidebar → 🔗 Liens de formulaires
```

Cette page permet de :
1. Générer un lien portail prestataire (par nom ou depuis la liste)
2. Copier le lien formulaire Prospect
3. Copier le lien formulaire Propriétaire
4. Générer un lien propriétaire personnalisé (nom pré-rempli)

---

## 🗂️ Structure du repo GitHub

```
mon-repo/
├── index.html     ← L'application complète (unique fichier)
└── README.md      ← Cette documentation
```

---

## 🔐 Sécurité

### Ce que contient le lien prestataire
Le lien contient votre token Airtable en clair dans l'URL.

### Recommandations
- Créer un token dédié par prestataire avec accès limité à votre base
- Ne pas partager les liens sur des canaux publics
- Pour révoquer l'accès d'un prestataire : supprimer son token sur airtable.com/account
- Le repo GitHub peut être **privé** — GitHub Pages fonctionne aussi avec les repos privés (plan payant) ou utilisez un repo public

### Token avec permissions minimales pour prestataires
```
Scopes minimum prestataire :
✓ data.records:read    ← voir les fiches
✓ data.records:write   ← créer / modifier
(Pas besoin de schema.bases:read si les tables sont connues)
```

---

## 🧑‍💻 Technologies utilisées

| Tech | Rôle |
|---|---|
| React 18 (CDN) | Interface utilisateur |
| Babel Standalone (CDN) | Compilation JSX dans le navigateur |
| Airtable REST API | Base de données |
| Google Fonts — Inter | Typographie |
| CSS inline | Styles (aucune dépendance externe) |

Aucun npm, aucun build, aucun serveur Node requis.

---

## 🆘 Résolution des problèmes courants

### "Failed to fetch" à la connexion
- Vérifiez votre connexion internet
- Utilisez Chrome ou Firefox
- Désactivez les extensions de blocage (uBlock, AdGuard)
- Vérifiez que votre token commence bien par `pat`

### "Token invalide [401]"
- Régénérez un nouveau token sur airtable.com/create/tokens
- Vérifiez que vous avez copié le token complet

### "Permissions insuffisantes [403]"
- Vérifiez que les 3 scopes sont cochés sur votre token
- Vérifiez que votre base est sélectionnée dans "Access"

### "Base introuvable [404]"
- Vérifiez l'ID de base (commence par `app`, 17 caractères)
- Vérifiez que votre token a accès à cette base spécifique

### Table litiges non trouvée (portail prestataire)
- Créez une table nommée **"Litiges"** dans votre base Airtable
- L'application cherche une table contenant le mot "litige"

### Les vues n'apparaissent pas
- Vérifiez que le scope `schema.bases:read` est activé
- Sans ce scope, l'application utilise des tables de secours pré-configurées

---

## 📞 Contact & support

CRM développé par **Fluxia** pour **Aux portes des landes**  
Conciergerie Airbnb premium — Landes, France

---

*Fichier index.html · React 18 · Airtable API · Single-file app*
