# Now-WayPoint

## 개요

Now-WayPoint(나와)의 프로젝트 개요를 설명합니다.

## 프로젝트 구조

벡엔드 프로젝트 하위는 각 API서버 프로젝트(컨테이너 기반으로 구성됨)로 나눠져있습니다.
API서버는 아래 아키텍처 구조을 따르고 있으며 각 프로젝트는 다음과 같습니다.

![스크린샷 2024-07-09 오전 10 34 49](https://github.com/Isn-t-this-E-not-I/Now-WayPoint-BE/assets/62759873/2214efb2-a816-4980-9cd3-98372096256b)

- now-waypoint-core : 인증, 사용자 관리, 게시글관리, 채팅, 좋아요 관리, 해시태그 관리 등 핵심 기능을 제공하는 코어 서버
- now-waypoint-mysql : MySQL 데이터베이스 서버

## 주요 기능
- 회원가입 및 로그인
- 게시글 등록 및 조회
- 실시간 데이터 처리(알림, 채팅, 지도 연동)

## 배포 환경
- AWS EC2, S3, RDS, Redis

## 🚀 주요 기술 스택
### 백엔드
	•Java 11
	•Spring Boot
	•Spring Security + JWT
	•Redis
	•MySQL
	•AWS S3
	•STOMP (WebSocket)
### 인프라 및 배포
	•AWS EC2 (개발 서버 & 프로덕션 서버)
	•AWS RDS (MySQL)
	•AWS S3 (파일 저장)
	•Redis (휘발성 데이터 저장)
	•GitHub Actions (CI/CD)
	•Docker, Docker Hub

## 🔥 아키텍처 설계
### 배포 환경 및 서버 구성
	### 개발 서버와 프로덕션 서버 분리
	•개발 서버에서 발생할 수 있는 이슈를 사전에 발견하고 해결
	•프로덕션 서버에서는 안정적으로 서비스 운영
	•비용 절감을 위해 개발 서버는 AWS 프리 티어 활용 및 데이터 초기화 방식 적용
 
	### CI/CD 자동화
	•GitHub Actions, Docker, Docker Hub를 활용하여 자동 배포 파이프라인 구축
	•develop 브랜치: Docker 이미지 생성 후 Docker Hub에 등록
	•main 브랜치: 개발 서버(EC2) 자동 배포
	•prod 브랜치: 프로덕션 서버(EC2) 자동 배포

 ## 📌 기능별 구현 방식
 1️⃣ 회원가입 및 로그인
	### 앱 내 회원가입 & 소셜 로그인(OAuth2)
	•이메일 인증(SMTP) 방식 도입 → 보안 강화
	•소셜 로그인(Kakao, Naver, Google) → OAuth2 인증 후 DB 저장
 
	### JWT 기반 로그인 및 토큰 관리
	•accessToken + refreshToken 발급
	•Redis TTL 기능 활용하여 토큰 만료 시간 관리
	•refreshToken을 이용한 자동 로그인 유지 및 토큰 갱신
 2️⃣ 실시간 데이터 처리 (STOMP)
	•실시간 알림, 지도 내 게시글 업데이트, 채팅 기능 구현
	•Spring STOMP 사용하여 실시간 데이터 송수신
	•유저가 로그인하면 알림, 게시글, 메시지 등의 구독 채널에 자동 등록
 3️⃣ 데이터 저장 및 관리

✔ 휘발성 데이터 처리 (Redis)
	•TTL 기능을 활용하여 실시간 데이터를 효율적으로 관리
	•일정 시간이 지난 데이터는 자동 삭제 → DB 부하 감소
	•API 호출 없이도 필요한 데이터 관리 가능

✔ 업로드 파일 관리 (AWS S3)
	•이미지, mp3, mp4 파일 저장을 위해 AWS S3 버킷 활용
	•확장성 & 복구 기능 제공
	•업로드된 파일에 대해 URL을 제공하여 관리 용이

 ## 🤝 협업 방식
 	### Git Flow 전략 도입
	•feature 브랜치 → develop 브랜치 → main/prod 브랜치로 배포
 
	### GitHub Actions을 활용한 코드 리뷰 프로세스
	•Pull Request 시 팀원 자동 assign → 코드 리뷰 진행
	•코드 스타일 및 성능 최적화 논의
 
	### Notion을 활용한 문서 및 일정 관리
	•API 명세서, 요구사항 정의, 회의록 정리
 
	### 디스코드(Discord) 회의 진행
	•매일 1시간 개발 진행 상황 공유 및 문제 해결 논의

## 💡 프로젝트에서 배운 점
	•OAuth2 기반 로그인 및 인증 처리 방식에 대한 이해
	•Redis TTL을 활용한 실시간 데이터 관리 및 DB 부하 감소 기법
	•STOMP 프로토콜을 사용한 실시간 알림, 채팅 기능 구현 경험
	•GitHub Actions + Docker + EC2 기반 CI/CD 자동 배포 경험
	•AWS 인프라 환경 구축 및 비용 최적화 방법 학습
