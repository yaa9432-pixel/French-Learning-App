# Appelle-moi

프랑스어 초급 학습용 단일 HTML 앱입니다. 별도 빌드나 서버 없이 무료 GitHub Pages에 공개할 수 있습니다.

## 무료로 공개하기

1. GitHub에서 새 **Public repository**를 만듭니다.
2. 저장소의 **Settings → Pages → Build and deployment → Source**에서 **GitHub Actions**를 선택합니다.
3. 이 폴더에서 터미널을 열고 아래 명령을 실행합니다. `USERNAME`과 `REPOSITORY`는 본인의 GitHub 계정과 저장소 이름으로 바꿉니다.

```powershell
git init -b main
git add index.html README.md .github/workflows/deploy.yml
git commit -m "Deploy Appelle-moi"
git remote add origin https://github.com/USERNAME/REPOSITORY.git
git push -u origin main
```

4. 저장소의 **Actions** 탭에서 `Deploy Appelle-moi` 작업이 완료될 때까지 기다립니다.
5. 앱은 `https://USERNAME.github.io/REPOSITORY/` 주소에서 열립니다.

이후 `main` 브랜치에 변경 사항을 푸시할 때마다 자동으로 다시 배포됩니다. GitHub Pages는 정적 웹 호스팅이므로 앱은 서버나 유료 호스팅 없이 실행되며, 학습 진도는 각 사용자의 브라우저에 저장됩니다.