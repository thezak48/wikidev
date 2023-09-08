---
title: Radarr Windows Installation
description: Windows-Installationsanleitung für Radarr
published: true
date: 2023-07-04T15:22:03.589Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:12:19.928Z
---

# Windows

Radarr wird nativ unter Windows unterstützt. Radarr kann als Windows-Dienst oder als Anwendung in der Systemleiste installiert werden.
> Windows-Versionen werden nur für die von Microsoft derzeit unterstützten Versionen unterstützt. Andere Versionen können funktionieren, jedoch handelt es sich dabei um eine nicht unterstützte Konfiguration.
{.is-warning}

Ein Windows-Dienst läuft auch dann, wenn der Benutzer nicht angemeldet ist. Es müssen jedoch besondere Vorkehrungen getroffen werden, da Windows-Dienste [nicht auf Netzlaufwerke](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\-Laufwerke oder \\\server\share UNC-Pfade) zugreifen können, es sei denn, spezielle Konfigurationsschritte wurden durchgeführt.

Darüber hinaus läuft der Windows-Dienst unter dem Konto "Lokaler Dienst". Standardmäßig **hat dieses Konto keine Berechtigungen zum Zugriff auf das Benutzerverzeichnis, es sei denn, die Berechtigungen wurden manuell zugewiesen**. Dies ist besonders relevant, wenn Download-Clients so konfiguriert sind, dass sie in Ihr Benutzerverzeichnis herunterladen.

Daher empfiehlt es sich, Radarr als Anwendung in der Systemleiste zu installieren, wenn der Benutzer angemeldet bleiben kann. Diese Option wird während der Installation angeboten.

> Sie müssen möglicherweise nach der Installation einmalig "Als Administrator ausführen", wenn Sie einen Zugriffsfehler erhalten - wie z.B. "Zugriff auf den Pfad `C:\ProgramData\Radarr\config.xml` verweigert" - oder wenn Sie Netzlaufwerke verwenden. Dadurch erhält Radarr die erforderlichen Berechtigungen. Sie sollten nicht jedes Mal "Als Administrator ausführen" müssen.
{.is-warning}

1. Laden Sie die neueste Version von Radarr für Ihre Architektur über den unten stehenden Link herunter.
1. Führen Sie das Installationsprogramm aus.
1. Öffnen Sie <http://localhost:7878>, um Radarr zu verwenden.

- [Windows x64 Installer](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Es ist möglich, Radarr manuell über den [x64 .zip-Download](https://radarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64) zu installieren. In diesem Fall müssen Sie jedoch manuell Abhängigkeiten, Installation und Berechtigungen behandeln.
{.is-info}