# IRIS Version 1.5_Close Beta

# IRIS Close Beta 안내

이 문서는 IRIS Close Beta 테스터를 위한 사용 안내서입니다. IRIS는 Windows 데스크톱에서 음성/텍스트 대화, 짧은 문장 번역, 회의 보조, 화면 설명, 장치 확인, 진단 자료 수집을 돕는 AI 어시스턴트입니다.

현재 Close Beta는 최종 제품이 아니며, v1.5 패키징 단계입니다. 문제가 발생하면 이 문서의 “문제 발생 시 전달할 정보” 섹션을 참고해 안전하게 공유해주세요.

## 포함된 주요 기능

- Live conversation: IRIS와 음성 또는 텍스트로 대화합니다.
- Translation Mode: 짧은 문장/발화 단위 번역을 수행합니다.
- Translation 출력 방식:
  - `자막`
  - `음성`
  - `자막 + 음성`
- Translation 번역 모델:
  - `기본 번역 — Flash`
  - `정밀 번역 — Pro`
  - `빠른 번역 — Flash-Lite`
- Translation 음성 모델:
  - `기본 음성 — Flash TTS`
  - `고품질 음성 — Pro TTS`
- 번역 스타일/프리셋, 번역 방향 설정:
  - 자동
  - 한국어 → 영어
  - 영어 → 한국어
- 별도 자막창:
  - `자막창 사용`
  - `자막창 테스트 표시`
  - `자막창 위치 초기화`
- 번역 결과 복사:
  - 자막창이 켜져 있어도 `복사` 버튼은 최신 성공 번역 결과를 복사합니다.
- Meeting Assistant
- Screen Assistant
- Device Check
- Zoom/Webex Helper
- System / Diagnostics:
  - `Check Connection`
  - `Open Logs Folder`
  - `Open Output Folder`
  - `Open Settings Folder`
  - `Copy Diagnostics`
  - `Create Support Bundle`
  - `Restart IRIS`
  - `Exit IRIS`

## 실행 전 준비사항

- Windows PC
- 인터넷 연결
- Gemini API 키
- 마이크 권한, 화면 캡처 권한 등 필요한 OS 권한
- Close Beta용 IRIS 실행 파일 또는 소스 실행 환경

주의:

- API 키를 스크린샷, 채팅, 이슈 보고서에 포함하지 마세요.
- 백신/보안 기능을 끄거나 예외 처리하라고 안내하지 않습니다. 문제가 있으면 증상과 진단 정보를 공유해주세요.
- 기존 Jarvis 이름이 내부 파일이나 클래스에 남아 있을 수 있지만, 사용자에게 보이는 제품명은 IRIS입니다.

## 실행 방법

패키지된 Close Beta를 받은 경우:

1. 제공된 IRIS 폴더를 엽니다.
2. `IRIS.exe`를 실행합니다.
3. Windows 보안 또는 권한 안내가 나오면 내용을 확인한 뒤 진행합니다.

소스 테스트 환경에서 실행하는 경우:

```powershell
cd "C:\Users\asdf7\Desktop\기획\DX\IRIS"
C:\IRIS_BUILD\IRIS\.venv-packaging\Scripts\python.exe main.py
```

참고:

- 현재 문서는 Close Beta 사용 안내이며, Inno/MSIX 설치 프로그램 안내가 아닙니다.
- 이 단계에서는 PyInstaller 빌드나 ZIP 배포를 다루지 않습니다.

## API 키 설정

처음 실행 시 설정이 필요하면 First Run Setup 또는 Settings에서 Gemini API 키를 입력합니다.

- API 키 저장 위치: `%APPDATA%\IRIS`
- API 키는 진단 화면에서 값이 표시되지 않고, 설정 여부만 표시됩니다.
- `Check Connection`으로 API 키와 선택한 번역 모델 상태를 확인할 수 있습니다.

API 키가 없거나 잘못된 경우 Translation, Live conversation, 일부 진단 기능이 정상 동작하지 않을 수 있습니다.

## Translation Mode 사용법

Translation Mode는 짧은 문장 또는 짧은 발화 단위 번역을 위한 기능입니다. 문서 전체 번역이나 긴 글 번역 기능이 아닙니다.

