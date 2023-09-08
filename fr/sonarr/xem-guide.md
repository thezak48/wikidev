---
title: Guide de modération de TheXEM
description: Guide pour mapper différents scénarios dans XEM pour une utilisation optimale avec Sonarr et d'autres logiciels PVR.
published: true
date: 2021-11-24T19:26:31.972Z
tags: sonarr, xem
editor: markdown
dateCreated: 2021-10-03T16:48:28.241Z
---

# Table des matières

- [Table des matières](#table-des-matières)
- [Guide de modération de TheXEM](#guide-de-modération-de-thexem)
- [Nomination](#nomination)
- [Les différents types d'entités](#les-différents-types-dentités)
- [Types de mappage](#types-de-mappage)
  - [Mappage !SxxExx](#mappage-sxxexx)
  - [Mappage absolu](#mappage-absolu)
  - [Mappage complet](#mappage-complet)
  - [Mappage direct](#mappage-direct)
- [Exemples](#exemples)
  - [Mappage basique d'anime](#mappage-basique-danime)
  - [Mappage complexe d'anime](#mappage-complexe-danime)
  - [Émissions de dessins animés occidentaux au format court](#émissions-de-dessins-animés-occidentaux-au-format-court)
  - [Mappage individuel complexe](#mappage-individuel-complexe)
- [Limitations](#limitations)
  - [Un seul schéma de numérotation de scène par série est pris en charge](#un-seul-schéma-de-numérotation-de-scène-par-série-est-pris-en-charge)
  - [Un seul entité principale est prise en charge](#un-seul-entité-principale-est-prise-en-charge)
  - [Suppression de la colonne principale ou des saisons individuelles](#suppression-de-la-colonne-principale-ou-des-saisons-individuelles)
  - [Certaines choses ne peuvent tout simplement pas être mappées](#certaines-choses-ne-peuvent-tout-simplement-pas-être-mappées)
- [Besoin d'aide ?](#besoin-daide)

# Guide de modération de TheXEM

[TheXEM](https://thexem.info) est un service qui permet de faire le lien entre d'autres services/entités qui utilisent différents schémas de numérotation et de nomination pour les sorties de séries TV. Sonarr utilise TVDB comme source de données pour ses informations sur les épisodes et parfois les groupes de sortie et autres scènes utilisent un schéma de nomination ou de numérotation différent. Grâce à un mappage approprié, il est possible de s'assurer que l'épisode 1 de la saison 1 selon TVDB correspond à l'épisode 5 de la saison 1 selon la scène, de sorte que Sonarr puisse télécharger le bon épisode malgré la différence de numérotation.

Ce guide s'adresse aux personnes disposant d'un compte sur TheXEM et vous guidera à travers certains des modèles les plus courants que vous voudrez peut-être utiliser. Mais d'abord, nous vous expliquerons les bases.

# Nomination

Par convention, nous utilisons le même nom que celui utilisé par The TVDB pour la série elle-même. Cela est particulièrement intéressant pour les émissions internationales telles que les animes et se résume essentiellement à utiliser le nom officiel en anglais de l'émission sous licence.

Il est également possible d'entrer différents alias pour le nom de la série, ce qui est principalement utilisé pour les animes, mais occasionnellement utile pour les émissions "classiques" également.

# Les différents types d'entités

TheXEM dispose de quatre types d'entités ou sources de données différentes qu'il prend actuellement en charge et peut connecter les unes aux autres au besoin. Ces quatre types sont :

- Scène
- [TVDB](https://thetvdb.com)
- [AniDB](https://anidb.net)
- Principale

Un mappage XEM approprié pour une émission particulière devrait *au moins* comporter une entrée dans la colonne scène et une entrée dans la colonne TVDB avec le type de mappage applicable (voir le paragraphe intitulé *Types de mappage* ci-dessous) entre elles.

> Les émissions qui n'ont pas au moins une colonne scène et une colonne TVDB sont inutiles et seront potentiellement supprimées. Il en va de même pour les émissions pour lesquelles il n'existe aucune connexion directe ou indirecte entre la colonne scène et la colonne TVDB.
{.is-warning}

# Types de mappage

TheXEM propose trois options automatiques différentes pour connecter différentes entités les unes aux autres : le mappage SxxExx, le mappage absolu et la combinaison des deux, le mappage complet. Vous pouvez également mapper directement des épisodes les uns sur les autres à l'aide du mappage direct. Chacun de ces types a sa propre utilité et est utile dans des situations particulières.

## Mappage ![SxxExx](/assets/sonarr/xem-guide/mapping-sxxexx.svg) SxxExx

Ce type de mappage détermine que entre les deux entités qu'il connecte, les numéros de saison et d'épisode sont identiques, ce qui signifie que S01E01 est le même épisode dans les deux types d'entités. La numérotation absolue, en revanche, n'est pas nécessairement la même.

## Mappage ![absolu](/assets/sonarr/xem-guide/mapping-abs.svg) absolu

À quelques exceptions près, le mappage absolu est presque exclusivement utile pour les séries d'anime. Le schéma de nomination d'anime utilisé par la plupart des groupes de sortie utilise simplement un numéro d'épisode croissant plutôt qu'une numérotation SxxExx, que nous appelons numérotation absolue. Le fait de marquer le mappage entre deux entités comme "absolu" indique aux services utilisant ces données que la numérotation SxxExx peut différer ou non, mais que la numérotation absolue est au moins la même.

## Mappage ![complet](/assets/sonarr/xem-guide/mapping-full.svg) complet

Le mappage complet indique à tout service utilisant TheXEM que la numérotation absolue et le mappage SxxExx entre les deux entités qu'il connecte sont identiques, ce qui signifie que la numérotation est la même entre les deux entités.

> Cela signifie que si tout ce que vous voulez ajouter à votre mappage est une colonne scène et une colonne TVDB avec un mappage complet entre elles, votre entrée de série est obsolète car cela fonctionne par défaut sans une entrée sur TheXEM.
{.is-info}

## Mappage ![direct](/assets/sonarr/xem-guide/mapping-direct.svg) direct

Le mappage direct est uniquement possible entre l'entité principale et les entités de chaque côté. Vous devez l'utiliser aussi peu que possible, car une fois que vous commencez à utiliser des connexions directes, vous devrez continuer à les utiliser pour le reste de la saison au moins et dans certains cas pour le reste de l'émission.

Vous pouvez activer le mappage direct en cliquant sur l'icône au-dessus du type de mappage automatique. Vous verrez l'interface de la page se déplacer légèrement pour faire de la place aux connexions que vous êtes sur le point de créer. Pour connecter un épisode à un autre épisode, vous cliquez simplement sur un épisode du côté gauche de la connexion, puis vous cliquez sur l'épisode correspondant du côté droit. Si vous l'avez bien fait, le site vous demandera de confirmer la connexion.

> Il est possible de lier un seul épisode d'un côté à plusieurs épisodes de l'autre, par exemple si TVDB considère deux épisodes comme des épisodes distincts alors que la scène les combine en un seul numéro. Cela est particulièrement intéressant pour les dessins animés occidentaux.
{.is-info}

# Exemples

Ce qui précède est beaucoup à assimiler, mais dans l'ensemble, il n'y a que quelques cas d'utilisation qui couvrent la grande majorité des émissions que vous aurez jamais besoin d'ajouter à TheXEM. Voici quelques types de mappage très courants.

## Mappage basique d'anime

Lorsque vous mappez une émission d'anime, nous utilisons toujours la colonne AniDB. Chaque fois que cela est autorisé par le mappage que vous essayez d'obtenir, vous devriez *toujours* viser à utiliser un mappage complet entre la colonne Scène et la colonne AniDB.

La plupart des émissions d'anime peuvent être directement mappées entre la colonne scène via AniDB et enfin vers TVDB. Un exemple simple serait l'émission [Ronia the Robber's Daughter](https://thexem.info/xem/show/1603). Elle a besoin d'un mappage en premier lieu parce que le nom japonais utilisé par les groupes de sortie ne correspond pas au nom anglais utilisé par TVDB, mais sinon le mappage est simple : la numérotation est identique entre la scène et AniDB, nous utilisons donc un mappage complet entre ces deux-là, tandis que la seule chose que nous savons avec certitude entre AniDB et TVDB est que la numérotation SxxExx est identique.

> AniDB réinitialise la numérotation absolue à chaque saison car elle considère chaque saison comme sa propre émission. Lorsque vous ajoutez une nouvelle saison AniDB, assurez-vous d'entrer son numéro d'identification et de définir le champ "Début absolu" pour cette nouvelle saison sur 1.
{.is-info}

Pour un exemple d'une émission d'anime avec plusieurs saisons, jetez un œil à [Assassination Classroom](https://thexem.info/xem/show/2817). Notez les alias séparés pour la deuxième saison, qui aident Sonarr à comprendre que `[Groupe de sortie] Ansatsu Kyoushitsu - 01 (1080p)` correspond à S01E01 dans TVDB tandis que `[Groupe de sortie] Ansatsu Kyoushitsu S2 - 01 (1080p)` correspond à S02E01.

## Mappage complexe d'anime

Parfois, le concept de saison selon TVDB ne correspond pas à ce qu'AniDB appelle une saison. Cela se produit notamment lorsque l'anime est diffusé en tant que *split-cour*. Cela se présente sous la forme d'un ensemble d'épisodes, suivis d'une courte pause après laquelle le prochain ensemble d'épisodes est également diffusé. Les animes split-cour ont généralement une ou au plus deux saisons d'anime entre eux et TVDB considère principalement un anime split-cour lorsque le deuxième lot d'épisodes est annoncé pendant la diffusion de la première partie.

Un exemple de ce que cela pourrait ressembler serait [That Time I Got Reincarnated as a Slime](https://thexem.info/xem/show/5241). Notez comment ce que TVDB appelle saison 2 est en réalité divisé en saisons 2 et 3 selon AniDB. Nous utilisons un lien vers l'entité principale ici pour rendre le mappage moins complexe. Fondamentalement, l'entrée principale combine la numérotation absolue utilisée sur TVDB avec la numérotation SxxExx qu'AniDB utilise. Nous relions ensuite la colonne principale à TVDB en utilisant un mappage absolu et à la colonne AniDB en utilisant un mappage SxxExx. La colonne Scène peut être liée en utilisant un mappage complet comme d'habitude.

## Émissions de dessins animés occidentaux au format court

Les dessins animés pour enfants posent souvent un défi lors du mappage des épisodes, car si un épisode de 30 minutes est divisé en deux histoires distinctes, TVDB les considère comme deux épisodes différents tandis que la scène les considère généralement comme un seul épisode. Cela signifie que nous aurons besoin d'un mappage direct très détaillé entre les épisodes individuels.

Un exemple de cela est l'émission [Paw Patrol](https://thexem.info/xem/show/4814). Lorsque vous survolez les épisodes dans la colonne principale, vous verrez qu'un seul épisode du côté de la scène est lié à un ou deux épisodes du côté de TVDB. Ce type particulier de mappage nécessite une entrée constante au fur et à mesure que de nouveaux épisodes de la série sont diffusés.

> Gardez à l'esprit que le mappage d'un épisode d'un côté à plusieurs épisodes de l'autre peut avoir du sens dans des cas comme celui-ci, mais le mappage de plusieurs épisodes d'un côté à plusieurs épisodes de l'autre n'en a pas. Le logiciel vous permettra de le faire, mais s'il vous plaît, ne le faites pas car Sonarr ne pourra rien en faire.
{.is-warning}

## Mappage individuel complexe

Dans certains cas (heureusement très rares !), le mappage des épisodes les uns sur les autres peut devenir très complexe. TVDB considère que les dates de diffusion sur le réseau principal de l'émission sont déterminantes pour l'ordre des épisodes. Cela peut rendre les choses vraiment complexes dans des cas comme Firefly ou [Transporter](https://thexem.info/xem/show/1653), qui ont été diffusés par leurs réseaux d'origine dans un ordre qui rompt l'ordre chronologique. La scène compense souvent cela en utilisant l'ordre chronologique des épisodes, ce qui nécessite un mappage individuel complexe pour chaque épisode.

Notez qu'avec Transporter, il n'y a pas de mappage automatique entre la colonne principale et la colonne Scène ; tout le mappage est réalisé par des liens directs entre les épisodes.

# Limitations

TheXEM a actuellement quelques limitations que nous essaierons de couvrir ici.

## Un seul schéma de numérotation de scène par série est pris en charge

Si plusieurs groupes de sortie utilisent différents schémas de numérotation, cela complique les choses. Il existe donc quelques lignes directrices en cas de sources en désaccord.

1. La numérotation des sorties de scène a toujours la priorité sur celle des sorties P2P.
2. Si aucune sortie de scène n'existe pour une certaine émission, choisissez celle qui semble la plus populaire. Cela se résumera généralement au groupe qui a tendance à sortir les épisodes le plus rapidement et avec une qualité décente.
3. Dans le cas des animes, nous suivons la numérotation de SubsPlease/Erai-Raws si elle est disponible. Sinon, la ligne directrice précédente s'applique également ici.

## Un seul entité principale est prise en charge

Vous utiliserez le type d'entité principale dans certains cas relativement rares pour établir des connexions directes *ou* pour éviter d'avoir à établir des connexions directes. Cependant, vous ne pouvez utiliser qu'une seule de ces entités principales pour connecter deux autres entités. Parce que l'objectif final est de s'assurer que le mappage fonctionne pour le cas d'utilisation principal de la connexion de TVDB à la scène, vous devrez vous assurer que *ce* mappage fonctionne au moins et si cela nécessite une entité principale, c'est là que vous devrez prioriser son utilisation.

## Suppression de la colonne principale ou des saisons individuelles

Lorsque vous supprimez la colonne principale pour une raison quelconque, assurez-vous qu'il n'y a pas de mappages directs sur les épisodes individuels à l'intérieur. Si vous supprimez la saison alors que les mappages sont toujours présents, **le mappage sera invisible dans l'interface mais existera toujours !** Si vous faites cela par accident, ajoutez simplement à nouveau la saison que vous avez supprimée, annulez les liens individuels, puis supprimez à nouveau la saison.

## Certaines choses ne peuvent tout simplement pas être mappées

L'une des choses à garder à l'esprit est que parfois une série est tellement désordonnée ou complexe qu'elle ne peut pas être mappée dans TheXEM. Parfois, vous pourrez mapper l'un des cas d'utilisation, parfois même pas cela. Dans ces cas, il n'y a souvent rien à faire.

# Besoin d'aide ?

Enfin, si vous avez besoin d'aide pour quoi que ce soit ou si vous n'avez tout simplement pas de compte sur TheXEM, rejoignez-nous sur le serveur Discord de Sonarr dans le canal [#xem](https://discord.gg/QzDaBmN2J3). Nous serons heureux de vous aider. Gardez toutefois à l'esprit que les délais de réponse peuvent être lents et dépendent beaucoup du décalage horaire.
