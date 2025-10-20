<div lang="fr">

# Le Management du Version pour XIOS

## Numérotation des Versions

XIOS vise à mettre en œuvre le versioning sémantique (https://semver.org/lang/fr/spec/v2.0.0.html) pour les versions et la numérotation des versions de XIOS.

Étant donné un numéro de version MAJEUR.MINEUR.CORRECTIF, il faut incrémenter :

1. le numéro de version MAJEUR quand il y a des changements non rétrocompatibles,
1. le numéro de version MINEUR quand il y a des ajouts de fonctionnalités rétrocompatibles,
1. le numéro de version de CORRECTIF quand il y a des corrections d’anomalies rétrocompatibles.

Des libellés supplémentaires peuvent être ajoutés pour les versions de pré-livraison et pour des méta-données de construction sous forme d’extension du format MAJEURE.MINEURE.CORRECTIF.

Pour XIOS, la gestion sémantique des versions est basée sur l’intention et une interprétation pragmatique. Les modifications majeures, mineures et de correctifs doivent être conformes à Les utilisateurs doivent être conscients que des changements subtils de comportement peuvent se produire entre les versions mineures et les versions majeures.

Le versioning sémantique

> Pour que ce système fonctionne, vous devez d’abord déclarer une API publique. Il peut s’agir d’un document ou de règles imposées par le code lui-même.
> Quoi qu’il en soit, il est important que cette API soit claire et précise. Une fois celle-ci prête,
> vous communiquez ses modifications par des incrémentations successives de son numéro de version. 

## Étiquetage de Version

Les étiquettes de version sont immuables. Ils font état d’une révision fixe du code.
Une fois qu’une version est étiquetée, aucune modification ne doit être apportée à cette version, il s’agit d’une version.

### Branches de publié

Pour chaque cible de version mineure, une nouvelle branche doit être créée avec le dépôt. Une fois cette branche créée, aucune nouvelle fonctionnalité ne doit être ajoutée à la branche. Seules les corrections de bogues rétrocompatibles peuvent être ajoutées à la branche.

Par exemple, une nouvelle branche peut être créée pour une version `vn3.1.x` release: `XIOS3/branches/xios-3.1`. La création de cette branche gèlera l’ensemble des fonctionnalités incluses dans toutes les versions de `vn3.1.x`.

Des étiquettes de publié doivent être apposées à l’égard d’une branche de déblaiement.

### Git Tag


### Étiquetage Futur

Tout changement futur du système de contrôle de version doit préserver les chaînes d’étiquettes de version de la subversion, et fournir un mécanisme pour obtenir des versions explicites en utilisant les chaînes d’étiquettes comme clés.

## Candidates de Version

optional

Les candidates de version sont des versions immuables, qui sont utilisées à des fins d’évaluation. L’étiquette du candidates de version doit comporter le suffixe `.rc` suivi d’un numéro à un chiffre.

Ainsi, 'vn3.1.1.rc1' représente une candidate de version pour une future version 'vn3.1.1'
Une candidate de version doit être mise à disposition pendant au moins 1 mois civil pour permettre aux utilisateurs de XIOS de tester et de rendre compte de l’adéquation de la version candidate pour être une version officielle.

Les candidates de version peuvent entraîner des corrections de bogues sur la branche de publication, avant une publication.

Si des modifications importantes sont apportées, une nouvelle version candidate doit être envisagée pour les tests avant une publication.

</div>

<div lang="en">

# Release Management for XIOS

## Version Numbering

XIOS aims to implement semantic versioning (https://semver.org/spec/v2.0.0.html) for releases and version numbering of XIOS.

This means that, given a version number MAJOR.MINOR.PATCH, increment the:

1. MAJOR version when you make incompatible API changes
1. MINOR version when you add functionality in a backward compatible manner
1. PATCH version when you make backward compatible bug fixes

Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

For XIOS, Semantic versioning is based on intent and a pragmatic interpretation.  The major, minor and patch changes should conform to 
the expectations set above, users need to be aware that subtle changes in behaviour can occur between minor versions as well as major versions.

Semantic versioning defines backwards compatibility with respect to the API:

> For this system to work, you first need to declare a public API. This may consist of documentation or be enforced by the code itself.
> Regardless, it is important that this API be clear and precise. Once you identify your public API,
> you communicate changes to it with specific increments to your version number.

So, a backwards compatible change is one that preserves the API that users use, it does not break code by making it unable to run.
It does not guarantee identical behaviour, a new minor release may include a fix to the behaviour of an existing API call.
All that is being asserted is that code that ran using the API will not fail due to an unknown function, argument, XML configuration.

## Release Labelling

Release (or version) Labels are immutable.  They point to a fixed revision of the code.
Once a version is labelled, no change shall be made to that version, it is a release.

### Release Branches

For each minor version target, a new branch shall be created with the `upstream` repository.  Once this branch has been created, no new functionality shall be added to the branch.  
Only backward compatible bug fixes may be added to the branch.

For example, a new branch may be created for the `vn3.1.x ` release set: `XIOS-3.1`.  The creation of this branch shall freeze the feature set that is included in all `vn3.1.x` releases.

Release tags shall be made with respect to a release branch.

### Git Tagging

Each release shall be a Git tag and a Gitlab release.

### Release Candidates

A release vandidate is an optional tag, releases may not have a release candidate before the full release is tagged.  This protocol element is adopted only when deemed necessary by the development team.

Release candidates are immutable releases, that are used for evaluation purposes.  The release candidate label shall include the suffix `.rc` plus a single digit number.

Thus `vn3.1.1.rc1` represent a release candidate for a future `vn3.1.1` release

A release candidate may be made available for a minimum of 1 calendar month to enable users of XIOS to test and report back on the suitability of the release candidate to be a formal release.
Release candidates may lead to bug fixes on the release branch, prior to a release.
If significant changes are made, a new release candidate should be considered for testing prior to a release.

</div>
