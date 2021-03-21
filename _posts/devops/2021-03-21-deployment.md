---
title: "Deployment"
excerpt: "Deployment(배포)에 대한 설명과 Strategy(전략) 소개"
last_modified_at: 2021-03-21T12:40:00
header:
  image: /assets/images/devops/deployment/deployment.png
categories:
  - Devops
tags:
  - Programming
  - Devops
  - Deployment

toc: true
toc_ads: true
toc_sticky: true
---
# Deployment
- 제품 팀은 릴리스를 더 자주 프로덕션에 배포하며, 순수한 소프트웨어 제품을 구축하는 경우에는 수 개월 또는 수 년에 걸친 릴리스 주기가 드물어지고 있다.
- 배포 빈도가 높을수록 배포 된 코드가 사이트 안정성이나 고객 경험에 부정적인 영향을 미칠 수 있으므로, 제품과 고객에 대한 위험을 최소화하는 코드 배포 전략을 개발하는 것이 중요하다.
- 배포 직후 발생하는 문제를 모니터링하는 것은 완벽한 배포를 계획하고 실행하는 것 만큼 중요하다.

# Strategy
## Rolling Deployment
![RollingDeployment](../../assets/images/devops/deployment/rolling.png)
- 서버를 한 대씩 구버전에서 새 버전으로 교체해가는 전략이다.
- 서버의 수에 제약이 있을 경우 유용하다.
- 배포 중 인스턴스 수가 감소하므로, 서버 처리 용량을 미리 고려해야 한다.

## Blue-Green Deployment
![Blue-GreenDeployment-After](../../assets/images/devops/deployment/bluegreen-after.png)
![Blue-GreenDeployment-Before](../../assets/images/devops/deployment/bluegreen-before.png)
- 구버전에서 새 버전으로 일제히 전환하는 전략이다.
- 하나의 버전만 프로덕션 되므로 버전 관리 문제를 방지 할 수 있다.
- 빠른 롤백이 가능하다.
- 운영 환경에 영향을 주지 않고 실제 서비스 환경에서 새 버전 테스트가 가능하다.
- 시스템 자원이 두 배로 필요하고, 전체 플랫폼에 대한 테스트가 진행되어야 한다.

## Canary Deployment
![CanaryDeployment](../../assets/images/devops/deployment/canary.png)
- 카나리아 새처럼 위험을 빠르게 감지할 수 있는 배포 기법이다.
- 구 버전의 서버와 새 버전의 서버를 구성하고 일부 트래픽을 새 버전으로 분산하여 오류 여부를 판단한다.
- A/B 테스트도 가능하며, 오류율 및 성능 모니터링에 유용하다.
  * A/B Testing : 카나리 배포와 유사하지만, A/B Testing은 신규 애플리케이션 기능에 관한 사용자 반응을 측정하는 데 초점을 맞춘다.
- 트래픽을 분산시킬 때는 라우팅을 랜덤하게 할 수 있고, 사용자로 분류할 수도 있다.