# 맥한영 · MacHanYoung 1.01
사과공방 · Apple Craft / 개발자 최귀동
© 2026 Apple Craft. All rights reserved.

macOS 13 이상, Apple Silicon 및 Intel. Karabiner 없이 동작합니다.

## 다운로드
[맥한영 1.01 DMG 다운로드](https://github.com/Choikuidong/MacHanYoung/releases/download/v1.01/MacHanYoung-1.01.dmg)

[릴리스와 소스 ZIP](https://github.com/Choikuidong/MacHanYoung/releases/latest)

전체 소스는 MacHanYoung-1.01-Source.zip에 포함되어 있습니다. 압축을 해제하면 Sources, Resources, Scripts, Tests 및 build.sh가 있습니다.

## 시작하기
DMG의 맥한영.app을 응용 프로그램에 옮긴 뒤 실행합니다.
기존 앱을 먼저 종료하세요. 키보드 권한을 허용한 뒤 ‘Windows 사용자 추천 설정 적용’을 누릅니다.
Ctrl 단축키·키 배치·한영·한자 전환·로그인 자동 실행과 마우스 휠 반전을 켭니다.
팝업 선호는 보존하고 트랙패드 반전은 끕니다. 표준 기능 키 설정은 별도로 선택합니다.
세부 항목은 항상 표시됩니다. 창 가장자리를 드래그해 크기를 바꾸고, 스크롤해 아래 항목을 조정할 수 있습니다. 기존 사용자의 설정은 자동으로 덮어쓰지 않습니다.

## 스크롤 방향
현재 macOS 방향을 기준으로 반전합니다. 앱 종료 시 원래 방향으로 돌아옵니다.
일반 휠(비연속)과 트랙패드(연속) 이벤트를 구분합니다. 부드러운 스크롤을 보내는 일부 마우스와 Magic Mouse는 트랙패드 옵션을 따를 수 있습니다.
장치 모델을 식별하는 방식은 아닙니다. 외장 키보드 한정 옵션은 스크롤에는 적용되지 않습니다.

## 1.01 정정본
- 관하여 버전과 파일 버전을 1.01로 통일
- 사과공방 표기와 https://applecraft.kr/ 링크 추가

## 이전 기능 변경
- 모든 세부 설정을 항상 표시하고 접기/펼치기 제거
- 설정 창 크기 조절, 줄바꿈, 세로 스크롤 및 창 크기 기억
- 업데이트 후 기존 권한 요청 기록 때문에 새 권한 안내가 생략되는 문제 수정
- 키보드 권한 미연결 시 메뉴와 설정에 복구 절차 표시; 승인 후 입력 필터 자동 재시도
- 표시 버전 1.01, 내부 빌드 31

## 1.1 변경
- 추천 설정과 접고 펼치는 세부 설정, 작은 화면용 스크롤 지원
- 마우스·트랙패드 유형별 스크롤 반전, 가로·세로 및 관성 값 보존
- 앱 활성화 시 동기 장치 조회 제거, 변함없는 설정 UI/메뉴 재생성 생략
- 한영 전환 경로의 중복 소스 읽기와 설정 저장 제거
- 표시 버전 1.1, 내부 빌드 29

## 빌드 및 검사
macOS와 Xcode Command Line Tools가 필요합니다.
```sh
zsh build.sh
./맥한영.app/Contents/MacOS/WinKeys --self-test
./맥한영.app/Contents/MacOS/WinKeys --integration-test
./맥한영.app/Contents/MacOS/WinKeys --layout-test
swiftc -parse-as-library Sources/Preferences.swift Sources/ScrollTransformer.swift Tests/Scroll/main.swift -o /tmp/machanyoung-scroll-tests
/tmp/machanyoung-scroll-tests
```
팝업 검사는 앱 종료 후 `--popup-test`로 실행합니다.
통합 검사는 실제 입력 소스를 변경한 뒤 원래 소스로 복원합니다.
자동 검사만으로 모든 앱·물리 키보드·마우스의 실제 동작을 보증하지 않습니다.

## 업데이트 후 한영 전환이 안 될 때
현재 배포는 임시(ad-hoc) 서명으로, 파일이 바뀌면 macOS가 이전 키보드 권한을 새 실행 파일에 연결하지 않을 수 있습니다.
시스템 설정 → 개인정보 보호 및 보안 → 손쉬운 사용(macOS 27에서는 ‘기기 제어 및 데이터 접근’)에서 기존 맥한영 항목을 삭제한 뒤,
+ 버튼으로 /Applications/맥한영.app을 추가하고 켜세요. 승인 후 앱은 자동으로 입력 필터를 다시 시작합니다.
암호 입력은 macOS 창에서 직접 진행합니다. 권한을 우회하거나 보안 기능을 끄지 않습니다.

## 배포
유효한 Developer ID가 있으면 `MACHANYOUNG_SIGNING_IDENTITY`를 지정해 동일한 인증서로 계속 서명하세요.
외부 배포에는 별도 Apple 공증과 stapling이 필요합니다. 이 빌드에는 인증서나 비밀 키가 포함되지 않습니다.
임시 서명 빌드이며 Apple Developer ID 공증은 없습니다. 업데이트 후 기존 키보드 권한을 제거하고 새 앱을 다시 추가해야 할 수 있습니다.
GitHub에 소스를 올릴 때 이 폴더를 사용하고, DMG는 Releases 첨부 파일로 올리세요.
소스 공개와 오픈소스 라이선스 부여는 별개입니다. 별도 라이선스는 부여하지 않았습니다.
