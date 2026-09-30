# JAYU PET Dental Wipes Game — Final Release Archive

이 폴더는 2026-08-07 기준 Vercel 최종 배포본을 독립적으로 보관하기 위해 정리한 실행 패키지입니다.

- 배포 URL: https://deploy-iota-lilac-47.vercel.app/
- 기준 코드: `index.html`
- 구조: 빌드 과정이 없는 단일 HTML/CSS/JavaScript 모바일 웹 게임
- 런타임 파일: 이미지 16개, 오디오 7개
- 원본 배포 코드 SHA-256: `D65C1B468BC2993086325289CEBB2E8DFBC486F689234F37A81F8D5CB67F58E3`
- 현재 `index.html`은 에셋 폴더 분리 경로를 반영한 정리본이므로 원본 배포 코드와 해시는 다릅니다.

## 처음 업무를 이어받는 경우

1. 회사 GitHub 저장소를 Clone하거나 ZIP으로 내려받습니다.
   - <https://github.com/grassmedimkt/jayupet-dental-wipe-game>
2. 이 README와 `ASSET-LIST.md`, `LICENSES.md`를 먼저 확인합니다.
3. 아래 실행 방법에 따라 로컬에서 게임을 확인합니다.
4. 수정 전 로컬 실행 화면과 현재 배포본을 비교합니다.
5. 수정이 끝나면 회사 Vercel 계정에서 GitHub 저장소를 Import해 배포합니다.
6. 배포 후 모바일 게임 진행, 이미지·오디오, Amazon 이동 및 Meta Pixel을 확인합니다.
7. 정상 작동하는 새 Production URL을 인수인계 노션에 기록합니다.

## 실행 방법

오디오와 브라우저 보안 정책 때문에 `index.html`을 파일로 직접 여는 대신 로컬 HTTP 서버로 실행하는 것을 권장합니다.

### Windows PowerShell

```powershell
cd "다운로드한 jayupet-dental-wipe-game 폴더의 전체 경로"
python -m http.server 4173
```

`python`이 인식되지 않으면 `py -m http.server 4173`을 사용합니다.

### macOS·Linux

```bash
cd "/다운로드한/jayupet-dental-wipe-game/폴더"
python3 -m http.server 4173
```

브라우저에서 `http://127.0.0.1:4173/`을 엽니다. `127.0.0.1`은 서버를 실행한 컴퓨터에서만 접속할 수 있으며 터미널을 닫으면 서버도 종료됩니다.

## 폴더 구성

```text
.
├─ index.html              최종 게임 코드
├─ asset/
│  ├─ images/             Dropbox 이미지 업로드용 16개
│  └─ audio/              Dropbox 오디오 업로드용 7개
├─ ASSET-LIST.md           에셋별 용도
├─ LICENSES.md             권리·출처 확인 기록
└─ SHA256SUMS.txt          전체 파일 무결성 체크섬
```

## 게임 흐름

메인 화면 → 구강 화면 → 제품 소개·선택 → 듀얼 핑거 와이프 착용 → 파란 3D 돌기면 세정 → 흰색 엠보싱 면 마무리 → 완료 → 선택 제품 Amazon CTA

## 주요 수정 위치

- 게임 화면·로직·문구: `index.html`
- 이미지: `asset/images/`
- 오디오: `asset/audio/`
- 제품별 Amazon 링크: `index.html`의 `amazonUrl`
- Meta Pixel ID: `fbq('init', '...')`와 `<noscript>`의 `tr?id=...`
- 에셋별 파일명과 사용 위치: `ASSET-LIST.md`
- 이미지·음원 권리 및 출처: `LICENSES.md`

## 배포 시 주의사항