기본 명령:

- 켜기: `번역 모드 켜`
- 끄기: `번역 모드 꺼`
- 상태 확인: `번역 상태 알려줘`

입력 길이 정책:

- 0–500자: 일반 빠른 경로입니다.
- 501–800자: 번역은 진행되지만 `긴 문장 번역 중...` 상태가 표시될 수 있습니다.
- 801자 이상: 실시간 번역 모드에는 긴 입력으로 보고 차단됩니다.

801자 이상 입력 시 안내:

```text
입력이 실시간 번역 모드에는 긴 편입니다. 짧은 문장 단위로 나누어 번역해주세요.
```

중요한 안전 동작:

Translation Mode가 켜져 있으면 명령처럼 보이는 문장도 “번역할 내용”으로 처리됩니다. 즉, 아래 문장은 실행되지 않고 번역됩니다.

- `회의 시작해`
- `Zoom 열어줘`
- `현재 대통령 누구야`
- `마이크 확인해줘`
- `IRIS 종료해`

이 동작은 회의 시작, 앱 종료, 장치 조작 같은 명령이 번역 중 실수로 실행되지 않도록 막기 위한 안전 기능입니다.

## 자막창 사용법

Settings에서 `자막창 사용`을 켜면 번역 결과가 별도 floating subtitle window에 표시됩니다.

- `자막창 테스트 표시`: Gemini API나 TTS를 호출하지 않고 테스트 문구를 표시합니다.
- `자막창 위치 초기화`: 자막창 위치와 크기를 안전한 기본값으로 되돌립니다.
- 자막창을 직접 이동하거나 크기를 바꾸면 다음 번역에서도 위치/크기가 유지됩니다.
- 자막창을 닫아도 `자막창 사용` 설정은 꺼지지 않습니다. 다음 번역이 성공하면 마지막 위치에서 다시 열립니다.
- Translation Mode를 끄면 자막창은 숨겨지고 내용이 정리됩니다.

자막창이 켜져 있을 때:

- floating subtitle window가 번역 결과의 주 표시 영역입니다.
- 메인 UI는 `번역 완료`, `자막창에 표시됨` 같은 상태만 표시할 수 있습니다.
- `복사` 버튼은 상태 문구가 아니라 최신 성공 번역 결과를 복사합니다.

자막창이 꺼져 있을 때:

- 출력 방식에 따라 메인 UI에 번역 결과가 표시됩니다.

## Meeting Assistant 사용법

Meeting Assistant는 로컬 마이크 녹음을 기반으로 회의 보조 작업을 수행합니다.

대표 명령:

- `회의 상태 알려줘`
- `회의 시작해`
- `회의 끝내`
- `회의록 만들어줘`

동작:

- 녹음 출력은 `Desktop\IRIS\Meetings` 아래에 저장됩니다.
- 회의를 끝내면 기존 동작에 따라 transcript, summary, draft minutes, action items 등이 생성될 수 있습니다.
- Translation Mode가 켜져 있으면 회의 관련 문장도 번역 내용으로 처리되므로 회의 명령이 실행되지 않습니다.

지원하지 않는 항목:

- 시스템 오디오 녹음
- 화자 분리
- Zoom/Webex 회의 자체 녹화
- 캘린더 연동
- 자동 회의 참가

## Screen Assistant 사용법

대표 명령:

- `이 화면 설명해줘`

Screen Assistant는 현재 화면을 설명하는 기능입니다. 화면 캡처 권한이나 환경에 따라 안전한 실패 메시지가 표시될 수 있습니다.

Translation Mode가 켜져 있으면 `이 화면 설명해줘`도 실행 명령이 아니라 번역할 내용으로 처리됩니다.

## Device Check 사용법

대표 명령:

- `마이크 확인해줘`
- `카메라 확인해줘`

Device Check는 Zoom/Webex 키워드 없이도 마이크와 카메라 상태를 확인할 수 있습니다. 장치를 사용할 수 없거나 권한이 부족하면 안전한 안내가 표시됩니다.

Translation Mode가 켜져 있으면 장치 확인 명령도 번역할 내용으로 처리됩니다.

