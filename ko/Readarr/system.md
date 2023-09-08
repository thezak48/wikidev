# 상태

## 건강 상태

- 이 페이지에는 건강 검사 오류 목록이 포함되어 있습니다. 이 건강 검사는 Readarr에서 주기적으로 수행되며 특정 이벤트에서 수행됩니다. 결과로 나타나는 경고 및 오류는 해결 방법에 대한 안내를 제공하기 위해 여기에 나열됩니다.

### 시스템 경고

#### 브랜치가 유효한 릴리스 브랜치가 아닙니다

- 설정한 브랜치가 유효한 릴리스 브랜치가 아닙니다. 업데이트를 받을 수 없습니다. [현재 릴리스 브랜치](/readarr/faq#how-do-i-update-readarr) 중 하나로 변경하십시오.

#### 현재 설치된 SQLite 버전이 지원되지 않습니다

- Readarr은 데이터를 SQLite 데이터베이스에 저장합니다. 시스템에 설치된 SQLite3 라이브러리가 너무 오래되었습니다. Readarr은 적어도 버전 3.9.0 이상을 필요로 합니다. Readarr은 SQLite3 업그레이드 패키지에 포함되어 있을 수도 있고 포함되어 있지 않을 수도 있는 `libSQLite3.so`를 사용합니다.

> Readarr은 SQLite3 업그레이드 패키지에 포함되어 있을 수도 있고 포함되어 있지 않을 수도 있는 `libSQLite3.so`를 사용합니다.
{.is-info}

#### 새로운 업데이트가 사용 가능합니다

- 개발자들이 새로운 업데이트를 릴리스했습니다. 이는 일반적으로 멋진 새로운 기능과 버그 수정을 의미합니다 (맞죠?). 자동 업데이트가 활성화되어 있지 않으므로 플랫폼에서 업데이트하는 방법을 찾아야 합니다. 시스템 => 업데이트 페이지에서 설치 버튼을 누르는 것이 좋은 시작점입니다.

> 현재 버전이 14일 이내인 경우에는 이 경고가 표시되지 않습니다.
{.is-info}

#### 사용자가 시작 폴더를 쓸 수 없기 때문에 업데이트를 설치할 수 없습니다

- 이는 Readarr이 자체 업데이트를 수행할 수 없음을 의미합니다. Readarr을 수동으로 업데이트하거나 Readarr의 시작 디렉토리 (설치 디렉토리)의 권한을 설정하여 Readarr이 자체 업데이트할 수 있도록 해야 합니다.

#### 업데이트를 삭제하면 AppData가 삭제될 수 있으므로 업데이트할 수 없습니다

- Readarr은 운영 체제의 AppData 폴더가 Readarr 이진 파일을 포함하는 디렉토리 내에 위치해 있는 것을 감지했습니다. 일반적으로 Windows의 경우 C:\ProgramData이고, Linux의 경우 ~/.config입니다.

- 현재 AppData 및 시작 디렉토리를 확인하려면 System => Info를 참조하십시오.
- 이는 데이터 손실의 위험 없이 Readarr이 자체 업데이트할 수 없음을 의미합니다.
- Linux의 경우 Readarr을 실행하는 사용자의 홈 디렉토리를 변경하고 현재 ~/.config/Readarr 디렉토리의 내용을 복사해야 합니다.

#### 브랜치는 이전 버전을 위한 것입니다

- 설정/일반에서 설정한 업데이트 브랜치는 이전 버전의 Readarr을 위한 것이므로 시스템/업데이트 피드에서 올바른 업데이트 정보를 볼 수 없으며 새로운 업데이트를 받을 수 없을 수 있습니다.

#### signalR에 연결할 수 없습니다

- signalR은 동적 UI 업데이트를 제어합니다. 따라서 브라우저가 서버의 signalR에 연결할 수 없으면 UI에서 실시간 업데이트를 볼 수 없습니다.

- 가장 일반적인 경우는 역방향 프록시나 클라우드플레어의 사용입니다.
- 클라우드플레어에서는 웹소켓을 활성화해야 합니다.

##### Nginx

- Nginx에는 다음과 같은 추가가 필요합니다.

```none
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection $http_connection;
```

> nginx 문서에서 제안하는 대로 proxy_set_header Connection "Upgrade";를 포함하지 않도록 주의하십시오. 이렇게 하면 작동하지 않습니다.
> <https://github.com/aspnet/AspNetCore/issues/17081>을 참조하십시오.
{.is-warning}

Apache2 역방향 프록시의 경우 다음 모듈을 활성화해야 합니다: proxy, proxy_http 및 proxy_wstunnel. 그런 다음 다음 웹소켓 터널 지시문을 vhost 구성에 추가하십시오.

```none
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /(.*) ws://127.0.0.1:8787/$1 [P,L]
```

Caddy (V1)의 경우 다음을 사용하십시오:
참고: Readarr 구성에도 웹소켓 지시문을 추가해야 합니다.

```none
 proxy /readarr 127.0.0.1:8787 {
     websocket
     transparent
 }
```

#### 구성된 프록시 호스트의 IP 주소를 확인할 수 없습니다

- 프록시 설정을 검토하고 정확한지 확인하십시오.
- 프록시가 실행 중이고 작동 가능한지 확인하십시오.

#### 프록시 테스트 실패

- 구성된 프록시가 테스트에 실패했습니다. 제공된 HTTP 오류를 검토하거나 자세한 내용은 로그를 확인하십시오.

#### 시스템 시간이 1일 이상 차이가 납니다

- 시스템 시간이 1일 이상 차이가 납니다. 시간이 수정될 때까지 예약된 작업이 올바르게 실행되지 않을 수 있습니다.
- 시스템 시간을 검토하고 권위 있는 시간 서버와 동기화되어 있는지 확인하십시오.

### 다운로드 클라이언트

#### 사용 가능한 다운로드 클라이언트가 없습니다

- Readarr이 미디어를 다운로드하기 위해서는 올바르게 구성되고 활성화된 다운로드 클라이언트가 필요합니다. Readarr은 다양한 다운로드 클라이언트를 지원하므로 요구 사항과 가장 일치하는 클라이언트를 결정해야 합니다. 이미 다운로드 클라이언트를 설치했다면 Readarr에서 사용하도록 구성하고 카테고리를 생성해야 합니다. 설정 => 다운로드 클라이언트를 참조하십시오.

#### 다운로드 클라이언트와 통신할 수 없습니다

- Readarr이 구성된 다운로드 클라이언트와 통신할 수 없었습니다. 다운로드 클라이언트가 작동 중인지 확인하고 URL을 다시 확인하십시오. 이는 인증 오류일 수도 있습니다.
- 일반적으로 잘못 구성된 다운로드 클라이언트로 인해 발생합니다. 일반적으로 확인할 수 있는 사항:
- 다운로드 클라이언트의 IP 주소는 동일한 물리적인 기계에 있는 경우 일반적으로 127.0.0.1입니다.
- 다운로드 클라이언트가 사용하는 포트 번호는 기본 포트 번호로 채워져 있지만 변경한 경우 Readarr에도 동일한 포트 번호를 입력해야 합니다.
- 로컬 네트워크에서 Readarr 인스턴스와 다운로드 클라이언트를 모두 사용하는 경우 SSL 암호화를 사용하지 않도록 설정되어 있는지 확인하십시오. 자세한 내용은 SSL FAQ 항목을 참조하십시오.

#### 다운로드 클라이언트가 실패로 인해 사용할 수 없습니다

{#download-clients-are-unavailable-due-to-failures}

- 하나 이상의 다운로드 클라이언트가 Readarr의 요청에 응답하지 않습니다. 따라서 Readarr은 일반적으로 활성 다운로드를 추적하고 완료된 다운로드를 가져오는 데 사용되는 정상적인 1분 주기의 다운로드 클라이언트 쿼리를 일시적으로 중지하기로 결정했습니다. 그러나 Readarr은 계속해서 다운로드를 클라이언트에 보내려고 시도하지만 아마도 실패할 것입니다.
- 실패의 원인을 확인하려면 System=>Logs를 검사하십시오.
- 이 다운로드 클라이언트를 더 이상 사용하지 않는 경우 Readarr에서 비활성화하여 오류를 방지하십시오.

#### 완료된 다운로드 처리 활성화

- Readarr은 완료된 다운로드 처리를 활성화해야 다운로드 클라이언트에서 다운로드한 파일을 가져올 수 있습니다. 완료된 다운로드 처리를 활성화하는 것이 좋습니다.
- (완료된 다운로드 처리는 새로운 사용자에 대해 기본적으로 활성화됩니다.)

#### Docker 잘못된 원격 경로 매핑

- 이 오류는 다운로드 클라이언트나 Readarr 내에서 잘못된 도커 경로와 관련이 있습니다.

- 예를 들면:
  - 다운로드 클라이언트: 다운로드 경로: /mnt/user/downloads:/downloads
  - Readarr: 다운로드 경로: /mnt/user/downloads:/data
- 이 예에서 다운로드 클라이언트는 다운로드를 /downloads에 저장하고 완료된 책이 /downloads에 있다고 알립니다. 그런 다음 Readarr이 "좋아, /downloads를 확인해볼게요"라고 말합니다. 그러나 Readarr 내에서는 /downloads 경로를 할당하지 않았고 /data 경로를 할당했으므로 이 오류가 발생합니다.
- 이 문제를 해결하는 가장 쉬운 방법은 일관성입니다. 다운로드 클라이언트에서 한 가지 체계를 사용하는 것입니다.

- Team Readarr은 /data를 사용하는 것을 권장합니다.
  - 다운로드 클라이언트: /mnt/user/data/downloads:/data/downloads
  - Readarr: /mnt/user/data:/data

- 이제 다운로드 클라이언트에서 /data에 파일을 저장할 위치를 지정할 수 있습니다. 클라이언트에 따라 다르지만 "네, 다운로드 클라이언트, 파일을 여기에 저장해주세요."라고 말할 수 있어야 합니다. /data/torrents (또는 usenet)/books와 같이 사용할 수 있습니다. 그리고 Readarr에서 /data를 사용했으므로 다운로드 클라이언트가 완료되었다고 알리면 Readarr은 "/data를 가지고 있고 /torrents (또는 usenet)/books도 볼 수 있습니다. 모든 것이 올바르게 작동합니다."
- [Docker 가이드](/docker-guide)와 TRaSH의 [Hardlinks and Instant Moves (Atomic-Moves) 가이드](https://trash-guides.info/hardlinks/)에 대한 많은 정보가 있습니다. 이 가이드는 하드링크와 원자적 이동에 중점을 두지만 컨테이너와 경로 매핑 작동 방식에 대한 개념이 이러한 토론의 핵심입니다.

- 운영 체제를 넘나드는 경우나 네이티브와 도커를 넘나드는 경우 원격 경로 매핑이 필요합니다. 모든 \*Arr에 대해 동일한 개념이 적용되지만 TRaSH의 [Radarr용 원격 경로 매핑 가이드](https://trash-guides.info/Radarr/Radarr-remote-path-mapping/)를 참조하여 자세한 내용을 확인하십시오.

- Calibre에서 이 오류가 발생하는 경우 Redarr은 Calibre의 라이브러리에 액세스할 수 없습니다. 해결 방법은 동일합니다 - 컨테이너의 일관성이 없는 마운트를 수정하십시오. 또는 Calibre 라이브러리 경로를 Readarr에서 액세스할 수 있는 경로로 매핑하는 원격 경로 매핑을 만들 수 있습니다. 원격 경로 매핑은 운영 체제나 서버를 넘나드는 경우에만 필요합니다. 모든 것이 Docker에 있는 경우 마운트를 수정하는 것이 좋습니다.

#### 루트 폴더에 다운로드 중입니다

{#downloads-in-root-folder}

- 응용 프로그램 내에서 루트 폴더는 구성된 미디어 라이브러리 폴더로 정의됩니다. 이는 마운트의 루트 폴더가 아닙니다. 다운로드 클라이언트가 루트(라이브러리) 폴더로 불완전하거나 완료된 다운로드(또는 완료된 다운로드를 이동)를 이동하고 있습니다.
- 이는 데이터 손실을 포함한 문제를 자주 발생시키며 수행해서는 안 됩니다. 이를 수정하려면 다운로드 클라이언트를 변경하여 루트 폴더에 다운로드하지 않도록 설정하십시오. '다운로드' 클라이언트 카테고리가 루트 폴더로 설정되어 있는 경우나 NZBGet/SABnzbd가 정렬을 사용하고 루트 폴더로 정렬하는 경우도 포함됩니다.
- 이 체크는 현재 사용 중인 루트 폴더뿐만 아니라 추가된 모든 정의된 루트 폴더를 확인합니다. 즉, 다운로드 클라이언트가 다운로드를 수행하거나 완료된 다운로드를 이동하는 폴더는 *arr 응용 프로그램에서 구성한 루트/라이브러리/최종 미디어 대상 폴더와 동일한 폴더일 수 없습니다.
- 구성된 루트 폴더(라이브러리 폴더)는 [설정 => 미디어 관리 => 루트 폴더](/readarr/settings/#root-folders)에서 찾을 수 있습니다.
- 예를 들어 다운로드가 `\data\downloads`로 이동한다면 루트 폴더로 `\data\downloads`가 설정되어 있습니다.
- 루트 폴더/라이브러리 폴더에는 미디어가 아닌 다운로드가 저장되는 다운로드 폴더와 동일한 폴더를 사용하지 않도록 권장합니다.
- 루트 폴더에는 `\data\media\`와 같은 경로를 사용하는 것이 좋습니다. 다운로드에는 `\data\downloads\`와 같은 경로를 사용하는 것이 좋습니다.
- 올바른 경로 설정에 대한 자세한 내용은 [Docker 가이드](/docker-guide)와 TRaSH의 [Hardlinks and Instant Moves (Atomic-Moves) 가이드](https://trash-guides.info/hardlinks/)를 검토하십시오. 도커 및 비도커에 대한 개념이 적용됩니다.

> 다운로드 클라이언트가 다운로드 폴더에 다운로드한 파일을 가져와서 라이브러리로 가져옵니다. 다운로드 클라이언트는 라이브러리로 아무것도 이동하거나 다운로드해서는 안 됩니다.
{.is-warning}

#### 잘못된 다운로드 클라이언트 설정

- 다운로드 클라이언트가 파일을 다운로드하는 위치가 문제를 일으키고 있습니다. 자세한 정보는 로그를 확인하십시오. 이는 권한이나 Windows에서 Linux로 또는 Linux에서 Windows로 이동하려고 할 때 발생할 수 있습니다.

#### 잘못된 원격 경로 매핑

- 다운로드 클라이언트가 파일을 다운로드하는 위치가 문제를 일으키고 있습니다. 자세한 정보는 로그를 확인하십시오. 이는 권한 문제이거나 Windows에서 Linux로 또는 Linux에서 Windows로 이동할 때 원격 경로 매핑이 없는 경우일 수 있습니다. 자세한 내용은 [TRaSH의 원격 경로 가이드](https://trash-guides.info/Readarr/Readarr-remote-path-mapping/)를 참조하십시오.

#### 권한 오류

- Readarr 또는 readarr 사용자가 다운로드 클라이언트가 파일을 다운로드하는 위치에 액세스할 수 없습니다. 일반적으로 이는 권한 문제입니다.

#### 작성자 마운트는 읽기 전용입니다

{#author-mount-ro}

- 작성자 경로를 포함하는 마운트가 읽기 전용으로 마운트되었습니다. 마운트 설정과 소유권/권한을 확인하십시오.

#### 원격 파일이 처리 중에 제거되었습니다

- 원격 경로 맵을 통해 액세스 가능한 파일이 처리가 완료되기 전에 제거된 것으로 보입니다.

#### 원격 경로가 사용되고 가져오기에 실패했습니다

- 자세한 정보는 로그를 확인하십시오. 문제 해결 가이드를 참조하십시오.

### 완료/실패한 다운로드 처리

#### 완료된 다운로드 처리가 비활성화되었습니다

- (이 경고는 완료된 다운로드 처리 기능이 구현되기 전에 기존 사용자를 위해 생성됩니다. 이 기능은 기본적으로 비활성화되어 있어 현재 구성이 예상대로 작동하도록 보장합니다.)
- 완료된 다운로드 처리를 사용하는 것이 좋습니다. 완료된 다운로드 처리는 다양한 다운로드 클라이언트의 압축 해제 및 후 처리 논리와의 호환성을 제공하기 때문입니다. 이를 통해 Readarr은 다운로드 클라이언트가 준비되었다고 보고할 때만 다운로드를 가져옵니다.
- 완료된 다운로드 처리를 사용하려면 다음을 확인해야 합니다. * 경고: 완료된 다운로드 처리는 다운로드 클라이언트와 Readarr이 동일한 컴퓨터에 있을 때만 올바르게 작동합니다. 왜냐하면 다운로드 클라이언트로부터 가져올 경로를 직접 얻기 때문입니다. 그렇지 않으면 원격 맵이 필요합니다.

### 인덱서

#### 자동 검색이 활성화된 인덱서가 없습니다. Readarr은 자동 검색 결과를 제공하지 않습니다.

- 간단히 말해서, 자동 검색을 허용하는 인덱서가 없습니다.
- 설정 => 인덱서로 이동하여 자동 검색을 허용하려는 인덱서를 선택한 후 저장을 클릭하십시오.

#### RSS 동기화가 활성화된 인덱서가 없습니다. Readarr은 새로운 릴리스를 자동으로 가져오지 않습니다.

- Readarr은 RSS 피드를 사용하여 새로운 릴리스를 가져옵니다. 자세한 내용은 여기에서 확인하십시오.
- 이 문제를 수정하려면 설정 => 인덱서로 이동하여 사용 중인 인덱서를 선택하고 RSS 동기화를 활성화하십시오.

#### 인덱서가 활성화되지 않았습니다

- Readarr은 새로운 릴리스를 발견하기 위해 인덱서가 필요합니다. 인덱서를 추가하는 방법에 대한 지침은 위키를 참조하십시오.

### 활성화된 인덱서가 검색을 지원하지 않습니다

- 활성화된 인덱서 중 어느 하나도 검색을 지원하지 않습니다. 이는 Readarr이 RSS 피드를 통해 새로운 릴리스를 찾을 수 있지만 책을 검색하는 경우(자동 검색 또는 수동 검색)에는 결과를 반환하지 않을 것입니다. 이 문제를 해결하기 위해서는 다른 인덱서를 추가해야 합니다.

#### 대화식 검색이 가능한 인덱서가 없습니다

- 활성화된 인덱서 중 어느 하나도 대화식 검색을 지원하지 않습니다. 이는 응용 프로그램이 RSS 피드나 자동 검색을 통해 새로운 릴리스를 찾을 수 있을 것입니다.

#### 인덱서가 오류로 인해 사용할 수 없습니다

- Readarr이 인덱서 중 하나를 사용하려고 시도하는 동안 오류가 발생했습니다. Readarr은 재시도를 제한하기 위해 해당 인덱서를 점점 더 오랜 시간 동안 사용하지 않을 것입니다(최대 24시간까지).
- 이 메커니즘은 Readarr이 인덱서로부터 응답을 받지 못한 경우(도메인 이름 시스템(DNS), 프록시/VPN 연결, 인증 또는 인덱서 문제로 인한 것일 수 있음) 또는 인덱서로부터 nzb/torrent 파일을 가져오지 못한 경우에 트리거됩니다. 문제의 원인을 확인하기 위해 로그를 검사하십시오.
- 해당 인덱서를 비활성화하여 경고를 방지할 수 있습니다.
- 인덱서를 다시 확인하려면 인덱서에서 테스트를 실행하십시오. Readarr은 인덱서를 다시 확인하기 위해 테스트를 실행합니다. 단, 건강 상태 확인 경고가 즉시 사라지지 않을 수 있습니다.

#### Jackett의 모든 엔드포인트가 사용되었습니다

- Jackett의 /all 엔드포인트는 편리하지만 그것만의 이점이 있습니다. 그 외의 모든 것은 잠재적인 문제입니다. 따라서 각 트래커를 개별적으로 추가해야 합니다.
- [Jackett의 개발자들도 이를 피하고 사용하지 말아야 한다고 말합니다.](https://github.com/Jackett/Jackett#aggregate-indexers)
- /all 엔드포인트를 사용하는 것에는 장점이 없으며, 다음과 같은 단점이 있습니다:
  - 인덱서별 설정(카테고리, 검색 모드 등)을 제어할 수 없습니다.
  - 검색 모드(IMDB, 쿼리 등)를 혼합하면 품질이 낮은 결과가 발생할 수 있습니다.
  - 인덱서별 카테고리(\>= 100000)를 사용할 수 없습니다.
  - 느린 인덱서는 전체 결과를 느리게 만듭니다.
  - 총 결과는 1000개로 제한됩니다.
  - /all의 트래커 중 하나에서 오류가 발생하면 \*Arr은 해당 트래커를 비활성화하고 결과를 얻을 수 없게 됩니다.

##### 해결 방법

- Jackett에서 각 트래커를 수동으로 인덱서로 추가하십시오.
- \*Arr에 인덱서를 동기화할 수 있는 [Prowlarr](/prowlarr)를 확인하십시오. 이는 Lidarr/Radarr/Readarr 개발팀에서 제공합니다.
- 인덱서를 \*Arr에 동기화할 수 있는 [NZBHydra2](https://github.com/theotherp/nzbhydra2)를 확인하십시오. 그러나 단일 집계 엔드포인트를 사용하지 마시고 동기화를 사용할 경우 `multi`를 사용하십시오.

### 책 폴더

#### 루트 폴더가 없습니다

- 이 오류는 작성자가 루트 폴더를 찾고 있지만 해당 루트 폴더가 더 이상 사용할 수 없는 경우에 일반적으로 식별됩니다.
- 이 오류는 여전히 루트 폴더를 가리키는 목록이 있지만 해당 루트 폴더가 더 이상 사용할 수 없는 경우에도 발생할 수 있습니다.
- 이 경고를 제거하려면 간단히 이전 루트 폴더를 사용하는 앨범을 찾아서 올바른 루트 폴더로 편집하면 됩니다.

- 문제가 있는 작성자를 찾는 가장 쉬운 방법은 다음과 같습니다.

  - 작성자(라이브러리) 탭으로 이동합니다.
  - 이전 루트 폴더 경로로 사용자 지정 필터를 생성합니다.
  - 상단 표시줄에서 대량 편집을 선택하고 루트 경로 드롭다운에서 이 작성자를 이동할 새 루트 경로를 선택합니다.
  - 그런 다음 '작성자 폴더를 '루트 경로'로 이동하시겠습니까?'라는 팝업이 표시됩니다. 이 팝업에는 '이 작성자 폴더의 이름도 설정에서 지정한 작성자 폴더 형식에 따라 변경됩니다. 파일을 이동하지 않으려면 아니오를 선택하십시오.'라고도 나와 있습니다. Lidarr이 파일을 이동하지 않도록 하려면 아니오를 선택하십시오.
  - 시스템 => 작업에서 체크 헬스크 작업을 실행하십시오.

### 가져오기 목록

#### 가져오기 목록이 실패로 인해 사용할 수 없습니다

- 일반적으로 이는 Readarr이 API를 통해 통신하거나 선택한 목록 제공자에 로그인할 수 없게 되어 있는 것을 의미합니다. 문제가 지속되는 경우, 해당 목록 제공자에 문의하여 제외할 수 있도록 하십시오. 시스템이 때때로 과부하될 수 있습니다.

## 디스크 공간

- 이 섹션에서는 사용 가능한 디스크 공간을 표시합니다.
- Docker의 경우 Docker 이미지 내에서 사용 가능한 공간을 일반적으로 표시합니다.

## 정보

- 현재 Readarr 설치에 대한 정보를 제공합니다.

## 추가 정보

- 홈페이지: Readarr의 홈페이지
- 위키: 이미 여기에 있습니다
- Reddit: r/readarr
- Discord: Discord에 가입하세요
- 기부: 기부하고 싶으시다면 여기를 클릭하세요
- Sonarr에 기부: 모든 것을 시작한 프로젝트에 기부하고 싶으시다면 여기를 클릭하세요
- 소스: GitHub
- 기능 요청: 멋진 아이디어가 있다면 여기에 제출하세요

# 작업

## 예약된 작업

- 이 섹션에서는 Readarr이 실행하는 모든 예약된 작업을 나열합니다.

- 응용 프로그램 업데이트 확인 - 이 작업은 UI에 표시된 일정에 따라 실행되며, Readarr이 가장 최신 버전인지 확인한 다음 업데이트 스크립트를 트리거하여 Readarr을 업데이트합니다. 설정 => 업데이트

> 참고: Docker를 사용하는 경우 이 작업은 컨테이너를 업데이트하지 않습니다. 새 이미지를 다운로드해야 합니다.
{.is-warning}

- 백업 - 이 작업은 설정된 일정에 따라 Readarr 데이터베이스를 백업합니다. 자세한 내용은 여기에서 확인할 수 있습니다. 백업에 대한 자세한 정보는 시스템 => 백업을 참조하십시오.
- 건강 상태 확인 - 건강 상태 확인은 UI에 표시된 일정에 따라 실행되며 Readarr의 전반적인 건강 상태를 확인합니다. 가능한 건강 관련 문제 목록은 건강 상태 확인 위키 항목을 참조하십시오.
- 정리 - UI에 표시된 일정에 따라 이 작업은 모든 먼지를 제거하고 바닥을 쓸고 진공청소기를 사용하여 바닥을 닦아주며, 깔끔하고 정리된 메모를 작성합니다. 하지만 쓰레기는 처리하지 않습니다. 그것은 충분히 잘 지불받지 못했습니다.
- 가져오기 목록 동기화 - UI에 표시된 일정에 따라 이 작업은 목록을 실행하고 가능한 새 책을 가져옵니다. 목록에 대한 자세한 정보는 설정 => 목록을 참조하십시오.
- 메시지 정리 - UI에 표시된 일정에 따라 이 작업은 Readarr 왼쪽 하단에 나타나는 메시지를 정리합니다.
- 작성자 새로 고침 - 이 작업은 라이브러리의 모든 작성자를 새로 고칩니다.
- 모니터링 중인 다운로드 새로 고침 - 이 작업은 활동 아래에 있는 다운로드 대기열을 새로 고칩니다. 다운로드가 완료되었는지 확인하기 위해 다운로드 클라이언트에 핑을 보냅니다.
- 폴더 다시 스캔 - 이 작업은 모든 책 폴더를 스캔하여 책이 존재하는지 여부를 확인하고 적절한 상태로 업데이트합니다.
- RSS 동기화 - 이 작업은 RSS 동기화를 실행합니다. 이는 설정 => 옵션에서 변경할 수 있습니다. RSS 기능에 대한 자세한 정보는 FAQ에서 확인할 수 있습니다.
  
> 이러한 작업은 각 작업의 가장 오른쪽에 있는 아이콘을 클릭하여 예약된 시간 외에 수동으로 실행할 수 있습니다.
{.is-info}

## 대기열

대기열에서는 실행 중인 작업과 예정된 작업, 최근 실행된 작업 및 해당 작업에 걸린 시간의 기록을 표시합니다.

# 백업

> Readarr 인스턴스를 백업/복원하는 방법을 찾고 있다면 [여기](/readarr/faq)를 클릭하세요.
{.is-info}

- 백업 섹션에서는 이전 백업(백업을 만들지 않은 새로 설치한 경우 제외)이 표시됩니다.
  
- 지금 백업 - 이 옵션을 선택하면 Readarr 데이터베이스의 수동 백업이 트리거됩니다.
- 백업 복원 - 이 옵션을 선택하면 이전 백업에서 복원하기 위해 새 화면이 열립니다.
  - 파일 선택을 선택하면 브라우저가 Readarr Zip 백업을 복원하기 위한 대화 상자를 엽니다.
  
- 이전 백업이 있고 이를 다운로드하여 표준 위치에 저장하려면 이 파일 중 하나를 선택할 수 있습니다.
- 이전 다운로드의 오른쪽에는 두 가지 옵션이 있습니다.
  - 복원(시계 아이콘) - 이전 백업에서 복원하기 위해 - 이 옵션을 선택하면 새 창이 열려 이 백업에서 복원하려는지 확인합니다.
  - 삭제(휴지통 아이콘) - 이전 백업을 삭제합니다.

# 업데이트

- 업데이트 화면에서는 지난 5개의 업데이트와 현재 버전이 표시됩니다.
- 이 페이지에서는 개발자가 Readarr에 수정 또는 추가한 내용을 알려주는 업데이트 노트도 표시됩니다.

> 유지 보수 릴리스에는 버그 수정 및 기타 다양한 개선 사항이 포함됩니다. 자세한 내용은 커밋 기록을 참조하십시오.
{.is-info}

# 이벤트

- 이벤트 탭에서는 Readarr 내에서 발생한 이벤트를 표시합니다. 이를 통해 일부 경량 문제를 진단할 수 있습니다. 그러나 이는 로깅에서 설명한 추적 로그를 대체하지 않습니다.

> 이벤트는 INFO 로그와 동일합니다. {.is-info}

- 구성 요소 - 이 열은 Readarr 내에서 트리거된 구성 요소를 나타냅니다.
- 메시지 - 이 열은 이전 열에서 전송된 메시지를 나타냅니다.
- 기어 아이콘 - 이 옵션을 사용하면 페이지당 표시되는 구성 요소/메시지 수를 변경할 수 있습니다(기본값은 50입니다).
- 페이지 상단의 옵션
  - 새로 고침 - 이 옵션을 선택하면 현재 페이지가 새로 고쳐지고 새 이벤트 로그가 표시됩니다.
  - 지우기 - 이 옵션을 선택하면 현재 이벤트 로그가 지워지고 처음부터 시작할 수 있습니다.

# 로그 파일

- 이 페이지에서는 Readarr의 현재 사용 가능한 로그 파일을 다운로드하고 확인할 수 있습니다.

- 맨 위 행에는 로그 파일을 제어할 수 있는 여러 옵션이 있습니다.

- 가장 왼쪽 상단의 드롭다운에서 로그 파일과 업데이트 로그 파일로 전환할 수 있습니다.
  - 로그 파일 - 지원 문제의 필수 요소입니다. 로그 파일에 대한 자세한 내용은 여기에서 확인할 수 있습니다.
  - 업데이트 로그 파일 - Readarr의 업데이트 스크립트와 관련된 로그 파일을 표시합니다.

> Docker를 사용하는 경우 이 항목은 비어 있을 것입니다. 새 Docker 이미지를 다운로드하여 업데이트해야 합니다.
{.is-info}

- 새로 고침 - 이 옵션을 선택하면 현재 페이지가 새로 고쳐지고 새로 생성된 로그가 표시됩니다.
- 삭제 - 이 옵션을 선택하면 모든 로그가 지워지고 처음부터 시작할 수 있습니다.
- 파일 이름 - 이는 로그와 관련된 파일 이름을 표시합니다.
- 마지막 작성 - 이는 해당 로그 파일이 마지막으로 작성된 로컬 시간입니다.
  - Readarr은 각각 1MB로 제한된 롤링 로그 파일을 사용합니다. 현재 로그 파일은 항상 readarr.txt이며, 다음으로 최신 파일은 readarr.0.txt입니다(숫자가 높을수록 오래된 파일입니다. 총 51개의 로그 파일이 있습니다). 이 로그 파일에는 `fatal`, `error`, `warn`, `info` 항목이 포함됩니다.
  - 디버그 로그 레벨이 활성화되어 있는 경우, 추가적인 readarr.debug.txt 롤링 로그 파일이 있을 수 있으며, 최대 51개의 파일이 있습니다. 이 로그 파일에는 `fatal`, `error`, `warn`, `info`, `debug` 항목이 포함됩니다. 보통 약 40시간 정도를 커버합니다.
  - 추적 로그 레벨이 활성화되어 있는 경우, 추가적인 readarr.trace.txt 롤링 로그 파일이 있을 수 있으며, 최대 51개의 파일이 있습니다. 이 로그 파일에는 `fatal`, `error`, `warn`, `info`, `debug`, `trace` 항목이 포함됩니다. 추적 로그는 대부분 몇 시간 정도를 커버합니다.