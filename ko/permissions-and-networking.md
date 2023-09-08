# 네트워크 문제 해결 가이드

- 대부분의 문제 해결에는 `curl`이 필요합니다.
- SSL의 경우 문제 해결에는 `openssl`이 필요합니다.

## SSL 문제

- curl은 \*Arr와 같이 SSL 인증서를 확인하지 않으므로 openssl을 사용해야 합니다.

- openssl을 사용하여 연결/사이트를 테스트하여 인증서가 유효한지 확인합니다.

```bash
openssl s_client -showcerts -connect <url>:443
```

## 연결할 수 없는 IPv6 IP

- curl을 사용하여 연결을 테스트합니다.

```bash
curl -sv -6 "http://<url>:<port>/"
```

## Windows에서 사용 중인 포트 확인

- netsh를 사용하여 사용 중인 포트와 해당 포트를 사용하는 프로그램 목록을 가져옵니다.

```bash
netstat -ab
```

## Windows URL 예약 확인

- netsh를 사용하여 앱이 바인딩되고 수신 대기 중인 포트와 URL 목록을 가져옵니다.

```bash
netsh http show urlacl
```

## Windows URL 예약 생성

- netsh를 사용하여 urlacl을 생성합니다. 아래 예제는 포트 `7878`을 사용하는 radarr을 위한 것입니다.

```bash
http add urlacl http://*:7878/ sddl=D:(A;;GX;;;S-1-1-0)
```

## Linux에서 사용 중인 포트 확인

- netstat을 사용하여 사용 중인 포트를 찾거나 앱이 어떤 포트를 사용하는지 확인합니다.

```bash
sudo netstat -tnlp | grep <:port or app>
```

### 예제

- 포트 `8989`

```bash
sudo netstat -tnlp | grep ':8989'
```

- 이름이 `Radarr`인 앱

```bash
sudo netstat -tnlp | grep 'Radarr'
```