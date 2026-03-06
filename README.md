# 🍷 Affût Heures

**Application de saisie des heures de travail pour le Domaine L'Affût**

Une application web moderne et intuitive permettant aux employés de saisir et suivre leurs heures de travail, avec un tableau de bord administrateur pour la gestion centralisée.

---

## 📋 Fonctionnalités principales

### Pour les employés
- ✏️ **Saisie des heures** : Enregistrer le temps de travail par séquence (début/fin avec précision au 5 minutes)
- 🎯 **Gestion des activités** : Sélectionner parmi une liste d'activités prédéfinies ou ajouter une activité personnalisée
- 🏞️ **Parcelles/Lieux-dits** : Associer les heures à des parcelles spécifiques (CVI, cépage, lieu)
- ☕ **Gestion de la pause** : Enregistrer les horaires de pause déjeuner
- 📅 **Historique** : Consulter et modifier l'historique de travail précédent
- 💾 **Validation** : Marquer une journée comme complète/validée
- 📱 **Progressive Web App** : Application installable sur mobile

### Pour les administrateurs
- 👥 **Gestion des employés** : Ajouter/modifier/activer/désactiver des employés
- ⚙️ **Paramètres** : Configurer les heures cibles hebdomadaires et ajustements de solde
- 📊 **Exports Excel** : Exporter les données de travail pour analyse ou paie
- 📈 **Suivi global** : Voir toutes les séquences de travail par période
- 🛠️ **Maintenance** : Gérer les activités et parcelles disponibles

---

## 🛠️ Stack technique

- **Frontend** : HTML5, CSS3, JavaScript vanilla (ES6+)
- **Backend** : Supabase (PostgreSQL)
- **Authentification** : Supabase Auth
- **Hébergement** : GitHub Pages
- **Dépendances externes** :
  - [Supabase JS Client](https://www.npmjs.com/package/@supabase/supabase-js) — ORM/client BD
  - [SheetJS (XLSX)](https://sheetjs.com/) — Export Excel

---

## 📁 Structure du projet

```
affut-heures/
├── index.html          # Interface employé
├── admin.html          # Interface administrateur
├── .gitignore          # Fichiers à ignorer
├── CNAME               # Configuration domaine personnalisé
└── README.md           # Ce fichier
```

### Architecture du code

**index.html** (~62 KB)
- UI pour la saisie des heures
- Gestion d'état côté client (objet `S`)
- Fonctions de formatage et calcul
- Intégration Supabase

**admin.html** (~69 KB)
- Tableau de bord administrateur
- Gestion des employés
- Exports et rapports
- Configuration du système

---

## 🚀 Installation & Utilisation

### Prérequis
- Compte Supabase configuré avec les tables appropriées
- Variables d'environnement Supabase (URL et clé API)

### Démarrage

1. **Cloner le dépôt**
   ```bash
   git clone https://github.com/Mat075/affut-heures.git
   cd affut-heures
   ```

2. **Configurer Supabase**
   - Remplacer les identifiants Supabase dans `index.html` et `admin.html`
   - S'assurer que les tables existent dans la base de données

3. **Accéder à l'application**
   - URL locale : `file:///path/to/index.html`
   - URL en production : domaine configuré dans `CNAME`

---

## 📊 Modèle de données (Supabase)

### Tables principales

| Table | Description |
|-------|-------------|
| `employees` | Employés (nom, heures/semaine, solde) |
| `day_entries` | Journées de travail (employé, date, pause) |
| `work_sequences` | Séquences individuelles (début, fin, activité, parcelle) |
| `activities` | Types d'activités disponibles |
| `parcels` | Parcelles/vignes (CVI, cépage, lieu-dit) |

---

## ⚙️ Configuration

### Horaires
- Les heures doivent être saisies en tranches de **5 minutes** (ex : 08:00, 08:05, 08:10)
- Format 24h

### Activités personnalisées
- Sélectionner "Autre" pour ajouter une activité non listée
- La description est enregistrée dans `other_activity_label`

### Solde horaire
- Calculé automatiquement basé sur `weekly_hours_target` et `balance_offset_minutes`
- Visible dans l'interface employé

---

## 🔐 Sécurité

- Authentification via Supabase Auth
- Données transmises via HTTPS en production
- Échappement des caractères spéciaux (XSS prevention)
- RLS (Row Level Security) recommandé sur Supabase

**⚠️ Attention** : L'application stocke les données sensibles côté client. Ne pas exposer les clés Supabase publiques dans les fichiers.

---

## 📱 Fonctionnalités Mobile

L'application supporte l'installation PWA sur mobile :
- Meta tags configurés pour iOS et Android
- Thème de couleur : `#E0004D`
- Interface responsive

---

## 🐛 Gestion des erreurs

L'application inclut :
- Validation des horaires (fin après début, tranches de 5 min)
- Messages de toast pour les retours utilisateur
- Gestion des erreurs Supabase
- Historisation des modifications (timestamps)

---

## 🎨 Personnalisation

### Couleurs
Modifier les variables CSS dans les balises `<style>` :
```javascript
:root {
  --bg:           #F8F5F0;
  --surface:      #FFFFFF;
  --primary:      #001A72;
  --primary-dk:   #001050;
  --accent:       #E0004D;
  // ... autres variables
}
```

### Polices
Chargées depuis Google Fonts (Montserrat)

---

## 📞 Support & Contact

Pour des questions ou problèmes, consulter l'administrateur du Domaine L'Affût.

---

## 📜 Licence

Propriété du Domaine L'Affût — Usage interne uniquement.

---

**Dernière mise à jour** : 2026-03-04
