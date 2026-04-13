# myslide

AWS reInvent 2023 디자인 시스템 기반 프레젠테이션 생성기.

PptxGenJS(Node.js)로 슬라이드를 생성하고, Python 스크립트로 그라디언트 배경과 SVG 아키텍처 다이어그램을 만듭니다. 20가지 슬라이드 레이아웃, 248개 AWS 서비스 아이콘 내장.

## 트리거

`myslide`, `AWS 프레젠테이션`, `슬라이드 만들어`, `발표자료`, `make slides`, `AWS slides`

## 사전 설치 (필수)

### Node.js 패키지

```bash
npm install -g pptxgenjs
npm install -g sharp
```

### Python 패키지

```bash
pip install Pillow
pip install cairosvg   # SVG→PNG 변환 (선택, 없으면 rsvg-convert 사용)
```

### 시스템 도구

```bash
# macOS
brew install librsvg    # rsvg-convert (SVG→PNG 변환)
brew install poppler    # pdftoppm (PPTX→이미지 변환, QA용)
brew install --cask libreoffice  # PPTX→PDF 변환 (QA용)
```

### 연관 Power (필수)

myslide는 다음 Power를 참조합니다. `~/.kiro/skills/`에 심볼릭 링크가 필요합니다:

- `aws-diagram` — 복잡한 AWS 아키텍처 다이어그램

## 구성

```
myslide/
├── SKILL.md                    # Power 정의 (디자인 시스템, 워크플로우, QA 체크리스트)
├── LICENSE.txt
├── icons/                      # AWS 서비스 아이콘 248개 (SVG)
├── scripts/
│   ├── create_aws_slide.py     # 배경 이미지, SVG 다이어그램, AWS 로고 생성
│   ├── add_slide.py            # 기존 PPTX에 슬라이드 추가
│   ├── thumbnail.py            # 슬라이드 썸네일 그리드 생성
│   ├── clean.py                # PPTX XML 정리
│   └── office/                 # LibreOffice 연동 (PDF 변환, unpack/pack)
└── references/
    ├── aws-theme.md            # 색상, 폰트, 간격 규칙
    ├── slide-patterns.md       # 20가지 레이아웃 템플릿
    ├── pptxgenjs.md            # PptxGenJS 사용 가이드
    ├── editing.md              # 기존 PPTX 편집 가이드
    └── animations.md           # 애니메이션 프리미티브 레퍼런스
```
