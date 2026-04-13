# Kiro CLI Powers

Claude Code Custom Skill을 Kiro CLI Power로 마이그레이션한 컬렉션입니다.

## Powers 목록

| Power | 용도 | 의존성 |
|-------|------|--------|
| **myslide** | AWS reInvent 테마 프레젠테이션 생성 (PptxGenJS) | aws-diagram |
| **aws-diagram** | AWS 아키텍처 다이어그램 (SVG/PPTX, 직교 화살표) | 없음 |
| **svg-diagram** | 범용 SVG 다이어그램/배너 (순수 마크업) | 없음 |
| **youtube-script** | YouTube 영상 자막/스크립트 추출 | youtube-transcript-api |
| **readme** | 프로젝트 README.md 전문 생성기 | 없음 |

## 사전 설치 (Prerequisites)

### 시스템 도구 (Homebrew)

```bash
brew install node           # Node.js 18+ (myslide)
brew install python@3.11    # Python 3.9+ (대부분의 Power)
brew install librsvg        # rsvg-convert — SVG→PNG 변환 (myslide, aws-diagram)
brew install poppler        # pdftoppm — PDF→이미지 변환 (myslide QA)
brew install --cask libreoffice  # PPTX→PDF 변환 (myslide QA)
```

### Node.js 패키지 (전역)

```bash
npm install -g pptxgenjs    # PPTX 생성 (myslide)
npm install -g sharp        # 이미지 변환 (myslide SVG→PNG)
```

### Python 패키지

```bash
pip install Pillow                  # 배경 이미지 생성 (myslide)
pip install cairosvg                # SVG→PNG 변환 (myslide, 선택)
pip install youtube-transcript-api  # YouTube 자막 추출 (youtube-script)
```

## 설정 방법

### 1. agent에 등록

`~/.kiro/agents/<agent-name>.json`의 `resources` 배열에 추가합니다.
`<POWERS_DIR>`을 이 디렉토리의 절대 경로로 바꿔주세요.

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

### 2. ~/.kiro/skills/ 에 심볼릭 링크

myslide가 `~/.kiro/skills/aws-diagram/` 등을 참조하므로 심볼릭 링크가 필요합니다.

```bash
POWERS_DIR="$(cd "$(dirname "$0")" && pwd)"  # 이 디렉토리의 절대 경로

ln -sf "$POWERS_DIR/aws-diagram" ~/.kiro/skills/aws-diagram
ln -sf "$POWERS_DIR/svg-diagram" ~/.kiro/skills/svg-diagram
ln -sf "$POWERS_DIR/myslide" ~/.kiro/skills/myslide
ln -sf "$POWERS_DIR/youtube-script" ~/.kiro/skills/youtube-script
ln -sf "$POWERS_DIR/readme" ~/.kiro/skills/readme
```

## 각 Power 소개

### myslide
AWS reInvent 2023 디자인 시스템 기반 프레젠테이션 생성기. PptxGenJS(Node.js)로 슬라이드를 생성하고, Python 스크립트로 그라디언트 배경/SVG 다이어그램을 만듭니다. 20가지 슬라이드 레이아웃, 248개 AWS 서비스 아이콘 내장.

트리거: `myslide`, `AWS 프레젠테이션`, `슬라이드 만들어`, `발표자료`

### aws-diagram
JSON 정의 → SVG/PPTX 아키텍처 다이어그램 자동 생성. 직교(right-angle) 화살표 라우팅, VPC/AZ/Subnet 컨테이너 중첩, 260개 공식 AWS 아이콘 내장.

트리거: `AWS 구성도`, `아키텍처 다이어그램`, `인프라 그림`

### svg-diagram
순수 SVG 마크업으로 다이어그램, 배너, 플로우차트 생성. 외부 도구 불필요. Anti-overlap 규칙과 다크모드 호환 팔레트 내장.

트리거: `SVG 다이어그램`, `배너 만들어`, `파이프라인 시각화`

### youtube-script
YouTube 영상에서 자막/캡션을 추출하여 텍스트 파일로 저장. 자동 생성 자막과 수동 자막 모두 지원하며, 한국어/영어/일본어 등 다국어 대응. 타임스탬프 포함 및 JSON 출력 옵션.

트리거: `유튜브 스크립트`, `자막 추출`, `youtube transcript`, `유튜브 자막`

### readme
프로젝트 README.md 전문 생성기. 8단계 워크플로우, 7가지 프로젝트 타입별 템플릿, Shields.io 배지, Mermaid 다이어그램, GIF 데모 가이드 포함. awesome-readme 커뮤니티 100+ 베스트 프랙티스 기반.

트리거: `readme`, `README 만들어`, `리드미`, `프로젝트 문서화`

## 라이선스

MIT License — [LICENSE](LICENSE) 참고