- `.vercel/project.json`은 기존 Vercel 프로젝트 `deploy`에 연결된 정보입니다. 다른 계정이나 프로젝트에 배포할 때는 그대로 사용하지 말고 새로 연결합니다.
- `index.html`에는 Meta Pixel ID와 제품별 Amazon Attribution URL이 포함되어 있습니다.
- Amazon 링크와 Meta Pixel 사용 승인이 현재도 유효한지 재배포 전에 확인합니다.
- MP3 파일의 재배포 권리는 `LICENSES.md`의 확인 항목을 완료한 후 판단합니다.
- 현재 로컬 경로는 `asset/images/...`와 `asset/audio/...`로 설정되어 있습니다.
- GitHub의 `asset` 폴더는 실제 게임 실행에 사용하고, Dropbox는 이미지·오디오 원본의 별도 백업으로 사용합니다. 일반적인 Vercel 배포에서는 현재 상대 경로를 그대로 유지합니다.
- 에셋을 GitHub에서 분리해 운영하기로 결정한 경우에만 Dropbox 직접 접근 URL 또는 CDN URL로 경로를 교체합니다. 일반 Dropbox 공유 페이지 URL은 웹 에셋 URL로 사용할 수 없습니다.
- 파일명이나 폴더 구조를 바꾸면 `index.html`의 경로도 함께 수정해야 합니다.

## 회사 계정으로 재배포할 때

향후 배포 담당자는 이 README의 실행 방법과 배포 시 주의사항을 먼저 확인합니다.

1. 회사 GitHub 저장소 `grassmedimkt/jayupet-dental-wipe-game`을 회사 Vercel 계정에서 Import합니다.
2. Framework Preset은 `Other`를 선택하고, Build Command와 Output Directory는 비워둡니다.
3. 기존 개인 계정의 `.vercel/project.json`은 재사용하지 않습니다.
4. 배포 전에 `index.html`의 **Meta Pixel ID를 회사에서 계속 사용할 수 있는 활성 Pixel ID로 반드시 확인·교체**합니다.
5. Meta Pixel ID는 `fbq('init', '...')`와 `<noscript>`의 `tr?id=...` 두 위치에 동일하게 반영합니다.
6. 제품 3종의 Amazon Attribution URL이 유효한지도 확인합니다.
7. 배포 후 이미지 16개, 오디오 7개, 모바일 게임 진행, Meta Pixel 이벤트, Amazon 이동을 점검합니다.
8. 정상 작동을 확인한 Production URL을 인수인계 노션에 기록합니다.

현재 정리본에 포함된 Meta Pixel ID는 `1354831389950247`입니다. 이 값이 개인 계정 또는 기존 자산에 연결되어 있다면 회사 소유 Pixel ID로 교체한 뒤 배포해야 합니다.

## 배포 후 확인

- 첫 화면과 제품 선택 화면이 정상적으로 표시되는가
- 이미지 16개가 누락되거나 깨지지 않는가
- 오디오 7개가 사용자의 첫 클릭·터치 이후 재생되는가
- 와이프 착용부터 양면 세정과 완료 화면까지 진행되는가
- 제품 3종의 Amazon 버튼이 올바른 상품으로 연결되는가
- Meta Pixel의 PageView와 게임 이벤트가 수집되는가
- 모바일 Safari와 Chrome에서 정상 작동하는가

## 관련 자료

- GitHub: <https://github.com/grassmedimkt/jayupet-dental-wipe-game>
- 현재 배포본: <https://deploy-iota-lilac-47.vercel.app/>
- [Dropbox 이미지·오디오 백업](https://www.dropbox.com/work/GTEP%20INU/%EB%8D%B4%ED%83%88%EC%99%80%EC%9D%B4%ED%94%84%20%EB%AF%B8%EB%8B%88%EA%B2%8C%EC%9E%84%20%EC%9D%B4%EB%AF%B8%EC%A7%80%2C%20%EC%98%A4%EB%94%94%EC%98%A4%20%EB%B0%B1%EC%97%85%EB%B3%B8)
- [업무 및 성과 기록](https://app.notion.com/p/3acd6c2c7d9d8069a9c5dcc42092c184)

## 보관 기준

후보 이미지, 후보 BGM/SFX, 편집 소스와 광고 크리에이티브는 제외했습니다. 이 폴더에는 최종 배포 페이지가 실제로 참조하는 런타임 파일만 들어 있습니다.
