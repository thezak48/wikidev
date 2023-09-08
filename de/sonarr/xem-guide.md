---
title: TheXEM Moderationsleitfaden
description: Anleitung zur Zuordnung verschiedener Szenarien in XEM für eine optimale Verwendung mit Sonarr und anderen PVR-Software.
published: true
date: 2021-11-24T19:26:31.972Z
tags: sonarr, xem
editor: markdown
dateCreated: 2021-10-03T16:48:28.241Z
---

# Inhaltsverzeichnis

- [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [TheXEM Moderationsleitfaden](#thexem-moderationsleitfaden)
- [Benennung](#benennung)
- [Die verschiedenen Entitätstypen](#die-verschiedenen-entitätstypen)
- [Zuordnungstypen](#zuordnungstypen)
  - [!SxxExx Zuordnung](#-sxxexx-zuordnung)
  - [!Absolute Zuordnung](#-absolute-zuordnung)
  - [!Vollständige Zuordnung](#-vollständige-zuordnung)
  - [!Direkte Zuordnung](#-direkte-zuordnung)
- [Beispiele](#beispiele)
  - [Grundlegende Anime-Zuordnung](#grundlegende-anime-zuordnung)
  - [Komplexe Anime-Zuordnung](#komplexe-anime-zuordnung)
  - [Kurzformatige westliche Cartoon-Serien](#kurzformatige-westliche-cartoon-serien)
  - [Komplexe individuelle Zuordnung](#komplexe-individuelle-zuordnung)
- [Einschränkungen](#einschränkungen)
  - [Es wird nur ein Szenenzählungsschema pro Serie unterstützt](#es-wird-nur-ein-szenenzählungsschema-pro-serie-unterstützt)
  - [Es wird nur eine Master-Entität unterstützt](#es-wird-nur-eine-master-entität-unterstützt)
  - [Löschen der Master-Spalte oder einzelner Staffeln darin](#löschen-der-master-spalte-oder-einzelner-staffeln-darin)
  - [Einige Dinge können einfach nicht zugeordnet werden](#einige-dinge-können-einfach-nicht-zugeordnet-werden)
- [Brauchen Sie Hilfe?](#brauchen-sie-hilfe)

# TheXEM Moderationsleitfaden

[TheXEM](https://thexem.info) ist ein Dienst, der Verbindungen zwischen anderen Diensten/Entitäten ermöglicht, die unterschiedliche Nummerierungs- und Benennungsschemata für TV-Serienveröffentlichungen verwenden. Sonarr verwendet TVDB als Datenquelle für seine Episodeninformationen, und manchmal verwenden Szenen- und andere Veröffentlichungsgruppen ein anderes Benennungs- oder Nummerierungsschema. Mit der richtigen Zuordnung ist es möglich sicherzustellen, dass Episode 1 von Staffel 1 nach TVDB's Zählung Episode 5 von Staffel 1 nach der Zählung der Szene entspricht, sodass Sonarr die richtige Episode herunterladen kann, obwohl die Nummerierung unterschiedlich ist.

Dieser Leitfaden richtet sich an Personen mit einem Konto auf TheXEM und führt Sie durch einige der häufigeren Muster, die Sie verwenden möchten. Aber zuerst werden wir Ihnen die Grundlagen erklären.

# Benennung

Als Konvention verwenden wir denselben Namen, den The TVDB für die Show selbst verwendet. Dies ist besonders interessant für internationale Shows wie Anime und läuft im Wesentlichen darauf hinaus, dass wir den offiziell lizenzierten englischen Namen der Show verwenden.

Zusätzlich ist es möglich, verschiedene Aliasnamen für den Seriennamen einzugeben, was hauptsächlich für Anime, aber gelegentlich auch für "normales" Fernsehen nützlich ist.

# Die verschiedenen Entitätstypen

TheXEM hat vier verschiedene Datenquellen oder Entitätstypen, die es derzeit unterstützt und miteinander verbinden kann, wenn dies erforderlich ist. Diese vier Typen sind:

- Szene
- [TVDB](https://thetvdb.com)
- [AniDB](https://anidb.net)
- Master

Eine ordnungsgemäße XEM-Zuordnung für eine bestimmte Show sollte *mindestens* einen Eintrag in der Szene-Spalte und einen Eintrag in der TVDB-Spalte mit dem entsprechenden Zuordnungstyp (siehe Absatz *Zuordnungstypen* unten) haben.

> Shows, die keine Szene-Spalte und keine TVDB-Spalte haben, sind nutzlos und werden möglicherweise entfernt. Das Gleiche gilt für Shows, bei denen keine direkte oder indirekte Verbindung zwischen der Szene-Spalte und der TVDB-Spalte besteht.
{.is-warning}

# Zuordnungstypen

TheXEM bietet drei verschiedene automatische Optionen zum Verbinden verschiedener Entitäten miteinander: SxxExx-Zuordnung, absolute Zuordnung und die Kombination aus beidem, vollständige Zuordnung. Darüber hinaus können Sie auch Episoden direkt miteinander verbinden, indem Sie eine direkte Zuordnung verwenden. Jeder dieser Typen hat seine eigene Verwendung und ist in bestimmten Situationen nützlich.

## ![SxxExx-Zuordnung](/assets/sonarr/xem-guide/mapping-sxxexx.svg) SxxExx-Zuordnung

Bei diesem Typ der Zuordnung wird bestimmt, dass zwischen den beiden verbundenen Entitäten die Staffel- und Episodennummern gleich sind, d.h. S01E01 ist dieselbe Episode in beiden Entitätstypen. Die absolute Nummerierung ist jedoch nicht unbedingt gleich.

## ![Absolute Zuordnung](/assets/sonarr/xem-guide/mapping-abs.svg) Absolute Zuordnung

Abgesehen von einigen sehr spezifischen Anwendungsfällen ist die absolute Zuordnung fast ausschließlich für Anime-Serien nützlich. Das von den meisten Veröffentlichungsgruppen verwendete Anime-Benennungsschema verwendet nur eine fortlaufende Episodennummer anstelle der SxxExx-Nummerierung, die wir als absolute Nummerierung bezeichnen. Wenn die Zuordnung zwischen zwei Entitäten als "absolut" markiert ist, bedeutet dies, dass Dienste, die diese Daten verwenden, wissen, dass die SxxExx-Nummerierung möglicherweise unterschiedlich ist, aber die absolute Nummerierung zumindest gleich ist.

## ![Vollständige Zuordnung](/assets/sonarr/xem-guide/mapping-full.svg) Vollständige Zuordnung

Die vollständige Zuordnung teilt jedem Dienst, der TheXEM verwendet, mit, dass sowohl die absolute Nummerierung als auch die SxxExx-Zuordnung zwischen den beiden verbundenen Entitäten gleich sind, d.h. die Nummerierung ist zwischen beiden Entitäten gleich.

> Das bedeutet, dass wenn Sie Ihrer Zuordnung nur eine Szene-Spalte und eine TVDB-Spalte mit vollständiger Zuordnung zwischen ihnen hinzufügen möchten, Ihr Serieneintrag überflüssig ist, da dies standardmäßig ohne Eintrag in TheXEM funktioniert.
{.is-info}

## ![Direkte Zuordnung](/assets/sonarr/xem-guide/mapping-direct.svg) Direkte Zuordnung

Die direkte Zuordnung ist nur zwischen dem Master-Entitätstyp und den Entitäten auf beiden Seiten möglich. Sie sollten sie so sparsam wie möglich verwenden, da Sie, sobald Sie direkte Verbindungen verwenden, diese für mindestens den Rest der Staffel und in einigen Fällen für den Rest der gesamten Show beibehalten müssen.

Sie können die direkte Zuordnung aktivieren, indem Sie auf das Symbol über dem automatischen Zuordnungstyp klicken. Die Benutzeroberfläche der Seite wird sich ein wenig verschieben, um Platz für die Verbindungen zu schaffen, die Sie gleich herstellen werden. Um eine Episode mit einer anderen Episode zu verbinden, klicken Sie einfach auf eine Episode auf der linken Seite der Verbindung und dann auf die entsprechende Episode auf der rechten Seite. Wenn Sie es richtig gemacht haben, wird die Website Sie bitten, die Verbindung zu bestätigen.

> Es ist möglich, eine einzelne Episode auf einer Seite mit mehreren Episoden auf der anderen Seite zu verknüpfen, zum Beispiel wenn TVDB zwei Episoden als separate Episoden betrachtet, während die Szene sie zu einer Nummer kombiniert. Dies ist besonders interessant für westliche Cartoons.
{.is-info}

# Beispiele

Das oben Gesagte ist viel auf einmal, aber im Großen und Ganzen gibt es nur eine Handvoll Anwendungsfälle, die den Großteil aller Shows abdecken, die Sie jemals zu TheXEM hinzufügen müssen. Im Folgenden finden Sie einige sehr häufige Arten von Zuordnungen.

## Grundlegende Anime-Zuordnung

Bei der Zuordnung einer Anime-Show verwenden wir immer die AniDB-Spalte. Wenn es die Zuordnung, die Sie erreichen möchten, zulässt, sollten Sie immer eine vollständige Zuordnung zwischen der Szene-Spalte und der AniDB-Spalte verwenden.

Die meisten Anime-Shows können direkt von der Szene-Spalte über AniDB und schließlich zu TVDB zugeordnet werden. Ein einfaches Beispiel wäre die Show [Ronia the Robber's Daughter](https://thexem.info/xem/show/1603). Sie muss überhaupt zugeordnet werden, weil der von den Veröffentlichungsgruppen verwendete japanische Name nicht mit dem von TVDB verwendeten englischen Namen übereinstimmt, aber sonst ist die Zuordnung einfach: Die Nummerierung ist zwischen der Szene und AniDB identisch, daher verwenden wir eine vollständige Zuordnung zwischen diesen beiden, während das Einzige, was wir zwischen AniDB und TVDB sicher wissen, ist, dass die SxxExx-Nummerierung identisch ist.

> AniDB setzt die absolute Nummerierung zwischen jeder Staffel zurück, weil es jede Staffel als eigene Show betrachtet. Wenn Sie eine neue AniDB-Staffel hinzufügen, stellen Sie sicher, dass Sie deren ID-Nummer eingeben und dass Sie das Feld "Ab. Start" für diese neue Staffel auf 1 setzen.
{.is-info}

Für ein Beispiel einer Anime-Show mit mehreren Staffeln werfen Sie einen Blick auf [Assassination Classroom](https://thexem.info/xem/show/2817). Beachten Sie die separaten Aliasnamen für die zweite Staffel, die Sonarr dabei helfen, dass `[Release group] Ansatsu Kyoushitsu - 01 (1080p)` zu S01E01 in TVDB zugeordnet wird, während `[Release group] Ansatsu Kyoushitsu S2 - 01 (1080p)` zu S02E01 zugeordnet wird.

## Komplexe Anime-Zuordnung

Manchmal stimmt das Konzept einer Staffel, das TVDB hat, nicht mit dem überein, was AniDB als Staffel bezeichnet. Dies tritt insbesondere auf, wenn ein Anime als sogenanntes *split-cour* veröffentlicht wird. Dies zeigt sich als eine Reihe von Episoden, gefolgt von einer kurzen Pause, nach der die nächsten Episoden ebenfalls ausgestrahlt werden. Split-cour-Anime hat in der Regel eine oder höchstens zwei Anime-Staffeln zwischen sich, und TVDB betrachtet ein Anime in der Regel als split-cour, wenn die zweite Gruppe von Episoden während der Ausstrahlung des ersten Teils angekündigt wird.

Ein Beispiel dafür wäre [That Time I Got Reincarnated as a Slime](https://thexem.info/xem/show/5241). Beachten Sie, wie das, was TVDB als Staffel 2 bezeichnet, in AniDB tatsächlich in die Staffeln 2 und 3 aufgeteilt ist. Wir verwenden hier einen Link zur Master-Entität, um die Zuordnung weniger komplex zu gestalten. Im Wesentlichen kombiniert der Master-Eintrag die absolute Nummerierung, die auf TVDB verwendet wird, mit der SxxExx-Nummerierung, die AniDB verwendet. Wir verknüpfen dann die Master-Spalte mit TVDB mit absoluter Zuordnung und mit der AniDB-Spalte mit SxxExx-Zuordnung. Die Szene-Spalte kann wie gewohnt mit vollständiger Zuordnung verknüpft werden.

## Kurzformatige westliche Cartoon-Serien

Kinderzeichentrickfilme stellen oft eine Herausforderung dar, wenn es darum geht, die Episoden zuzuordnen, da TVDB sie als zwei verschiedene Episoden betrachtet, wenn eine 30-minütige Episode in zwei separate Geschichten aufgeteilt wird, während die Szene sie in der Regel als eine einzige Episode betrachtet. Das bedeutet, dass wir sehr detaillierte direkte Zuordnungen zwischen einzelnen Episoden benötigen.

Ein Beispiel dafür ist die Show [Paw Patrol](https://thexem.info/xem/show/4814). Wenn Sie über Episoden in der Master-Spalte schweben, sehen Sie, dass eine einzelne Episode auf der Szene-Seite mit einer oder zwei Episoden auf der TVDB-Seite verknüpft ist. Diese spezielle Art der Zuordnung erfordert ständige Eingabe, da neue Episoden der Serie ausgestrahlt werden.

> Beachten Sie, dass es in Fällen wie diesem sinnvoll sein kann, eine Episode auf einer Seite mehreren Episoden auf der anderen Seite zuzuordnen, aber es ist nicht sinnvoll, mehrere Episoden auf einer Seite mehreren Episoden auf der anderen Seite zuzuordnen. Die Software erlaubt es Ihnen, es zu tun, aber bitte tun Sie es nicht, da Sonarr damit nichts anfangen kann.
{.is-warning}

## Komplexe individuelle Zuordnung

In einigen (glücklicherweise sehr seltenen!) Fällen kann die Zuordnung von Episoden zueinander sehr komplex werden. TVDB betrachtet die Ausstrahlungsdaten des Hauptnetzwerks der Show als maßgeblich für die Bestimmung der Episodenreihenfolge. Das kann in Fällen wie Firefly oder [Transporter](https://thexem.info/xem/show/1653), die von ihren Originalnetzwerken in einer Reihenfolge ausgestrahlt wurden, die die chronologische Reihenfolge durchbricht, wirklich komplex werden. Die Szene gleicht dies oft dadurch aus, dass sie die chronologische Episodenreihenfolge verwendet, was dazu führt, dass für jede Episode eine komplexe individuelle Zuordnung erforderlich ist.

Beachten Sie, dass bei Transporter keine automatische Zuordnung zwischen der Master-Spalte und der Szene-Spalte besteht; alle Zuordnungen werden durch direkte Links zwischen den Episoden erreicht.

# Einschränkungen

TheXEM hat derzeit einige Einschränkungen, die wir hier behandeln werden.

## Es wird nur ein Szenenzählungsschema pro Serie unterstützt

Wenn mehrere Veröffentlichungsgruppen unterschiedliche Zählungsschemata verwenden, wird dies kompliziert. In solchen Fällen gibt es einige Richtlinien für den Fall von widersprüchlichen Quellen.

1. Die Nummerierung der Szene-Veröffentlichungen hat immer Vorrang vor der der P2P-Veröffentlichungen.
2. Wenn es keine Szene-Veröffentlichungen für eine bestimmte Show gibt, wählen Sie diejenige, die am beliebtesten zu sein scheint. In der Regel läuft es darauf hinaus, dass die Gruppe, die Episoden am schnellsten in guter Qualität veröffentlicht.
3. Im Falle von Anime folgen wir der Nummerierung von SubsPlease/Erai-Raws, sofern verfügbar. Wenn nicht, gilt hier ebenfalls die vorherige Richtlinie.

## Es wird nur eine Master-Entität unterstützt

Sie werden den Master-Entitätstyp in einigen relativ seltenen Fällen verwenden, um direkte Verbindungen herzustellen *oder* um zu vermeiden, direkte Verbindungen herstellen zu müssen. Sie können jedoch nur eine dieser Master-Entitäten verwenden, um zwei andere Entitäten zu verbinden. Da das Endziel darin besteht, sicherzustellen, dass die Zuordnung für den Hauptanwendungsfall der Verbindung von TVDB zur Szene funktioniert, müssen Sie sicherstellen, dass zumindest *diese* Zuordnung funktioniert und wenn dafür eine Master-Entität erforderlich ist, sollten Sie diese priorisieren.

## Löschen der Master-Spalte oder einzelner Staffeln darin

Wenn Sie aus irgendeinem Grund die Master-Spalte löschen, stellen Sie sicher, dass keine direkten Zuordnungen auf einzelnen Episoden darin vorhanden sind. Wenn Sie die Staffel löschen, während die Zuordnungen noch vorhanden sind, **wird die Zuordnung in der Benutzeroberfläche unsichtbar, besteht aber weiterhin!** Wenn Sie dies versehentlich tun, fügen Sie einfach die Staffel, die Sie entfernt haben, erneut hinzu, heben Sie die einzelnen Verknüpfungen auf und löschen Sie dann die Staffel erneut.

## Einige Dinge können einfach nicht zugeordnet werden

Eine der Dinge, die Sie immer im Hinterkopf behalten sollten, ist, dass manchmal eine Serie so durcheinander ist oder anderweitig komplex, dass sie nicht in TheXEM zugeordnet werden kann. Manchmal können Sie einen der Anwendungsfälle zuordnen, manchmal nicht einmal das. In solchen Fällen kann oft nichts wirklich dagegen unternommen werden.

# Brauchen Sie Hilfe?

Schließlich, wenn Sie Hilfe bei etwas benötigen oder wenn Sie einfach kein Konto auf TheXEM haben, treten Sie bitte unserem Sonarr-Discord-Server im [#xem-Kanal](https://discord.gg/QzDaBmN2J3) bei. Wir helfen Ihnen gerne weiter. Bitte beachten Sie jedoch, dass die Reaktionszeiten möglicherweise langsam sind und stark von der Zeitzone abhängen.