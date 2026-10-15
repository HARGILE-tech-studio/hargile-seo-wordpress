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

Ce dépôt ne porte que les versions publiées. Le code source est maintenu par
HARGILE et publié ici à chaque version.
