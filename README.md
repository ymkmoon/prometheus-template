# prometheus-template
프로메테우스, 그라파타 템플릿 프로젝트


## 빌드

### 1. 구조

```
prometheus-template/
├── docker-compose.yml      # 메인 Docker Compose 파일
├── prometheus/             # Prometheus 설정 디렉토리
│   └── prometheus.yml      # Prometheus 구성 파일 (Blackbox 타겟 포함)
├── blackbox/               # Blackbox Exporter 설정 디렉토리
│   └── blackbox.yml        # Blackbox 구성 파일
├── grafana/                # Grafana 설정 디렉토리 (프로비저닝용)
│   ├── provisioning/       # Grafana 프로비저닝 디렉토리
│   │   ├── dashboards/     # 대시보드 YAML 파일 (빈 폴더로 시작, 필요시 추가)
│   │   │   └── dashboard.yml  # 기본 대시보드 프로비저닝 (예시)
│   │   └── datasources/    # 데이터소스 YAML 파일
│   │       └── datasource.yml  # Prometheus 데이터소스 설정
│   └── grafana.ini         # Grafana 기본 설정 (옵션)
├── .env.local              # 로컬 환경 변수 파일 (예시)
└── README.md               # 사용 가이드 
```

### 2. 이미지 빌드 및 컨테이너 실행 

```bash
# 개발 환경
docker compose -p prometheus-template --env-file .env.dev down
docker compose -p prometheus-template --env-file .env.dev up -d

# 검수 환경
docker compose -p prometheus-template --env-file .env.stg down
docker compose -p prometheus-template --env-file .env.stg up -d

# 서비스 환경
docker compose -p prometheus-template --env-file .env.prd down
docker compose -p prometheus-template --env-file .env.prd up -d
```

### 3. 모니터링

- Prometheus: http://localhost:9090 (타겟 확인: /targets)
- Grafana: http://localhost:3000 (로그인: admin / $GF_SECURITY_ADMIN_PASSWORD)
- Blackbox: http://localhost:9115 (직접 접근 필요 없음)


> Prometheus에서 'blackbox' job을 확인하세요. API 서버가 업이면 up{instance="http://$API_HOST:$API_PORT/$CONTEXT_PATH"} = 1.


> Grafana에서 새 대시보드를 만들어 Blackbox 메트릭스(probe_success, probe_duration_seconds 등)를 시각화하세요. <br/>
(예: Prometheus Blackbox Exporter 대시보드 ID: 7587 import)