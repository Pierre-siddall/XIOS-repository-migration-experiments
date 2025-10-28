<div lang="fr">

# Le Management du Version pour XIOS

## Numérotation des Versions

XIOS vise à utiliser le versionnage sémantique (https://semver.org/lang/fr/spec/v2.0.0.html) pour la numérotation actuelle et préceédente des versions de XIOS.

Étant donné un numéro de version MAJEUR.MINEUR.CORRECTIF, il faut incrémenter :

1. le numéro de version MAJEUR quand il y a des changements non rétrocompatibles,
2. le numéro de version MINEUR quand des fonctionnalités rétrocompatibles ont été ajoutés,
3. le numéro de version de CORRECTIF quand il y a des corrections d’anomalies rétrocompatibles.

Des tags supplémentaires peuvent être ajoutés pour les versions de pré-version et pour les méta-données de construction sont disponible avec une extension du format MAJEURE.MINEURE.CORRECTIF.

Pour XIOS, la gestion sémantique des versions est basée sur une intention et interprétation pragmatique. Les modifications majeures, mineures et de correctifs doivent être conformes à le susmentionné guide. Les utilisateurs doivent être conscients que des changements subtils de comportement peuvent se produire entre les versions mineures et majeures.

Le versionnage sémantique est définé comme la rétrocompatibilitié par rapport à l'API:

> Pour que ce système fonctionne, vous devez d’abord déclarer une API publique. Il peut s’agir d’un document ou de règles imposées par le code.
> c'est important que cette API soit claire et précise. Quand le API publique est identifié.
> vous devez communiquez ses modifications par des incrémentations successives du numéro de version.

## Étiquetage de Version

Les tags de version sont immuables. Ils se lient à une révision fixe du code.
Une fois qu’une version est tagué, aucune modification doit être ajouté à cette version. C'est une nouvelle version.

### Branches de publié

Pour chaque branche ciblé vers une version mineure, la nouvelle branche doit être créée avec le dépôt 'upstream'. Une fois cette branche est créée, aucune fonctionnalité nouvelle doit être ajoutée à la branche, sauf les corrections des bugs rétrocompatibles.

Par exemple, une nouvelle branche peut être créée pour une version `vn3.1.x` release: `XIOS3/branches/xios-3.1`. La création de cette branche fige l'ensemble des fonctionnalités incluses dans toutes les versions de `vn3.1.x`.

Des tags de publication doivent être déposées relativement à la branche de la nouvelle version.

### Git Tag


### Étiquetage Futur

Tout changement futur du système de contrôle de version doit préserver les chaînes d’étiquettes de version de la subversion, et fournir un mécanisme pour obtenir des versions explicites en utilisant les chaînes d’étiquettes comme des clés.

## Candidates de Version


Les candidates de version sont des versions facultative et ne peux pas être ajouté avant que la nouvelle version est lancer. Cette element protocole est adopté seulement quand jugé nécessaire par l'equipe de dévelopment.

les candidates de version sont des versions immuable, qui sont utilisés pour l'évaluation. Les tags de candidates de version doivent comporter le suffixe `.rc` suivi par un seul chiffre.

Ainsi, 'vn3.1.1.rc1' représente une candidate de version pour une version future 'vn3.1.1'
Une candidate de version doit être mise à disposition pendant au moins 1 mois pour permettre aux utilisateurs de XIOS de tester et de rendre compte de l’adéquation de la version candidate pour être une version officielle.

Les candidates de version peuvent entraîner des corrections de bugs sur la branche de publication, avant une publication.

Si des modifications importantes sont ajouté, une nouvelle version candidate doit être considérer pour les tests avant une publication.

</div>

<div lang="en">

# Release Management for XIOS

## Version Numbering

XIOS aims to implement semantic versioning (https://semver.org/spec/v2.0.0.html) for the current and previous version numbering of XIOS.

This means that, given a version number MAJOR.MINOR.PATCH, increment the:

1. MAJOR version when you make incompatible API changes
2. MINOR version when you add functionality in a backward compatible manner
3. PATCH version when you make backward compatible bug fixes

Additional tags for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

For XIOS, Semantic versioning is based on intent and a pragmatic interpretation.  The major, minor and patch changes should conform to
the aforementioned guide. The users need to be aware that subtle changes in behaviour can occur between the minor and major versions.

Semantic versioning defines backwards compatibility with respect to the API:

> For this system to work, you first need to declare a public API. This may consist of documentation or be enforced by the code.
> It is important that this API be clear and precise. When the public API is identified,
> you must communicate changes to it with specific increments to your version number.

So, a backwards compatible change is one that preserves the API that users use, it does not break code by making it unable to run.
It does not guarantee identical behaviour, a new minor release may include a fix to the behaviour of an existing API call.
All that is being asserted is that code that ran using the API will not fail due to an unknown function, argument, XML configuration.

## Release Labelling

Release (or version) tags are immutable.  They link to a fixed revision of the code.
Once a version is tagged, no changes shall be added to that version, it is a release.

### Release Branches

For each branch targeted towards a minor version, the new branch shall be created with the `upstream` repository.  Once this branch has been created, no new functionality shall be added to the branch.
Only backward compatible bug fixes may be added to the branch.

For example, a new branch may be created for the `vn3.1.x ` release set: `XIOS-3.1`.  The creation of this branch shall freeze the feature set that is included in all `vn3.1.x` releases.

Release tags shall be made with respect to a release branch.

### Git Tagging

Each release shall be a Git tag and a Gitlab release.

### Release Candidates

A release candidate is an optional tag, releases may not have a release candidate before the full release is tagged.  This protocol element is adopted only when deemed necessary by the development team.

Release candidates are immutable releases, which are used for evaluation purposes.  The release candidate label shall include the suffix `.rc` plus a single digit number.

Thus `vn3.1.1.rc1` represent a release candidate for a future `vn3.1.1` release

A release candidate may be made available for a minimum of 1 month to enable users of XIOS to test and report back on the suitability of the release candidate to be a formal release.
Release candidates may lead to bug fixes on the release branch, prior to a release.
If significant changes are made, a new release candidate should be considered for testing prior to a release.

</div>
