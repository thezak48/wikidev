---
title: Lidarr Windows Installation
description: Windows-Installationsanleitung für Lidarr
published: true
date: 2023-07-03T20:30:47.519Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:11:02.991Z
---

# Windows

Lidarr wird nativ unter Windows unterstützt. Lidarr kann auf Windows als Windows-Dienst oder als Anwendung in der Systemleiste installiert werden.
> Die Unterstützung für Windows-Versionen ist auf diejenigen beschränkt, die derzeit von Microsoft unterstützt werden. Andere Versionen können funktionieren, aber dies ist eine nicht unterstützte Konfiguration.
{.is-warning}

Ein Windows-Dienst läuft auch dann, wenn der Benutzer nicht angemeldet ist. Es müssen jedoch besondere Vorkehrungen getroffen werden, da Windows-Dienste [nicht auf Netzlaufwerke](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\-Laufwerke oder \\\server\share UNC-Pfade) zugreifen können, ohne spezielle Konfigurationsschritte durchzuführen.

Zusätzlich läuft der Windows-Dienst unter dem Konto "Lokaler Dienst". Standardmäßig **hat dieses Konto keine Berechtigungen, um auf das Benutzerverzeichnis zuzugreifen, es sei denn, die Berechtigungen wurden manuell zugewiesen**. Dies ist besonders relevant, wenn Download-Clients konfiguriert sind, um in Ihr Benutzerverzeichnis herunterzuladen.

Daher empfiehlt es sich, Lidarr als Anwendung in der Systemleiste zu installieren, wenn der Benutzer angemeldet bleiben kann. Diese Option wird während der Installation angeboten.

> Möglicherweise müssen Sie nach der Installation im Systemleistenmodus einmalig "Als Administrator" ausführen, wenn Sie einen Zugriffsfehler erhalten - wie z.B. "Der Zugriff auf den Pfad `C:\ProgramData\Lidarr\config.xml` wurde verweigert" - oder wenn Sie Netzlaufwerke verwenden. Dadurch erhält Lidarr die erforderlichen Berechtigungen. Sie sollten nicht jedes Mal als Administrator ausführen müssen.
{.is-warning}

1. Laden Sie die neueste Version von Lidarr für Ihre Architektur über den unten stehenden Link herunter.
1. Führen Sie das Installationsprogramm aus.
1. Öffnen Sie <http://localhost:8686>, um Lidarr zu verwenden.

- [Windows x64 Installer](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Es ist möglich, Lidarr manuell mit dem [x64 .zip-Download](https://lidarr.servarr.com/v1/update/master/updatefile?os=windows&runtime=netcore&arch=x64) zu installieren. In diesem Fall müssen Sie jedoch manuell Abhängigkeiten, Installation und Berechtigungen behandeln.
{.is-info}