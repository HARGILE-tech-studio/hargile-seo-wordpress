# HARGILE SEO pour WordPress

Extension WordPress qui ouvre à l'API REST le titre et la description SEO
(The SEO Framework, Yoast, Rank Math) de chaque type de contenu public, pour
que le pilote HARGILE puisse les écrire et les relire. L'écriture exige
toujours un mot de passe d'application d'un compte qui peut modifier le
contenu visé.

## Installer

Télécharger `hargile-seo.zip` depuis la
[dernière version](https://github.com/HARGILE-tech-studio/hargile-seo-wordpress/releases/latest),
puis dans l'admin WordPress : Extensions, Ajouter, Téléverser une extension,
Activer.

Une fois installée, elle se met à jour comme les autres extensions
(WordPress 5.8 et plus).

## Vérifier

Dans l'admin : Extensions, ligne « HARGILE SEO ». Sans se connecter,
`https://<site>/wp-json/hargile/v1/version` répond 401 si elle est active,
404 sinon.

## Intégrité des releases

### Vérifier un zip à la main

Dans un dossier vide, télécharger `hargile-seo.zip`, `hargile-seo.zip.sha256`
et `info.json` depuis la page de la version, puis :

```sh
sha256sum -c hargile-seo.zip.sha256
```

La commande doit répondre `hargile-seo.zip: OK`. Comparer ensuite avec
`info.json` : le champ `sha256` doit être identique à l'empreinte du zip
(`sha256sum hargile-seo.zip`) et le champ `package` doit commencer par
`https://github.com/HARGILE-tech-studio/hargile-seo-wordpress/releases/download/`.

### Ce que vérifie l'extension

Avant d'installer une mise à jour, l'extension exige dans `info.json` un champ
`sha256` et une URL de téléchargement (`package`) qui commence par le préfixe
ci-dessus. Elle calcule le sha256 du zip téléchargé et le compare à `sha256`.
Si le champ manque, si l'URL sort du dépôt ou si l'empreinte diffère, la mise
à jour est refusée.

Limite : `info.json` et le zip viennent du même dépôt. Ce contrôle protège
contre un téléchargement corrompu ou un zip remplacé seul, pas contre un
compte publieur compromis qui changerait les deux. La signature (ci-dessous)
couvrira ce cas.

Le workflow `verify-release.yml` refait ces contrôles à chaque publication
(lecture seule) : format du tag, zip contre `.sha256`, zip contre `info.json`,
préfixe de l'URL.

### Publier une version

- Seul `publier.sh` du dépôt privé `crm` publie, depuis `main`, avec un tag
  `vX.Y.Z`. Il publie le zip, `info.json` (avec `sha256`) et l'asset
  `hargile-seo.zip.sha256`.
- Pas de dépôt de fichier à la main sur une release, pas de publication depuis
  un poste hors de ce script.
- Un tag qui ne respecte pas `vX.Y.Z` est rejeté par le workflow.

### Prévu

- Signature ed25519 de `info.json` et du zip, clé publique embarquée dans
  l'extension.
- Attestation de provenance de la build (`actions/attest-build-provenance`).

Ce dépôt ne porte que les versions publiées. Le code source est maintenu par
HARGILE et publié ici à chaque version.