## Zoom/Webex Helper 사용법

대표 명령:

- `Zoom 열어줘`
- `Webex 열어줘`

Zoom/Webex Helper는 Zoom 또는 Webex가 명시적으로 언급된 경우에만 해당 보조 경로를 사용합니다.

지원하지 않는 항목:

- 회의 예약
- 자동 참가
- 회의 링크 자동 처리
- Zoom/Webex 내부 회의 녹음

## System / Diagnostics 사용법

System 탭에는 진단과 앱 제어 기능이 있습니다.

- `Check Connection`: API 키와 선택된 Translation 모델의 사용 가능 여부를 확인합니다.
- `Open Logs Folder`: 로그 폴더를 엽니다.
- `Open Output Folder`: IRIS 출력 폴더를 엽니다.
- `Open Settings Folder`: 설정 폴더를 엽니다. API 키 파일을 직접 열지는 않습니다.
- `Copy Diagnostics`: 진단 요약을 클립보드에 복사합니다.
- `Create Support Bundle`: 지원 요청용 진단 묶음을 생성합니다.
- `Restart IRIS`: IRIS를 재시작합니다. 기존 확인 동작을 따릅니다.
- `Exit IRIS`: IRIS를 종료합니다. 기존 확인 동작을 따릅니다.

`Check Connection` 결과는 간단한 범주로 표시됩니다.

- `사용 가능`
- `API 키 없음`
- `인증/권한 확인 필요`
- `요청 한도 도달`
- `네트워크 확인 필요`
- `모델 사용 불가`
- `응답 지연`
- `공급자 오류`
- `테스트하지 않음`

Pro 또는 Flash-Lite 모델이 계정/프로젝트에서 제공되지 않으면 다음과 같은 안내가 표시될 수 있습니다.

```text
정밀 번역 모델을 현재 사용할 수 없습니다. 기본 번역 모델을 선택해주세요.
```

```text
빠른 번역 모델을 현재 사용할 수 없습니다. 기본 번역 모델을 선택해주세요.
```

## Settings 사용법

Settings 탭의 제목은 `번역 모드 설정`입니다.

설정 가능한 항목:

- Translation text model
- Translation TTS model
- Translation preset/style
- Translation direction
- Translation output mode
- `자막창 사용`

출력 방식:

- `자막`: 번역 결과를 자막/텍스트로 표시합니다. TTS가 없어 가장 빠릅니다.
- `음성`: 번역 음성을 재생합니다. 자막창 사용이 켜져 있으면 보조 자막도 표시될 수 있습니다.
- `자막 + 음성`: 번역 결과를 먼저 표시하고 이후 음성을 재생합니다.

버튼:

- `Save Translation Settings`: 현재 선택을 저장합니다.
- `Reload`: 디스크의 설정을 다시 불러옵니다.
- `Reset Translation Settings`: Translation 설정을 기본값으로 되돌립니다.
- `자막창 테스트 표시`: 안전한 테스트 자막을 표시합니다.
- `자막창 위치 초기화`: 자막창 위치/크기만 초기화합니다.

Reset Translation Settings는 API 키, 사용자 출력 파일, 회의 파일, 로그, unrelated settings를 삭제하지 않습니다.

## 저장 위치

IRIS는 설정과 사용자 출력 위치를 분리합니다.

- 설정/API 키: `%APPDATA%\IRIS`
- 사용자 출력 루트: `Desktop\IRIS`
- 회의 출력: `Desktop\IRIS\Meetings`
- 로그: `Desktop\IRIS\Logs`
- 문서 출력: `Desktop\IRIS\Documents`
- 내보내기 출력: `Desktop\IRIS\Exports`
- 스크린샷 출력: `Desktop\IRIS\Screenshots`

IRIS는 기본적으로 일반 사용자 권한으로 실행되도록 설계되어 있습니다. 설정/API 키를 Program Files 같은 시스템 보호 폴더에 저장하지 않습니다.

## 개인정보 및 보안 안내

