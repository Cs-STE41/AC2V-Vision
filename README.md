# AC2V Vision

Application web pour reconnaître le logo d’une marque de matériel agricole (caméra du téléphone, dans Chrome) et ouvrir la fiche de formation correspondante : vidéos de guidage et, pour John Deere, un livret de prise en main.

La page est servie par GitHub Pages : https://cs-ste41.github.io/AC2V-Vision/

## Structure

- `index.html` — page principale (caméra, reconnaissance, confirmation Oui / Non)
- `fiches/` — une fiche par marque, plus la feuille de style commune `style.css`
- `model/` — modèle Teachable Machine (`model.json`, `metadata.json`, `weights.bin`)
- `docs/tutoriel.html` — guide d’utilisation pas à pas
- `docs/livret-prise-en-main-john-deere.pdf` — livret John Deere (consoles G4 et G5)

Les classes du modèle doivent correspondre **exactement** aux clés du catalogue dans `index.html` : Fendt, SDF, John Deere, Massey Ferguson, Valtra, Case IH, Claas, New Holland, et `Autre - inconnu`.

## Mettre à jour une fiche

1. Ouvre le fichier de la marque dans `fiches/` (par exemple `fiches/fendt.html`).
2. Ajoute ou corrige les liens (vidéos, PDF). Les titres des vidéos restent en français, sur le même modèle que les fiches existantes.
3. Laisse le lien « Retour à la reconnaissance » vers `../index.html`, et la feuille de style `style.css` dans le même dossier.
4. Si tu ajoutes un document (PDF, etc.), place-le dans `docs/` et pointe vers `../docs/nom-du-fichier.pdf`.

## Mettre à jour le modèle

1. Entraîne un modèle image dans Teachable Machine, avec les mêmes noms de classes que ci-dessus.
2. Exporte le modèle (fichiers `model.json`, `metadata.json`, `weights.bin`).
3. Remplace les trois fichiers dans le dossier `model/` (ne les place pas à la racine du dépôt).
4. Vérifie que `MODEL_URL` dans `index.html` vaut bien `model/`.
5. Teste la page en local (un petit serveur HTTP suffit, par exemple `python3 -m http.server`) avant de pousser les changements.

Le modèle actuel a été entraîné à partir d’un petit nombre d’images de logos : la reconnaissance sur un vrai tracteur s’améliorera avec de nouvelles photos (30 à 50 par marque, angles et lumières variés).
