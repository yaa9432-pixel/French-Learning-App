# Appelle-moi — iOS 패키징 (Capacitor)

웹앱(`www/`)을 iOS 앱으로 감싸는 프로젝트예요. **Mac + Xcode가 필요해요.**

## 1. 준비
`www/fonts/README.md`를 보고 글꼴 파일 4개를 넣으세요(없어도 동작은 해요).
`capacitor.config.json`의 `appId`를 본인 고유 값(예: `com.내이름.appellemoi`)으로 바꾼 뒤, Node.js가 설치된 상태에서:
```
npm install @capacitor/core @capacitor/ios @capacitor/local-notifications
npm install -D @capacitor/cli @capacitor/assets
npx cap add ios
npm run assets      # assets/ 의 아이콘·스플래시로 iOS 이미지 생성
npm run sync
npm run open        # Xcode 열기
```

## 2. Xcode에서
1. Signing & Capabilities → Team 선택(Apple Developer 계정), Bundle Identifier 확인
2. Info.plist에 `ITSAppUsesNonExemptEncryption` = NO 추가 (표준 HTTPS 외 자체 암호화 없음)
3. General → Version 1.0.0 / Build 1, iPhone 전용이면 iPad 해제
4. 시뮬레이터(6.7인치급 기기)에서 실행해 동작 확인 후 스크린샷 촬영(⌘S)
5. Product → Archive → Distribute App → App Store Connect

## 3. 이후는 `store/CHECKLIST.md` 참고

## 4. 개인정보 처리방침·지원 페이지 올리기 (`site/`)
1. GitHub에서 새 저장소를 만들고 `site/` 안의 `index.html`, `privacy.html`을 올려요.
2. Settings → Pages에서 배포 브랜치를 선택해요.
3. 주소가 `https://<아이디>.github.io/<저장소>/` 형태로 생기면, App Store Connect의 **지원 URL**에는 그 주소를, **개인정보 처리방침 URL**에는 `.../privacy.html`을 입력해요.

## 5. Mac이 없다면
iOS 빌드와 서명에는 macOS + Xcode가 필요해요. 방법은 둘 중 하나예요.
- **클라우드 Mac 빌드 서비스**(Codemagic, GitHub Actions의 macOS 러너 등)로 빌드·TestFlight 업로드를 맡기기
- **클라우드 Mac 대여**(원격으로 Mac을 빌려 위 1~2단계 진행)
Codemagic 방식은 `codemagic.yaml`과 `store/CODEMAGIC_GUIDE.md`에 단계별로 정리해 뒀어요.
어느 쪽이든 Apple Developer 계정과 서명 인증서가 필요해요. 요금과 무료 한도는 각 서비스 사이트에서 확인하세요.
