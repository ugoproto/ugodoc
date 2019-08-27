Prenons un répertoire avec plusieurs fichiers, dont le fichier `ajout.md`

# Explorer

- Compter les mots: `wc -w ajout.md`
- Compter les lignes: `wc -l ajout.md`
- Compter les caractères: `wc -c ajout.md`
- Compter plusieurs fichiers (ou une liste de fichiers): `wc -w *.md`
- Envoyer les résultats dans un dossier/fichier (tsv, txt, csv): `wc -w *.md > r.txt`

# Rechercher (regex)

- Trouver un patron (sensible à la casse): `grep git *.md`
- Compter un patron (sensible à la casse): `grep -c git *.md`
- Trouver un patron (insensible à la casse): `grep -i git *.md`
- Compter un patron (insensible à la casse): `grep -ci git *.md`
- Trouver un patron et le numéro de la ligne: `grep -n git *.md`
- Trouver une/des chaines de caractères dans un fichier (une source de chaine de caractères sous forme de liste) (et le numéro de la ligne): `fgrep -f -n source *.md`

`grep` et `fgrep` fonctionnent sur une chaine complète (un mot), mais non sur un chaine dans une chaine (quelques caractères dans un mot).
`egrep` (ou l'option `-E`) fonctionne sur un chaine dans une chaine (quelques caractères dans un mot).

## Travailler avec les regex

- Trouver un patron étendu: `grep -E -n "(G|g)it" *.md, egrep -n "(G|g)it" *.md`
- Trouver des cas avec apostrophes: `egrep --color "' " *.md`
- Trouver des cas avec trois voyelles: `grep --color "[aeiou]{3}" *.md`
- Trouver des cas: `egrep --color "(J|j)e (veux|voulais|voudrais|voudrai|veuille)" *.md`

## Sommaire des options

- `-n` (numéro de la ligne)
- `-f` (fichier source ou fold pour convertir la casse)
- `-v` (inverser la recherche)
- `-w` (mots précis)
- `--color` (colorer)

Exemple: `fgrep -v -w -f source *.md`

# Lire, afficher

- Consulter les métadonnées du fichier: `file ajout.md`
- Lire le fichier: `head ajout.md`, `tail ajout.md`, `less ajout.md` (Q), `cat ajout.md`
- Trier un fichier: `sort fichier.md`
- Filtrer les valeurs uniques: `uniq fichier.md`
- Combiner avec des tubes: `sort fichier | uniq | head > résultat.txt`

# Télécharger

- Télécharger un fichier: `wget url`
