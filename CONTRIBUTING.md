<div lang="fr">

# Guide de contribution pour le développement de XIOS

## Suivi des problèmes

Toute activité de développement doit être associée à un Ticket.
Il s’agit d’un ticket trac sur https://forge.ipsl.fr/ioserver.

Les informations doivent comprendre :
* une description du problème abordé,
* un lien vers la branche,
* des éléments de test.

## Principes de Conception et Revue

XIOS vise à être un serveur d’entrée-sortie générique pour les simulations. XIOS essaie d’éviter l’intégrartion de code spécifique à un modèle dans son implémentation. Les fonctionnalités doivent être universelles et implémentées au regard de la variété des spécificités des modèles addressables par XIOS.

Les nouvelles fonctionnalités doivent être proposées à XIOS à l’aide d’un ticket de revue de conception. Cela permet d’adresser à la fois l’enjeu général et l'objectif de l'implémentation, ainsi que de discuter des principes de conception avant de proposer des modifications détaillées du code.

Un ticket de revue de conception doit inclure :
* une déclaration du résultat souhaité ;
* une description du contexte et de la plus value-value visés ;
* une proposition sur la manière dont cela pourrait être mis en œuvre dans la base de code XIOS ;
* une proposition sur la manière dont l’interface utilisateur pourrait être mise en œuvre :
    * pour répondre aux besoins spécifiques de la demande en étant extensible et généraliste ;
* comment la nouvelle fonctionnalité peut être testée ;
* une évaluation initiale des risques sur les capacités existante de la base du code.

Les petites fonctionnalités et les corrections de bugs peuvent contourner cette étape de révision de conception, si l’équipe de développement de XIOS l’accepte.

## Versions Majeures

XIOS3 est la version majeure actuelle du développement.

XIOS2 est une version stable incompatible avec les versions antérieures.
XIOS2 est encore largement utilisé dans certaines simulations, mais ne fait plus l'objet de développement propre.

Les arbres sources de ces versions sont divergents, une gestion de l'organisation des développements futurs est nécessaire.

### Règles pour le Développement de la Version Majeure

1. Les corrections de bugs peuvent s’appliquer :
    * au trunk de XIOS3 uniquement :
        * il s’agit de l’approche par défaut ;
    * au trunk de XIOS2 et le trunk de XIOS3 :
        * s’il est démontré que le bug pose des problèmes aux utilisateurs de XIOS2 ;
        * dans ce cas, créez deux branches liées à un ticket, pour gérer la correction du bug.
    * au trunk de XIOS2 uniquement, si cela n’a aucun rapport avec XIOS3 :
        * s’il est démontré que le bug cause des problèmes aux utilisateurs de XIOS2 et qu’il n’est pas évident dans XIOS3.
    * à une branche de version spécifique (alors ciblée par le ticket) :
        * seule la dernière version doit être ciblée pour une correction de bug :
            * à moins qu’un cas spécifique ne soit présenté et agréé dans un ticket pour expliquer pourquoi une branche plus ancienne devrait également être incluse ;
        * une correction de bug de branche de publication doit toujours être considérée pour être proposée aux trunks XIOS2 et XIOS3 :
            * bien que les tests puissent montrer que cela n’est pas nécessaire (par exemple, déjà résolu sur le trunk).
2. Nouvelles fonctionnalités
    * De nouvelles fonctionnalités peuvent être proposées au trunk de XIOS3 uniquement :
        * C’est la position par défaut pour l’effort de développement ;
        * il est reconnu que la plupart des nouvelles fonctionnalités ne seront pas disponibles dans XIOS2.
    * De nouvelles fonctionnalités peuvent être proposées au trunk de XIOS3, avec un portage vers le trunk do XIOS2 :
        * c’est un cas inhabituel, on s’attend à ce que de nouvelles fonctionnalités ne soient pas ajoutées à XIOS2 ;
        * si la fonctionnalité est examinée et évaluée comme appropriée pour le développement associé, elle peut cibler XIOS2 et XIOS3, par exception ;
        * deux branches liées ciblant XIOS2 et XIOS3 sont prévues, associées à un seul ticket.
    * Les nouvelles fonctionnalités ne peuvent pas être appliquées uniquement à XIOS2 :
        * XIOS2 n’est pas développé indépendamment de XIOS3.

## Revue et Intégration 

Les propositions de code doivent être examinées, par un ou plusieurs relecteurs de code, avec des commentaires ajoutés au ticket et des mises à jour de la branche, jusqu’à ce que le ou les relecteurs soient satisfaits.

L'intégration du contenu de la branche sur le(s) trunk(s) doit être entreprise par l’un des développeurs principaux de XIOS.

## Interactions Subversion pour les développeurs
```
export uname={myuname}
# pour consulter le trunk à partir de IPSL XIOS3:
svn co svn+ssh://$uname@forge.ipsl.jussieu.fr/ipsl/forge/projets/ioserver/svn/XIOS3/trunk

# pour créer un répertoire spécifique au développeur pour héberger les branches soumises par ce développeur
svn mkdir svn+ssh://$uname@forge.ipsl.jussieu.fr/ipsl/forge/projets/ioserver/svn/XIOS3/dev/$uname -m 'dev branches for $uname'
# notez que cela n’est nécessaire qu’une seule fois, puis le répertoire est disponible pour une utilisation ultérieure

# workflow de développement standard pour travailler sur une activité:
export abranch={Nom-de-l’œuvre}
svn copy svn+ssh://$uname@forge.ipsl.jussieu.fr/ipsl/forge/projets/ioserver/svn/XIOS3/trunk svn+ssh://$uname@forge.ipsl.jussieu.fr/ipsl/forge/projets/ioserver/svn/XIOS3/dev/$uname/$abranch -m 'create branch for minor build change'
svn co svn+ssh://$uname@forge.ipsl.jussieu.fr/ipsl/forge/projets/ioserver/svn/XIOS3/dev/$uname/$abranch
cd $abranch
# développement ... ...
svn commit
```

