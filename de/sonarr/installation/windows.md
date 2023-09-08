---
title: Sonarr Windows Installation
description: Windows-Installationsanleitung für Sonarr
published: true
date: 2023-07-04T15:22:44.146Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:54.851Z
---

# Windows

Sonarr wird nativ unter Windows unterstützt. Sonarr kann auf Windows als Windows-Dienst oder als Anwendung im System Tray installiert werden.

> Die Unterstützung für Windows-Versionen ist auf diejenigen beschränkt, die derzeit von Microsoft unterstützt werden. Andere Versionen können funktionieren, aber dies ist eine nicht unterstützte Konfiguration.
{.is-warning}

Ein Windows-Dienst läuft auch dann, wenn der Benutzer nicht angemeldet ist, aber es müssen besondere Vorkehrungen getroffen werden, da Windows-Dienste [nicht auf Netzlaufwerke](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\-Laufwerke oder \\\server\share UNC-Pfade) zugreifen können, ohne spezielle Konfigurationsschritte durchzuführen.

Darüber hinaus läuft der Windows-Dienst unter dem Konto "Lokaler Dienst". Standardmäßig **hat dieses Konto keine Berechtigungen, auf das Benutzerverzeichnis zuzugreifen, es sei denn, die Berechtigungen wurden manuell zugewiesen**. Dies ist besonders relevant, wenn Download-Clients verwendet werden, die so konfiguriert sind, dass sie in Ihr Benutzerverzeichnis herunterladen.

Daher empfiehlt es sich, Sonarr als Anwendung im System Tray zu installieren, wenn der Benutzer angemeldet bleiben kann. Diese Option wird während der Installation angeboten.

> Möglicherweise müssen Sie nach der Installation einmalig "Als Administrator" ausführen, wenn Sie einen Zugriffsfehler erhalten - wie z.B. "Zugriff auf den Pfad `C:\ProgramData\Sonarr\config.xml` verweigert" - oder wenn Sie Netzlaufwerke verwenden. Dadurch erhält Sonarr die erforderlichen Berechtigungen. Sie sollten nicht jedes Mal als Administrator ausführen müssen.
{.is-warning}

1. Laden Sie die neueste Version von Sonarr für Ihre Architektur über den unten stehenden Link herunter.
1. Führen Sie das Installationsprogramm aus.
1. Öffnen Sie <http://localhost:8989>, um Sonarr zu verwenden.

- [Windows x32 Installer](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows&installer=true)
{.links-list}

> Es ist möglich, Sonarr manuell mit dem [x32 .zip-Download](https://services.sonarr.tv/v1/download/main/latest?version=3&os=windows) zu installieren. In diesem Fall müssen Sie jedoch manuell mit Abhängigkeiten, Installation und Berechtigungen umgehen.
{.is-info}