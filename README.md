# ElecPlannerBE

Éditeur web de **plan de position** et de **schéma unifilaire** pour une installation électrique domestique belge (RGIE, Livre 1).

- Plan de base importé depuis draw.io (murs, fenêtres, portes, escaliers ; 1 unité = 1 cm)
- Google Drive : import (plan draw.io ou sauvegarde JSON, type reconnu automatiquement) et sauvegarde automatique du projet
- Palette de symboles : prises, éclairage, commandes, appareils fixes, tableau, terre, courants faibles
- Circuits (repère, disjoncteur, section, câble, classe de réaction au feu CPR) et différentiels 300 mA / 30 mA
- Symbole « Gaine en attente » pour les réservations (borne de recharge VE, PAC, PV…) avec code affiché
- Schéma unifilaire généré automatiquement, repères A1, A2… communs au plan
- Contrôles indicatifs (8 prises max par circuit, section/calibre, DDR 30 mA, 8 circuits par DDR, classe feu renseignée, résistance de terre)
- Exports : SVG (plan, unifilaire), `.drawio.svg` éditable dans draw.io, CSV des points, sauvegarde JSON

Application statique en un seul fichier (`index.html`), sans dépendance. Les données sont enregistrées dans le navigateur (localStorage) ; utiliser l'export JSON pour sauvegarder ou changer d'appareil.

> Les contrôles sont indicatifs. Le contrôle de conformité par un organisme agréé reste la référence.

## Google Drive

**Sauvegarde automatique** : « Enregistrer sur Drive » (onglet Projet) crée le fichier JSON dans un dossier « Plan électrique », puis chaque modification y est enregistrée après quelques secondes. Ouvrir une sauvegarde JSON depuis Drive lie aussi ce fichier. Avant chaque écriture, l'app vérifie que le fichier n'a pas été modifié ailleurs (autre appareil) ; si c'est le cas, la sauvegarde est suspendue et l'onglet Projet propose de charger la version Drive ou de l'écraser. La session Google dure environ une heure : l'indicateur sous le titre propose alors de se reconnecter d'un clic. Charger une sauvegarde locale ou tout réinitialiser délie le fichier Drive.

L'intégration Drive utilise Google Identity Services et Google Picker avec la portée `drive.file` : l'app ne lit que les fichiers choisis dans le sélecteur. Il faut un projet Google Cloud à soi :

1. Activer **Google Drive API** et **Google Picker API**.
2. Configurer l'écran de consentement OAuth (type *Externe*, en mode test, avec son propre compte comme utilisateur test).
3. Créer un **ID client OAuth** de type *Application Web*, origine JavaScript autorisée : l'URL du site (ex. `https://antarius225.github.io`).
4. Créer une **clé API**, restreinte aux deux API ci-dessus. En restriction d'application « Sites Web », ajouter **deux** entrées : l'URL du site (ex. `https://antarius225.github.io/*`) **et `https://docs.google.com/*`** — le sélecteur Google s'affiche depuis ce domaine ; sans elle, il répond « La clé de développement d'API n'est pas valide ». Le bouton « Tester la configuration » de l'app vérifie le reste.
5. Coller l'ID client et la clé API dans l'onglet **Projet → Google Drive** de l'app. Ils restent dans le navigateur (localStorage) et ne sont jamais inclus dans les sauvegardes JSON.
