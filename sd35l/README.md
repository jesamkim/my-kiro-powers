# sd35l

Amazon Bedrock의 Stability AI SD3.5 Large 모델로 이미지를 생성합니다.

text-to-image, image-to-image(스타일 변환) 지원. 9가지 종횡비, seed 기반 재현성.

## 트리거

`이미지 생성`, `그림 그려`, `SD 이미지`, `generate image`, `stable diffusion`

## 사전 설치 (필수)

### Python 패키지

```bash
pip install boto3
```

### AWS 설정

- AWS credentials 설정 필요 (`~/.aws/credentials` 또는 환경변수)
- Bedrock 콘솔에서 `Stable Diffusion 3.5 Large` 모델 접근 활성화 (리전: `us-west-2`)

## 사용 예시

```bash
python3 scripts/generate_image.py \
  --prompt "A futuristic city at sunset, cinematic lighting" \
  --aspect-ratio 16:9 \
  --seed 42 \
  --output-dir ./output
```

## 구성

```
sd35l/
├── SKILL.md                              # Power 정의 (워크플로우, 프롬프트 최적화)
├── LICENSE.txt
├── scripts/
│   └── generate_image.py                 # 이미지 생성 스크립트
└── references/
    ├── api_reference.md                  # SD3.5 Large API 파라미터
    └── prompt_best_practices.md          # 프롬프트 최적화 규칙
```
