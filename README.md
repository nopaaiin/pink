# 말 (馬 / 言)

> 인터랙티브 웹, 2026  
> **nopaaiin.github.io/pink**

---

## 작품 설명

붉은 말의 해에, 나는 말을 잡으려 했다.

손을 뻗으면 흩어지고, 쥐려 하면 사라진다.  
말(馬)은 말(言)처럼 — 한번 달리기 시작하면 내 손을 벗어난다.  
잡으려는 순간 멀어지고, 손을 내리면 다가온다.

**기뻐하지도 슬퍼하지도 말 것. 원래 잡히지 않는 것들이 있다.**


---

## 프로젝트 구조

```
pink/
│
├── index.html      # 메인 페이지 구조
├── style.css       # 스타일 (배경, 커서, UI)
├── horse.js        # 말 인터랙션 로직 전체
│
├── horse.gif       # 말 애니메이션 GIF
│
└── README.md       # 이 파일
```

---

## 사용 기술

| 분류 | 기술 | 용도 |
|------|------|------|
| HTML | HTML5 | 페이지 구조, 캔버스 |
| CSS | CSS3 | 스타일, 팝업 애니메이션 |
| JavaScript | Vanilla JS | 말 클래스, 렌더 루프, 충돌 처리 |
| JavaScript | Canvas API | 말 드로잉 (GIF / 아스키 / 도트) |
| JavaScript | MediaPipe Hands | 웹캠 손 인식 |
| Python | — | 사용 안 함 |

> **외부 라이브러리**
> - [MediaPipe Hands](https://cdn.jsdelivr.net/npm/@mediapipe/hands/) — 손 랜드마크 인식
> - [MediaPipe Camera Utils](https://cdn.jsdelivr.net/npm/@mediapipe/camera_utils/) — 웹캠 연결

---

## 인터랙션 설명

| 손 동작 | 말 반응 |
|---------|---------|
| ✋ 손 펼치기 | 말들이 손 쪽으로 다가옴 |
| ✊ 손 천천히 쥐기 | 말들이 천천히 걸어서 도망 |
| ✊ 손 빠르게 쥐기 | 말들이 호다닥 도주 |
| 손 없음 | 말들이 자유롭게 배회 |
| 랜덤 (1/20 확률) | 말 한 마리 넘어짐 + "이히힝~" |

---

## 말 종류

```
GIF 말    — horse.gif를 CSS filter로 붉은 톤 처리, 2마리
아스키 말  — 텍스트 문자로 그린 말 측면, 3마리
도트 말   — 픽셀 아트 16x10 그리드, 4마리
```

---

## Web Pipeline (배포 흐름)

```
로컬 편집 (VSCode)
       │
       ▼
git add .
git commit -m "변경 내용"
git push origin main
       │
       ▼
GitHub Repository (main 브랜치)
       │
       ▼
GitHub Pages 자동 배포 (1~3분 소요)
       │
       ▼
nopaaiin.github.io/pink
```

---

## 로컬에서 실행하는 법

```bash
# 1. 레포 클론
git clone https://github.com/nopaaiin/pink.git

# 2. 폴더 이동
cd pink

# 3. 브라우저에서 열기 (반드시 로컬 서버로 실행해야 카메라 작동)
# VSCode Live Server 확장 설치 후 index.html 우클릭 → Open with Live Server
```

> **주의**: 카메라(MediaPipe)는 `http://localhost` 또는 `https://` 환경에서만 작동  
> 파일을 그냥 더블클릭하면 (`file://`) 카메라 권한이 거부될 수 있음

---

## 파일 수정 후 배포하기

```bash
# 변경된 파일 스테이징
git add index.html style.css horse.js

# 커밋
git commit -m "fix: 말 속도 조정"

# 푸시
git push
```

---

## 언어별 역할 요약

**HTML** — 뼈대
- 캔버스, 웹캠 영역, UI 텍스트 배치

**CSS** — 외형
- 흰 배경, 커서 스타일, "이히힝~" 팝업 애니메이션

**JavaScript** — 동작
- `Horse` 클래스: 말 종류별 드로잉, 이동, 충돌 처리
- MediaPipe 손 인식: 손가락 굽힘 각도로 열림/닫힘 판별
- Canvas 렌더 루프: 60fps로 말 위치 업데이트 및 그리기

**Python** — 미사용
- 이 프로젝트는 순수 프론트엔드로 Python을 사용하지 않음
