# aws-web-infra

리눅스 기초부터 AWS 웹 인프라 구성, 코드화, 배포 자동화까지 단계별로 직접 만든 실습 기록이다.

## 목표

- AWS 콘솔에서 웹 인프라를 직접 구성하고 설명할 수 있다.
- 같은 구성을 Terraform 코드로 재현한다.
- 배포를 CI/CD 파이프라인으로 자동화한다.

## 전체 구성도

메인 단계를 마친 뒤 추가한다.

## 진행 흐름

| 단계 | 한 일 | 상태 | 결과물 |
|---|---|---|---|
| [00-basics](00-basics/README.md) | VM에서 리눅스 기본과 웹 서버 실행 | 예정 | - |
| [01-aws-manual](01-aws-manual/README.md) | AWS 콘솔로 웹 인프라 구성 | 예정 | - |
| [02-terraform](02-terraform/README.md) | 메인 구성을 코드로 재현 | 예정 | - |
| [03-cicd](03-cicd/README.md) | 배포 파이프라인 자동화 | 예정 | - |

## 결과 산출물

단계를 마칠 때마다 갱신한다.

## 문서 링크

| 문서 | 내용 |
|---|---|
| [decisions.md](docs/decisions.md) | 승인된 결정과 예외 |
| [rules.md](docs/rules.md) | 반복해서 지킬 규칙 |
| [cost.md](docs/cost.md) | 크레딧 사용 내역과 리소스 기록 |
| [account.md](docs/account.md) | 계정 종류, 리전, 권한, 제약 |
