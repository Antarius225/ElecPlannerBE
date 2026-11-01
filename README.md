# ElecPlannerBE

Éditeur web de **plan de position** et de **schéma unifilaire** pour une installation électrique domestique belge (RGIE, Livre 1).

- Plan de base importé depuis draw.io (murs, fenêtres, portes, escaliers ; 1 unité = 1 cm)
- Palette de symboles : prises, éclairage, commandes, appareils fixes, tableau, terre, courants faibles
- Circuits (repère, disjoncteur, section, câble, classe de réaction au feu CPR) et différentiels 300 mA / 30 mA
- Symbole « Gaine en attente » pour les réservations (borne de recharge VE, PAC, PV…) avec code affiché
- Schéma unifilaire généré automatiquement, repères A1, A2… communs au plan
- Contrôles indicatifs (8 prises max par circuit, section/calibre, DDR 30 mA, 8 circuits par DDR, classe feu renseignée, résistance de terre)
- Exports : SVG (plan, unifilaire), `.drawio.svg` éditable dans draw.io, CSV des points, sauvegarde JSON

Application statique en un seul fichier (`index.html`), sans dépendance. Les données sont enregistrées dans le navigateur (localStorage) ; utiliser l'export JSON pour sauvegarder ou changer d'appareil.

> Les contrôles sont indicatifs. Le contrôle de conformité par un organisme agréé reste la référence.
