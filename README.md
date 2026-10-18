# Fragrance du Bois — France Creator Intelligence

Dashboard statique pour une campagne de gifting France, coordonnée par Eaux Rares. Prototype indépendant du projet Eaux Rares OS.

## Déploiement Netlify

1. Netlify → **Add new project** → **Import an existing project** → **GitHub**.
2. Choisir `frederic75020/fdb-france-creator-intelligence`.
3. Build command : **laisser vide**. Publish directory : **.** (racine).
4. Déployer. Le fichier `netlify.toml` contient déjà la configuration nécessaire.

## Données et limites

- `data/creators.json` contient 13 créateurs et leurs campagnes ; aucun e-mail, numéro de téléphone ou adresse postale.
- Instagram : 12 audiences extraites avec Apify au **18 octobre 2026**, et 1 compte indisponible (Marc @lecarnet__).
- TikTok : comptes et 10 audiences de la liste de travail ; **non vérifiés par Apify**. Aucune valeur inventée pour Gwendal, Nolwenn ou Antoine (Antoine n'a pas de TikTok).
- 10 créateurs Forbidden Plum sont **en attente d'approbation**. Date de réception souhaitée : **30 octobre 2026**.
- Gwendal, Nolwenn et Antoine ont un gifting **validé en amont par James et/ou Yann**, sans expédition confirmée.
- Le dashboard est **en lecture seule**. Il ne modifie pas les approbations ni les envois.
- Pas de synchronisation Apify automatique actuellement : les données sont un export daté.
- Les totaux Instagram + TikTok sont des sommes d'abonnés et non des personnes uniques.

## Architecture

Site HTML/CSS/JS sans dépendance ni étape de compilation, facilement déployable sur Netlify. Chargement du fichier `data/creators.json` côté navigateur.

Pour une phase 2 : base Supabase avec rôles, interface d'administration authentifiée, Netlify Functions pour synchroniser Apify avec un jeton stocké en variable secrète, journal des extractions et suivis des expéditions. **Ne jamais ajouter de coordonnées privées ou de clés API à ce dépôt ni à des fichiers distribués publiquement.**

## Interface tablette/mobile et annotations (18 octobre 2026)

Le tableau bascule en fiches sur mobile et les graphiques se réorganisent sur tablette. Chaque profil comporte désormais une note éditable et une liste de commentaires horodatés. **Attention :** ces annotations sont enregistrées uniquement via `localStorage` dans le navigateur courant ; elles ne sont ni partagées, ni sauvegardées sur un serveur, et peuvent disparaître lors du nettoyage des données du navigateur. Ne pas y stocker de coordonnées privées ou d'informations sensibles. Pour un workflow collaboratif, une base authentifiée est nécessaire.

Le connecteur Apify mis à disposition pour cette session expose uniquement `apify/instagram-scraper` : aucune donnée TikTok ne peut être présentée comme vérifiée. Il faut configurer un acteur TikTok approprié et son accès avant de remplacer les valeurs déclaratives.
