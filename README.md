# Spine Portfolio - GitHub Pages 템플릿

스파인 애니메이션을 GitHub Pages로 호스팅하고, Notion 포트폴리오에 임베드할 수 있는 템플릿입니다.

---

## 폴더 구조

```
spine-portfolio/
├── player.html          ← 스파인 플레이어 (Notion 임베드용)
├── index.html           ← 갤러리 페이지 (선택)
├── README.md
└── animations/          ← 여기에 스파인 파일을 넣으세요
    ├── 캐릭터1/
    │   ├── 캐릭터1.json
    │   ├── 캐릭터1.atlas
    │   └── 캐릭터1.png
    ├── 캐릭터2/
    │   ├── 캐릭터2.json
    │   ├── 캐릭터2.atlas
    │   └── 캐릭터2.png
    └── ...
```

**중요:** 각 폴더 안의 `.json`, `.atlas` 파일명이 폴더명과 동일해야 합니다.
예: `hero/` 폴더 → `hero.json`, `hero.atlas`, (텍스처 png)

---

## 설정 방법 (5단계)

### 1단계: GitHub 저장소 만들기
1. [github.com](https://github.com) 에서 **New Repository** 클릭
2. 이름: `spine-portfolio` (원하는 이름으로)
3. **Public** 선택 (GitHub Pages 무료 사용을 위해)
4. **Create repository** 클릭

### 2단계: 파일 업로드
1. 저장소 페이지에서 **Add file → Upload files** 클릭
2. `player.html`, `index.html` 업로드
3. **Commit changes** 클릭
4. `animations` 폴더를 만들고 스파인 파일들을 업로드
   - **Add file → Upload files** 에서 폴더째 드래그 앤 드롭 가능

### 3단계: GitHub Pages 활성화
1. 저장소 → **Settings** 탭
2. 왼쪽 메뉴에서 **Pages** 클릭
3. Source: **Deploy from a branch** 선택
4. Branch: **main** / **/ (root)** 선택
5. **Save** 클릭
6. 몇 분 후 URL이 생성됩니다:
   `https://유저이름.github.io/spine-portfolio/`

### 4단계: 동작 확인
브라우저에서 아래 URL을 열어 확인하세요:
```
https://유저이름.github.io/spine-portfolio/player.html?name=캐릭터폴더명
```

### 5단계: Notion에 임베드
1. Notion 페이지에서 `/embed` 입력
2. URL 입력:
   ```
   https://유저이름.github.io/spine-portfolio/player.html?name=캐릭터폴더명
   ```
3. 원하는 크기로 조절

---

## URL 파라미터 옵션

| 파라미터 | 설명 | 기본값 | 예시 |
|---------|------|--------|------|
| `name` | animations/ 아래 폴더명 (필수) | - | `?name=hero` |
| `anim` | 재생할 애니메이션 이름 | 첫 번째 | `&anim=idle` |
| `skin` | 적용할 스킨 | default | `&skin=red` |
| `loop` | 반복 재생 | true | `&loop=false` |
| `bg` | 배경색 (hex, # 제외) | 투명 | `&bg=1a1a2e` |
| `controls` | 컨트롤 표시 | false | `&controls=true` |

**조합 예시:**
```
player.html?name=hero&anim=run&skin=warrior&bg=1a1a2e
player.html?name=boss&anim=attack&loop=false&bg=000000
```

---

## Spine 버전 변경

`player.html` 상단의 `SPINE_VERSION` 값을 본인의 Spine 버전에 맞게 수정하세요:

```javascript
const SPINE_VERSION = "4.2";  // ← 여기를 변경
```

지원 버전: `"3.8"`, `"4.0"`, `"4.1"`, `"4.2"`

---

## 파일명이 폴더명과 다른 경우

기본적으로 `animations/hero/hero.json` 형태를 기대합니다.
만약 파일명이 다르다면 (예: `skeleton.json`), 
`player.html`의 `initPlayer()` 함수에서 경로를 수정하세요:

```javascript
// 변경 전
jsonUrl: `animations/${config.name}/${config.name}.json`,
atlasUrl: `animations/${config.name}/${config.name}.atlas`,

// 변경 후 (파일명이 모두 skeleton인 경우)
jsonUrl: `animations/${config.name}/skeleton.json`,
atlasUrl: `animations/${config.name}/skeleton.atlas`,
```

---

## 문제 해결

- **애니메이션이 안 보여요**: 브라우저 개발자 도구(F12)에서 Console 탭을 확인하세요. 파일 경로 오류가 대부분입니다.
- **CORS 에러**: GitHub Pages에서 호스팅하면 발생하지 않습니다. 로컬에서 테스트할 때는 Live Server 등을 사용하세요.
- **Spine 버전 불일치**: export한 Spine 버전과 `SPINE_VERSION` 값이 일치하는지 확인하세요.
