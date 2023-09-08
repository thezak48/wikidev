---
title: Readarr Windows Installation
description: Windows-Installationsanleitung für Readarr
published: true
date: 2023-07-04T15:23:25.114Z
tags: 
editor: markdown
dateCreated: 2023-07-03T20:13:03.495Z
---

# Windows

Readarr wird nativ unter Windows unterstützt. Readarr kann auf Windows als Windows-Dienst oder als Anwendung in der Systemleiste installiert werden.
> Windows-Versionen werden nur für die von Microsoft derzeit unterstützten Versionen unterstützt. Andere Versionen können funktionieren, aber dies ist eine nicht unterstützte Konfiguration.
{.is-warning}

Ein Windows-Dienst läuft auch dann, wenn der Benutzer nicht angemeldet ist, aber es müssen besondere Vorsichtsmaßnahmen getroffen werden, da Windows-Dienste [nicht auf Netzlaufwerke](https://learn.microsoft.com/en-us/windows/win32/services/services-and-redirected-drives) (X:\-Laufwerke oder \\\server\share UNC-Pfade) zugreifen können, ohne spezielle Konfigurationsschritte.

Zusätzlich läuft der Windows-Dienst unter dem Konto 'Lokaler Dienst'. Standardmäßig **hat dieses Konto keine Berechtigungen, auf das Benutzerverzeichnis zuzugreifen, es sei denn, die Berechtigungen wurden manuell zugewiesen**. Dies ist besonders relevant, wenn Download-Clients verwendet werden, die so konfiguriert sind, dass sie in Ihr Benutzerverzeichnis herunterladen.

Daher ist es ratsam, Readarr als Anwendung in der Systemleiste zu installieren, wenn der Benutzer angemeldet bleiben kann. Diese Option wird während der Installation angeboten.

> Sie müssen möglicherweise nach der Installation einmal als Administrator ausführen, wenn Sie einen Zugriffsfehler erhalten - wie z.B. "Zugriff auf den Pfad `C:\ProgramData\Readarr\config.xml` verweigert" - oder wenn Sie Netzlaufwerke verwenden. Dadurch erhält Readarr die erforderlichen Berechtigungen. Sie sollten nicht jedes Mal als Administrator ausführen müssen.
{.is-warning}

> Warnung: Wenn Sie Plex als Dienst über [PmsService](https://github.com/cjmurph/PmsService) ausführen, müssen Sie entweder den Port von PMsService von `8787` ändern oder den Port ändern, auf dem Readarr in der `config.xml`-Datei ausgeführt wird.
{.is-info}

1. Laden Sie die neueste Version von Readarr für Ihre Architektur über den unten stehenden Link herunter.
1. Führen Sie das Installationsprogramm aus.
1. Öffnen Sie <http://localhost:8787>, um Readarr zu verwenden.

- [Windows x64 Installer](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64&installer=true)
- [Windows x32 Installer](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x86&installer=true)
{.links-list}

> Es ist möglich, Readarr manuell mit dem [x64 .zip-Download](https://readarr.servarr.com/v1/update/develop/updatefile?os=windows&runtime=netcore&arch=x64) zu installieren. In diesem Fall müssen Sie jedoch manuell mit Abhängigkeiten, Installation und Berechtigungen umgehen.
{.is-info}