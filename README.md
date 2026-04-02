# Kiro CLI Powers

Claude Code Custom Skill을 Kiro CLI Power로 마이그레이션한 컬렉션입니다.

## Powers 목록

| Power | 용도 | 의존성 |
|-------|------|--------|
| **myslide** | AWS reInvent 테마 프레젠테이션 생성 (PptxGenJS) | aws-diagram, sd35l |
| **aws-diagram** | AWS 아키텍처 다이어그램 (SVG/PPTX, 직교 화살표) | 없음 |
| **sd35l** | Stable Diffusion 3.5 Large 이미지 생성 (Bedrock) | 없음 |
| **svg-diagram** | 범용 SVG 다이어그램/배너 (순수 마크업) | 없음 |

## 설정 방법

### 1. agent에 등록

`~/.kiro/agents/<agent-name>.json`의 `resources` 배열에 추가합니다.
`<POWERS_DIR>`을 이 디렉토리의 절대 경로로 바꿔주세요.

```json
{
  "resources": [
    "skill:///<POWERS_DIR>/myslide/SKILL.md",
    "skill:///<POWERS_DIR>/aws-diagram/SKILL.md",
    "skill:///<POWERS_DIR>/sd35l/SKILL.md",
    "skill:///<POWERS_DIR>/svg-diagram/SKILL.md"
  ]
}
```

### 2. ~/.kiro/skills/ 에 심볼릭 링크

myslide가 `~/.kiro/skills/sd35l/`, `~/.kiro/skills/aws-diagram/` 등을 참조하므로 심볼릭 링크가 필요합니다.

```bash
POWERS_DIR="$(cd "$(dirname "$0")" && pwd)"  # 이 디렉토리의 절대 경로

ln -sf "$POWERS_DIR/aws-diagram" ~/.kiro/skills/aws-diagram
ln -sf "$POWERS_DIR/sd35l" ~/.kiro/skills/sd35l
ln -sf "$POWERS_DIR/svg-diagram" ~/.kiro/skills/svg-diagram
ln -sf "$POWERS_DIR/myslide" ~/.kiro/skills/myslide
```

## 각 Power 소개

### myslide
AWS reInvent 2023 디자인 시스템 기반 프레젠테이션 생성기. PptxGenJS(Node.js)로 슬라이드를 생성하고, Python 스크립트로 그라디언트 배경/SVG 다이어그램을 만듭니다. 20가지 슬라이드 레이아웃, 248개 AWS 서비스 아이콘 내장.

트리거: `myslide`, `AWS 프레젠테이션`, `슬라이드 만들어`, `발표자료`

### aws-diagram
JSON 정의 → SVG/PPTX 아키텍처 다이어그램 자동 생성. 직교(right-angle) 화살표 라우팅, VPC/AZ/Subnet 컨테이너 중첩, 260개 공식 AWS 아이콘 내장.

트리거: `AWS 구성도`, `아키텍처 다이어그램`, `인프라 그림`

### sd35l
Amazon Bedrock의 Stability AI SD3.5 Large 모델로 이미지 생성. text-to-image, image-to-image 지원. 9가지 종횡비, seed 기반 재현성.

트리거: `이미지 생성`, `그림 그려`, `SD 이미지`

### svg-diagram
순수 SVG 마크업으로 다이어그램, 배너, 플로우차트 생성. 외부 도구 불필요. Anti-overlap 규칙과 다크모드 호환 팔레트 내장.

트리거: `SVG 다이어그램`, `배너 만들어`, `파이프라인 시각화`

## 의존성

- Python 3.9+, `Pillow`, `boto3` (이미지 생성 스크립트)
- Node.js 18+, `pptxgenjs`, `sharp` (프레젠테이션 생성)
- LibreOffice (PPTX→PDF 변환, QA용)
- `librsvg` (SVG→PNG 변환)
- AWS credentials (Bedrock 모델 접근, sd35l)

각 Power의 상세 설치 가이드는 해당 디렉토리의 README.md를 참고하세요.