</div>

<div lang="en">
   
# Contributing Guide for XIOS development

## Git Code Maintenance

* All development activity shall be pushed to a personal fork of the project.
* Development shall only be included into this https://gitlab.in2p3.fr/ipsl/projets/xios project via `merge request`.

The https://gitlab.in2p3.fr/ipsl/projets/xios project is referred to as `upstream` in this guide.

### Simple Git Workflow

It is assumed that you have a local git repository where `origin` is your https://gitlab.in2p3.fr fork
and `upstream` is https://gitlab.in2p3.fr/ipsl/projets/xios.

This work flow is for proposing changes to `main`, currently `XIOS3`.

1. `git fetch origin`
1. `git checkout -b {new-branch-name} upstream/main`
1. < development activity >
1. < local testing >
1. `git commit`
1. `git push origin {new-branch-name}`
1. raise new `merge request` on `gitlab.in2p3.fr`
  * This should trigger the CI testing for the `merge request`

Further Git work flows are possible for making changes to release branches and older versions of XIOS
and for managing more complicated changes.

### Feature Branches

For large scale changes that require coherent adoption, then a developer may choose to create a
`Feature Branch` within their fork.

This branch can be contributed to by one or numerous developers.
Parts of the full feature may be reviewed and adopted into the feature branch by
`Merge Request`s within the lead developers fork.

Once Ready then the `Feature Branch` may be proposed to the `upstream` code base, with links to
all of the intermediate `Merge Request` reviews.

This work flow can significantly help to manage larger and more invasive changes to the code base.
For many development activities then it is not required and the simple work flow is fine.

## Issue tracking

### Merge Request

Any development activity targeting the `upstream` shall be associated with a `Merge Request` to `upstream`.

### Issue Tracking

https://gitlab.in2p3.fr/ipsl/projets/xios is an open issue tracker for XIOS development.

Merge Requests may link to Issues, and may explicitly close Issues or simply contribute to them.

It is not essential to have an Issue and a Merge Request for small changes, but for larger changes or Issues without solution, then an Issue is useful to manage awareness and work.  this is particularly the case when designing new features.

### Design Principles & design Review

XIOS aims to be a generally applicable Input Output Server for simulations. XIOS tries to avoid embedding 
model specific code within it's implementation. Features should be generally useful and implemented such
that models provide their own customisations through model configuration of XIOS.

New features should be proposed to XIOS using a design review ticket. This enables the general target and
the implementation targets to be explored and the design principles discussed prior to the proposal
of detailed code changes.

A design review ticket shall include:
* a statement of desired outcome;
* a description of the context and value being targeted;
* a proposal on how this could be implemented within the XIOS code base;
* a proposal on how the user interface could be implemented:
    * to meet the specific needs of the propser and to be extensible and useful generally;
* how the new feature can be tested;
* an initial assessment of risks to existing areas of the code base.

Small features and bug fixes may bypass this design review stage, if agreed by the XIOS development team.
It is fine to raise a `Merge Request` if you feel that the work is small.  If XIOS developers would
appreciate a design review Issue for the work, then we will tell you.

## Major Version Targeting

XIOS3 is the current major development version.

XIOS2 is a backwards incompatible stable version.
XIOS2 is still in broad use in some simulations, but is not undergoing further development.

The source trees for these major versions are divergent, so management is needed for development targeting.

### Major Version Development Rules

1. Bug fixes may apply to:
    * XIOS3 `main` only:
        * this is the default approach;
    * `XIOS2` branch & XIOS3 `main`:
        * if the bug is demonstrated to be causing problems for users of XIOS2;
        * in this case, create two branches linked to one ticket, to manage the bug fix.
    * `XIOS2` branch only, if this has no bearing on XIOS3 `main`:
        * if the bug is demonstrated to be causing problems for users of XIOS2 and shown to be not evident in XIOS3.
    * a specific release branch may also be targeted by a ticket:
        * only the latest release should be targeted for a bug fix:
            * unless a specific case is made and agreed on a ticket for why one further older release branch should be included as well;
        * a release branch bug fix shall always be considered for proposal to `main` XIOS3:
            * though testing may show that this is not required (e.g. already resolved on `main`).
1. New Features
    * New features may be proposed to XIOS3 only:
        * this is the default position for development effort;
        * it is recognised that most new features shall not be available in XIOS2.
    * New features may be proposed to XIOS3, with a back port to XIOS2:
        * this is an unusual case, the expectation is that new features are not added to XIOS2;
        * if the feature is reviewed and assessed as appropriate for linked development, it may target XIOS2 and XIOS3, by exception;
        * two linked branches targeting XIOS2 & XIOS3 are provided, linked to one ticket. 
    * New features may not be applied to XIOS2 only:
        * XIOS2 is not being developed independent of XIOS3.

## Review & Merge

Code proposals shall be reviewed, by one of more code reviewers, with comments added to the `Merge Request`
and updates to the branch, until the reviewer(s) are content.

Reviewers shall use the `Review` section to request changes or indicate that they are content.

Merge of merge request branch content onto an upstream branch  shall be undertaken by one the the XIOS core developers.


</div>
