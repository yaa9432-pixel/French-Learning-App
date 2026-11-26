# Mac 없이 iOS 앱 올리기 (Codemagic) — 단계별

화면 문구는 바뀔 수 있어요. 막히면 해당 화면 캡처를 보여 주세요.

## A. Apple 쪽 준비 (iPhone/웹으로 가능)
1. **Apple Developer Program 가입** — developer.apple.com (Apple ID 2단계 인증 필요, 승인에 며칠 걸릴 수 있어요)
2. developer.apple.com → Certificates, IDs & Profiles → **Identifiers**에서 App ID 등록 (Bundle ID = `capacitor.config.json`의 appId와 동일)
3. **App Store Connect**(appstoreconnect.apple.com) → 앱 → + → 새로운 앱 만들기 (이름, 언어 한국어, Bundle ID, SKU). 만든 뒤 **앱 정보의 Apple ID(숫자)**를 `codemagic.yaml`의 ③에 입력
4. App Store Connect → 사용자 및 액세스 → 통합 → **App Store Connect API 키 생성**, 권한은 **App Manager**. `.p8`는 **한 번만** 받을 수 있으니 안전하게 보관하고, Issuer ID·Key ID를 메모

## B. 코드 올리기
5. GitHub 새 저장소(비공개 가능)에 `appelle-moi-ios` 폴더의 **내용**을 올려요. `codemagic.yaml`이 저장소 맨 위에 있어야 해요. (`site/` 폴더는 별도 저장소/Pages로 써도 돼요)
6. `capacitor.config.json`의 `appId`와 `codemagic.yaml`의 ②를 같은 고유 값으로 바꿔요.

## C. Codemagic 설정
7. codemagic.io 가입 → GitHub 연결 → 저장소 추가 (codemagic.yaml 사용 선택)
8. Team settings → Integrations(Developer Portal) → **API 키 등록**: 이름을 `appellemoi_key`로, Issuer ID·Key ID·`.p8` 입력
9. 코드 서명: Codemagic 문서의 "Signing iOS apps"를 따라 App Store 배포용 인증서를 만들거나 가져와요 (API 키로 자동 관리 가능)
10. **Start new build** → 워크플로 `Appelle-moi iOS` 선택

## D. 테스트·제출
11. 빌드가 끝나면 TestFlight에 올라가요. iPhone의 TestFlight 앱으로 설치해 **알림 권한·예약, 검색, 오프라인 동작**을 직접 확인하세요.
12. App Store Connect에서 스크린샷, 설명(`listing-ko.md`), 개인정보 처리방침 URL, 지원 URL, 가격, App Privacy 입력 → 빌드 선택 → **심사 제출**
- 스크린샷은 iPhone 6.9형 또는 6.5형 크기(예: 1290×2796)가 필요해요. Mac이 없으니 본인 iPhone 캡처가 규격에 안 맞으면 알려 주세요.

## 자주 막히는 곳
- 서명 실패 → Bundle ID 불일치, 인증서·프로필 미생성
- 업로드 실패 → App Store Connect에 앱 레코드가 없거나 API 키 권한 부족
- 빌드 번호 중복 → 이 설정은 Codemagic 빌드 번호를 자동으로 써서 올라가요
