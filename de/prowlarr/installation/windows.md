---
title: Prowlarr Windows Installation
description: Windows-Installationsanleitung für Prowlarr
published: true
date: 2023-08-28T19:43:08.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:39.779Z
---

# Windows

Prowlarr wird nativ unter Windows unterstützt. Prowlarr kann entweder als Windows-Dienst oder als System Tray-Anwendung installiert werden.
> Die Unterstützung für Windows-Versionen ist auf diejenigen beschränkt, die derzeit von Microsoft unterstützt werden. Andere Versionen können funktionieren, jedoch handelt es sich dabei um eine nicht unterstützte Konfiguration.
{.is-warning}

Ein Windows-Dienst läuft auch dann, wenn der Benutzer nicht angemeldet ist.
Alternativ kann eine System Tray-Anwendung verwendet werden, wenn der Benutzer angemeldet bleibt. Diese Option wird während der Installation angeboten.

> Wenn Sie nach der Installation einen Zugriffsfehler wie "Zugriff auf den Pfad `C:\ProgramData\Prowlarr\config.xml` verweigert" erhalten, müssen Sie möglicherweise einmalig "Als Administrator" ausführen. Dadurch erhält Prowlarr die erforderlichen Berechtigungen. Sie sollten nicht jedes Mal als Administrator ausführen müssen.
{.is-warning}

1. Laden Sie die neueste Version von Prowlarr für Ihre Architektur über den unten stehenden Link herunter.
1. Führen Sie den Installer aus.
1. Öffnen Sie <http://localhost:9696>, um Prowlarr zu verwenden.

- [Windows x64 Installer](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Es ist möglich, Prowlarr manuell mit dem [x64 .zip-Download](https://prowlarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64) zu installieren. In diesem Fall müssen Sie jedoch manuell Abhängigkeiten, Installation und Berechtigungen behandeln.
{.is-info}

> Wenn Sie [Certify The Web](https://docs.certifytheweb.com/docs/backgroundservice/) zur Verwaltung von LetsEncrypt-Zertifikaten für IIS verwenden und Prowlarr auf demselben Computer installieren, wird der Port `9696` vom Hintergrunddienst verwendet. Sie müssen entweder den Hörport von Prowlarr in Ihrer `config.xml` auf einen anderen Wert ändern oder den Port des Certify The Web-Hintergrunddienstes ändern.
{.is-info}