- API 키를 이슈 보고서, 스크린샷, 채팅, 문서에 포함하지 마세요.
- 회의 녹음, 회의록, 문서, 스크린샷은 민감한 정보를 포함할 수 있습니다. 공유 전 내용을 확인하세요.
- Support Bundle은 민감정보를 제외하도록 설계되어 있습니다.
- Support Bundle에는 다음이 포함되지 않아야 합니다.
  - API 키
  - raw settings
  - 녹음 파일
  - transcript / minutes / meeting outputs
  - screenshots
  - documents / user files
  - Translation source/result text
  - subtitle content
  - latest translation copy payload
- 가능하면 Support Bundle도 공유 전 직접 확인해주세요.
- Translation Session Log는 구현되어 있지 않습니다.
- 자동 Translation logging도 구현되어 있지 않습니다.

## 알려진 제한사항

- Close Beta 빌드이며 최종 제품이 아닙니다.
- 기본 번역 모델인 Flash 사용을 권장합니다.
- Pro와 Flash-Lite는 API 키, 계정, 프로젝트, 모델 제공 상태에 따라 사용할 수 없을 수 있습니다.
- Translation Mode는 문장/짧은 발화 중심이며 긴 문서 번역용이 아닙니다.
- 실시간 스트리밍 동시통역 기능은 아닙니다.
- 801자 이상의 긴 입력은 차단됩니다.
- TTS는 자막 표시보다 느릴 수 있습니다.
- Pro 모델은 더 느리거나 사용할 수 없을 수 있습니다.
- Flash-Lite 모델도 계정/모델 지원 상태에 따라 사용할 수 없을 수 있습니다.
- Meeting Assistant는 로컬 마이크 녹음 기반입니다.
- 시스템 오디오 녹음은 지원하지 않습니다.
- 화자 분리는 지원하지 않습니다.
- Zoom/Webex 자동 참가, 스케줄링, 링크 자동화는 지원하지 않습니다.
- RAG/Hermes는 v1.5 Close Beta에 포함되지 않습니다.
- 자동 업데이트는 지원하지 않습니다.
- 앱을 종료하면 메모리에만 있던 최신 번역 복사 대상은 사라집니다.

## 문제 발생 시 전달할 정보

이슈를 보고할 때는 가능한 한 아래 항목을 포함해주세요.

- Windows 버전
- IRIS 버전/빌드
- source 실행인지 packaged 실행인지
- 사용한 명령 또는 클릭한 버튼
- 기대한 동작
- 실제 동작
- Translation Mode가 ON이었는지 OFF였는지
- 번역 문제인 경우:
  - 선택한 Translation 모델
  - 출력 방식: `자막`, `음성`, `자막 + 음성`
  - 자막창 사용 여부
- 안전한 경우 스크린샷
- 안전한 경우 `Copy Diagnostics` 결과
- 안전한 경우 Support Bundle

절대 포함하지 말아야 할 것:

- API 키
- 비공개 회의 녹음
- 민감한 회의록/문서
- 개인 정보가 담긴 화면 전체 스크린샷
- 번역 원문/결과 중 공유하면 안 되는 내용

## 빠른 테스트 체크리스트

- [ ] IRIS 실행
- [ ] `Check Connection`
- [ ] `번역 모드 켜`
- [ ] 짧은 문장 번역
- [ ] `자막창 사용` ON/OFF
- [ ] 출력 방식 `자막`
- [ ] 출력 방식 `음성`
- [ ] 출력 방식 `자막 + 음성`
- [ ] `복사` 버튼이 실제 번역 결과를 복사하는지 확인
- [ ] 501–800자 입력에서 `긴 문장 번역 중...` 확인
- [ ] 801자 이상 입력 차단 확인
- [ ] `번역 모드 꺼`
- [ ] `회의 상태 알려줘`
- [ ] `회의 시작해` / `회의 끝내`
- [ ] `마이크 확인해줘`
- [ ] `카메라 확인해줘`
- [ ] `이 화면 설명해줘`
- [ ] `Zoom 열어줘`
- [ ] `Webex 열어줘`
- [ ] `Copy Diagnostics`
- [ ] `Create Support Bundle`
- [ ] `Restart IRIS` 확인 동작
- [ ] `Exit IRIS` 확인 동작

