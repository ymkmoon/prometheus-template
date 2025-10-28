# prometheus-template
프로메테우스, 그라파타 템플릿 프로젝트


## 빌드

### 1. EMQX 이미지 빌드 및 컨테이너 실행 

```bash
# 로컬 환경
docker compose -p prometheus-template up -d
docker compose -p prometheus-template --env-file env.local up -d

# 개발 환경
docker compose -p prometheus-template --env-file env.dev down
docker compose -p prometheus-template --env-file env.dev up -d
```