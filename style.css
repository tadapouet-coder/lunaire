# Lunaire — suivi de cycle

Application web simple pour suivre les cycles menstruels : début/fin des
règles, ovulation, avec prédiction **continue** (pas de limite à 3/6/12
mois) des futurs cycles, calculée à partir de la moyenne des cycles déjà
enregistrés.

## Fonctionnalités

- Calendrier continu, navigable mois par mois sans limite.
- Saisie manuelle du début et de la fin des règles, et de la date
  d'ovulation (si elle est connue autrement, par exemple test d'ovulation
  ou température).
- Prédiction automatique et réapprise à chaque nouvelle saisie :
  - longueur de cycle moyenne (sur les N derniers cycles, réglable),
  - durée moyenne des règles,
  - durée moyenne de la phase lutéale (utilisée pour estimer l'ovulation
    quand elle n'est pas saisie manuellement),
  - fenêtre de fertilité (5 jours avant l'ovulation + le jour même).
- Roue de cycle (vue radiale) indiquant la position du jour actuel dans
  le cycle.
- Statistiques : cycle moyen, durée des règles, régularité (écart-type
  des longueurs de cycle récentes), jours avant les prochaines règles.
- Journal des cycles passés, avec édition et suppression.
- Suivi optionnel du flux et de symptômes (fatigue, douleurs, humeur…).
- Export / import des données en JSON (sauvegarde manuelle, ou transfert
  vers un autre appareil).
- Installable comme application (PWA), fonctionne hors-ligne une fois
  ouverte une première fois.
- Mode sombre.

## Confidentialité — important

Il n'y a **pas de serveur ni de base de données**. Toutes les données
sont stockées uniquement dans le `localStorage` du navigateur qui a
ouvert l'application. Cela veut dire :

- Les données ne se synchronisent **pas** automatiquement entre
  appareils (ton téléphone et celui de ta copine, par exemple).
- Si le site est ouvert sur plusieurs appareils, utilisez le bouton
  **Exporter** sur un appareil puis **Importer** sur l'autre pour
  transférer les données.
- Vider le cache/les données du navigateur effacera les données. Pensez
  à exporter régulièrement une sauvegarde.
- GitHub Pages héberge uniquement les fichiers de l'application (le
  code), jamais les données personnelles saisies dedans.

Si un jour vous voulez une vraie synchronisation multi-appareils, il
faudrait ajouter un petit backend (par ex. Firebase, Supabase) — ce
n'est pas nécessaire pour un usage simple à deux.

## Déploiement sur GitHub Pages

1. Créez un nouveau dépôt GitHub, par exemple `lunaire`.
2. Déposez-y tous les fichiers de ce dossier en conservant la
   structure :
   ```
   lunaire/
   ├── index.html
   ├── style.css
   ├── app.js
   ├── manifest.webmanifest
   ├── sw.js
   ├── icons/
   │   ├── icon.svg
   │   ├── icon-192.png
   │   ├── icon-512.png
   │   └── icon-maskable-512.png
   └── README.md
   ```
3. Poussez sur la branche `main` :
   ```bash
   git init
   git add .
   git commit -m "Première version de Lunaire"
   git branch -M main
   git remote add origin https://github.com/<votre-utilisateur>/lunaire.git
   git push -u origin main
   ```
4. Sur GitHub : **Settings → Pages → Build and deployment → Source**,
   choisissez `Deploy from a branch`, branche `main`, dossier `/ (root)`.
5. Après une minute ou deux, l'application est disponible à l'adresse :
   `https://<votre-utilisateur>.github.io/lunaire/`
6. Sur un téléphone, ouvrez ce lien puis utilisez « Ajouter à l'écran
   d'accueil » (Safari) ou le menu d'installation (Chrome) pour
   l'installer comme une application.

## Comment fonctionne le calcul des prédictions

- La **longueur de cycle moyenne** est la moyenne des écarts entre les
  débuts de règles des derniers cycles enregistrés (réglable dans les
  réglages, 6 par défaut). Tant qu'il y a moins de deux cycles complets,
  une valeur par défaut (28 jours, modifiable) est utilisée.
- La **durée des règles** utilisée pour les prédictions futures est la
  moyenne des durées déjà observées (quand la date de fin a été saisie).
- La **phase lutéale** (temps entre l'ovulation et les règles suivantes)
  est en général plus stable que le reste du cycle. Elle est calculée
  à partir des cycles où une date d'ovulation a été saisie manuellement.
  Sans donnée, une valeur par défaut de 14 jours est utilisée.
- L'**ovulation prédite** d'un cycle futur = date de début des règles
  prédite de ce cycle − durée moyenne de la phase lutéale.
- La **fenêtre de fertilité** affichée va de 5 jours avant l'ovulation
  (estimée ou saisie) jusqu'au lendemain de l'ovulation.
- Chaque nouvelle saisie recalcule immédiatement toutes ces moyennes et
  redessine le calendrier — il n'y a pas de plafond de mois affichables,
  le calendrier génère les prédictions à la volée pour n'importe quel
  mois futur consulté.

⚠️ Ce sont des estimations statistiques basées sur l'historique fourni,
pas un outil médical ni un moyen de contraception fiable.

## Réglages disponibles

- Longueur de cycle par défaut (utilisée tant qu'il n'y a pas assez de
  données).
- Durée des règles par défaut.
- Durée de la phase lutéale par défaut.
- Nombre de cycles récents utilisés pour les moyennes glissantes.
- Mode sombre.

## Idées d'améliorations futures

- Rappels/notifications avant les prochaines règles ou la fenêtre
  fertile (nécessiterait des notifications push, donc un petit
  backend).
- Synchronisation multi-appareils.
- Graphique d'évolution de la longueur des cycles dans le temps.
- Suivi de la température basale ou de la glaire cervicale pour affiner
  la détection d'ovulation.
