# Calendrier de travail JFO

Calendrier public en consultation, avec administration réservée au compte Google **ygaltasy@gmail.com**.

## Hébergement

Le fichier `index.html` est une page statique compatible avec GitHub Pages. Dans GitHub : **Settings → Pages → Deploy from a branch → main / (root)**. URL prévue : `https://ygaltasy-design.github.io/calendrier-jfo/`.

## Configuration requise dans Firebase

1. Dans Firebase Authentication → Sign-in method, activer **Google**.
2. Dans Authentication → Settings → Authorized domains, ajouter `ygaltasy-design.github.io` (si pas déjà présent).
3. Dans Firestore → Rules, **fusionner** le contenu de `firestore-calendrier.snippet.rules` dans le `match /databases/{database}/documents` existant. Ne jamais remplacer les autres règles par ce seul extrait.
4. Tester : visiteur anonyme peut consulter `/jfo_calendar/v1/plan`; compte Google connecté peut soumettre une demande ; seul `ygaltasy@gmail.com` peut créer et modifier les tâches ou prendre une décision.

Le projet Firebase ciblé est `gestionpax-d9f5d`. La configuration du SDK Web est publique par conception et ne contient **aucune** clé privée d'administration.

## Structure Firestore

- `jfo_calendar/v1/plan`: tâches du programme, visibles publiquement.
- `jfo_calendar/v1/progress`: avancement, visible publiquement et modifiable par les membres connectés.
- `jfo_calendar/v1/requests`: demandes, visibles par les membres connectés.
- `jfo_calendar/v1/decisions`: décisions réservées au Chef de Programme.
- `jfo_calendar/v1/log`: journal consultable par les membres connectés.

**Attention :** les données précédemment enregistrées dans l'environnement Claude ne migrent pas automatiquement vers Firestore. Export ou ressaisie nécessaire pour les conserver.

**Attention :** le calendrier n'aura pas d'écritures opérationnelles tant que les règles Firestore n'auront pas été intégrées et publiées. Toute règle globale déjà permissive doit aussi être examinée, car les règles Firestore sont additives.
