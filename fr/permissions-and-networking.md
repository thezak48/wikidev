---
title: Guide de dépannage des problèmes de réseau et d'autorisations
description: 
published: true
date: 2022-03-13T15:12:02.123Z
tags: dépannage
editor: markdown
dateCreated: 2021-11-13T21:09:50.099Z
---

# Dépannage réseau

- En général, `curl` sera nécessaire pour une grande partie du dépannage
- Pour les problèmes SSL, `openssl` sera nécessaire pour le dépannage

## Problèmes SSL

- curl ne valide pas les certificats SSL comme le font les navigateurs, il est donc nécessaire d'utiliser openssl

- Testez la connexion/site en utilisant openssl pour vérifier si les certificats sont valides

```bash
openssl s_client -showcerts -connect <url>:443
```

## Adresse IP IPv6 non connectable

- Testez la connexion avec curl

```bash
curl -sv -6 "http://<url>:<port>/"
```

## Vérification des ports utilisés sous Windows

- Utilisez netsh pour obtenir une liste des ports utilisés et de ce qui les utilise

```bash
netstat -ab
```

## Vérification des réservations d'URL sous Windows

- Utilisez netsh pour obtenir une liste des ports et des URL auxquels les applications sont liées et en écoute

```bash
netsh http show urlacl
```

## Création de réservations d'URL sous Windows

- Utilisez netsh pour créer la réservation d'URL - l'exemple ci-dessous concerne radarr qui utilise le port `7878`

```bash
http add urlacl http://*:7878/ sddl=D:(A;;GX;;;S-1-1-0)
```

## Vérification des ports utilisés sous Linux

- Utilisez netstat pour localiser les ports utilisés / sur quel port une application est en cours d'exécution

```bash
sudo netstat -tnlp | grep <:port or app>
```

### Exemples

- Port `8989`

```bash
sudo netstat -tnlp | grep ':8989'
```

- Application nommée `Radarr`

```bash
sudo netstat -tnlp | grep 'Radarr'
```