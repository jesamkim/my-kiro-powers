<div align="center">
  <h1>🔌 my-kiro-powers</h1>
  <p><strong>Kiro CLI용 커스텀 Power 컬렉션 — SA 업무 자동화 도구 모음</strong></p>
  <p>
    <img src="https://img.shields.io/badge/platform-Kiro_CLI-232F3E?style=flat-square&logo=amazon-aws" alt="Kiro CLI"/>
    <img src="https://img.shields.io/badge/powers-5-F66C02?style=flat-square" alt="5 Powers"/>
    <img src="https://img.shields.io/badge/license-MIT-blue?style=flat-square" alt="MIT License"/>
  </p>
</div>

---

Claude Code Custom Skill을 Kiro CLI Power로 마이그레이션한 컬렉션입니다.
프레젠테이션 생성, 아키텍처 다이어그램, YouTube 자막 추출 등 SA 업무에 필요한 도구를 Kiro CLI에서 바로 사용할 수 있습니다.

## 📦 Powers

| Power | 설명 | 트리거 |
|-------|------|--------|
| [**myslide**](myslide/) | AWS reInvent 테마 프레젠테이션 (PptxGenJS, 20가지 레이아웃) | `myslide`, `슬라이드 만들어` |
| [**aws-diagram**](aws-diagram/) | AWS 아키텍처 다이어그램 (SVG/PPTX, 직교 화살표, 260개 아이콘) | `AWS 구성도`, `아키텍처 다이어그램` |
| [**svg-diagram**](svg-diagram/) | 범용 SVG 다이어그램/배너 (순수 마크업, 외부 도구 불필요) | `SVG 다이어그램`, `배너 만들어` |
| [**youtube-script**](youtube-script/) | YouTube 자막/스크립트 추출 (다국어, 타임스탬프) | `유튜브 스크립트`, `자막 추출` |
| [**readme**](readme/) | 프로젝트 README.md 전문 생성기 (8단계 워크플로우) | `readme`, `README 만들어` |

## ⚡ Quick Start

### 1. 사전 설치

<details>
<summary><strong>Homebrew (시스템 도구)</strong></summary>

```bash
brew install node           # Node.js 18+ (myslide)
brew install python@3.11    # Python 3.9+
brew install librsvg        # SVG→PNG 변환 (myslide, aws-diagram)
brew install poppler        # PDF→이미지 변환 (myslide QA)
brew install --cask libreoffice  # PPTX→PDF 변환 (myslide QA)
```
</details>

<details>
<summary><strong>npm (전역 패키지)</strong></summary>

```bash
npm install -g pptxgenjs    # PPTX 생성 (myslide)
npm install -g sharp        # 이미지 변환 (myslide)
```
</details>

<details>
<summary><strong>pip (Python 패키지)</strong></summary>

```bash
pip install Pillow                  # 배경 이미지 생성 (myslide)
pip install cairosvg                # SVG→PNG 변환 (선택)
pip install youtube-transcript-api  # YouTube 자막 추출 (youtube-script)
```
</details>

### 2. 심볼릭 링크 생성

```bash
POWERS_DIR="/path/to/my-kiro-powers"  # 이 디렉토리의 절대 경로

ln -sf "$POWERS_DIR/aws-diagram"    ~/.kiro/skills/aws-diagram
ln -sf "$POWERS_DIR/svg-diagram"    ~/.kiro/skills/svg-diagram
ln -sf "$POWERS_DIR/myslide"        ~/.kiro/skills/myslide
ln -sf "$POWERS_DIR/youtube-script" ~/.kiro/skills/youtube-script
ln -sf "$POWERS_DIR/readme"         ~/.kiro/skills/readme
```

### 3. Agent에 등록

`~/.kiro/agents/<agent-name>.json`의 `resources` 배열에 추가:

```json
{
  "resources": [
    "skill:///<POWERS_DIR>/myslide/SKILL.md",
    "skill:///<POWERS_DIR>/aws-diagram/SKILL.md",
    "skill:///<POWERS_DIR>/svg-diagram/SKILL.md",
    "skill:///<POWERS_DIR>/youtube-script/SKILL.md",
    "skill:///<POWERS_DIR>/readme/SKILL.md"
  ]
}
```

## 🗂 프로젝트 구조

```
my-kiro-powers/
├── myslide/              # AWS 프레젠테이션 생성기
│   ├── SKILL.md
│   ├── icons/            # AWS 서비스 아이콘 248개
│   ├── scripts/          # 배경, 다이어그램, QA, 애니메이션
│   └── references/       # 테마, 레이아웃, 편집 가이드
├── aws-diagram/          # AWS 아키텍처 다이어그램
│   ├── SKILL.md
│   ├── icons/            # AWS 서비스 아이콘 260개
│   └── scripts/          # 다이어그램 생성 엔진
├── svg-diagram/          # 범용 SVG 다이어그램
│   └── SKILL.md
├── youtube-script/       # YouTube 자막 추출
│   ├── SKILL.md
│   └── scripts/          # 추출 스크립트
├── readme/               # README 생성기
│   ├── SKILL.md
│   └── references/       # 구조, 배지, 비주얼 가이드
├── LICENSE               # MIT License
└── README.md
```

## 📝 License

MIT License — [LICENSE](LICENSE) 참고

---

<div align="center">
  <sub>Built by <a href="https://github.com/jesamkim">Jesam Kim</a> — Solutions Architect @ AWS</sub>
</div>
