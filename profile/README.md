<div align="center">

<a href="https://gakdo.site">
  <img src="https://raw.githubusercontent.com/GAKDO/.github/main/profile/assets/banner.svg" width="100%" alt="TRACE — 빌린 노트북 상태, 사진으로 남겨 드려요" />
</a>

<br/>

<a href="https://gakdo.site"><img src="https://img.shields.io/badge/서비스-gakdo.site-c8161d?style=for-the-badge&labelColor=0b0b0f" alt="gakdo.site"/></a>
<a href="https://gakdo.github.io/docs/guide/"><img src="https://img.shields.io/badge/안내서-MVP_Guide-ffffff?style=for-the-badge&labelColor=0b0b0f" alt="MVP 안내서"/></a>
<a href="https://github.com/GAKDO/contracts"><img src="https://img.shields.io/badge/계약-OpenAPI_·_JSON_Schema-ffffff?style=for-the-badge&labelColor=0b0b0f" alt="contracts"/></a>

<br/><br/>

**TRACE: AI 비전과 해시 체인으로 증명하는 렌탈 노트북 상태 기록 서비스**<br/>
<sub>2026 조선대학교 IT Festival 캡스톤 출품작 · 팀 GAKDO</sub>

</div>

<br/>

## ✦ 무엇을 해결하나요

노트북을 빌리고 돌려줄 때마다 "이 흠집, 원래 있던 거예요"라는 다툼이 생깁니다. TRACE는 **출고 · 수령 · 반납** 세 시점에 같은 방식으로 사진을 남기고, AI가 흠집 후보를 찾고, 사람이 확정한 기록만 **해시 체인으로 봉인**합니다. 봉인된 기록은 누구나 검증 페이지에서 고쳐지지 않았는지 확인할 수 있습니다.

<table>
  <tr>
    <td width="33%" valign="top">
      <h3>📸 같은 조건으로 찍기</h3>
      부스 Jetson이 카메라 2대 × 조명 3개로 윗면·아랫면을 찍습니다. 수령 때는 고객이 QR로 들어와 폰으로 찍습니다.
    </td>
    <td width="33%" valign="top">
      <h3>🔍 AI는 넓게, 사람은 확실하게</h3>
      YOLO11-seg가 흠집 후보를 폴리곤으로 넓게 잡고, 관리자가 후보마다 확정·기각합니다. 확정한 흠집만 등급 A~D에 들어갑니다.
    </td>
    <td width="33%" valign="top">
      <h3>🔗 고칠 수 없는 기록</h3>
      시점마다 이전 기록의 해시를 이어 붙이고 Ed25519로 서명합니다. 한 글자만 바뀌어도 검증에서 바로 드러납니다.
    </td>
  </tr>
</table>

<br/>

<p align="center">
  <img src="https://raw.githubusercontent.com/GAKDO/.github/main/profile/assets/flow.svg" width="100%" alt="출고·수령·반납 세 시점과 해시 체인 봉인"/>
</p>

## ✦ 구성

<p align="center">
  <img src="https://raw.githubusercontent.com/GAKDO/.github/main/profile/assets/architecture.svg" width="100%" alt="TRACE 서비스 구성도"/>
</p>

- 밖으로 열린 입구는 **gakdo.site(HTTPS 443) 하나**입니다. 화면·API·사진 업로드가 모두 이 길로 들어옵니다.
- 서버끼리는 서로 직접 부르지 않고 RabbitMQ `trace.events` 이벤트로만 주고받습니다.
- 사진은 서버를 거치지 않고 사전 서명 URL로 저장소에 바로 올라가며, 올린 뒤 SHA-256으로 확인합니다.
- 학교 서버의 사진 검사와 부스 Jetson은 **항상 같은 버전의 모델**을 씁니다.

## ✦ 레포지토리

| 레포 | 하는 일 | 기술 |
|---|---|---|
| [**web**](https://github.com/GAKDO/web) | 관리자 화면 · 폰 촬영 · 3D 리포트 · 검증 페이지 | React 18 · TypeScript · Vite · R3F |
| [**gateway**](https://github.com/GAKDO/gateway) | JWT 검증 · 라우팅 · 요청 제한 | Spring Cloud Gateway · Redis |
| [**auth_server**](https://github.com/GAKDO/auth_server) | 회원 · 로그인 · QR · 페어링 · JWKS · 봉인 영수증 메일 | Spring Boot 3.5 · Nimbus JOSE |
| [**rental_server**](https://github.com/GAKDO/rental_server) | 기종 · 기기 · 렌탈 · 시점 | Spring Boot 3.5 · JPA · Flyway |
| [**capture_server**](https://github.com/GAKDO/capture_server) | 촬영 세트 · 사전 서명 URL · 탐지 · 검수 · 등급 | Spring Boot 3.5 · AWS SDK v2 |
| [**diagnostics_server**](https://github.com/GAKDO/diagnostics_server) | 진단 검증 · 렌탈 전후 비교 · 점검 플래그 | Spring Boot 3.5 · JSON Schema |
| [**report_server**](https://github.com/GAKDO/report_server) | 타임라인 · 해시 체인 · 검증 · SSE | Spring Boot 3.5 · Ed25519 |
| [**booth**](https://github.com/GAKDO/booth) | 부스 Jetson 앱 · 학습 데이터 촬영 도구 | Python · OpenCV · TensorRT |
| [**agent**](https://github.com/GAKDO/agent) | 노트북 진단 에이전트 (macOS · Windows) | Python |
| [**ml**](https://github.com/GAKDO/ml) | 사진 검사 워커 · 데이터셋 빌더 · 학습 | PyTorch · YOLO11-seg · ONNX |
| [**contracts**](https://github.com/GAKDO/contracts) | OpenAPI · 진단 JSON Schema · 이벤트 스키마 · 코드 값 | OpenAPI 3.1 · JSON Schema |
| [**gitops**](https://github.com/GAKDO/gitops) | 배포 구성 | Docker Compose · Kustomize |
| [**docs**](https://github.com/GAKDO/docs) | 설계서 · 결정 기록 · 안내서 · 팀 운영 | Markdown · Spec Kit |

## ✦ 기술 스택

<p>
  <img src="https://img.shields.io/badge/Java_21-0b0b0f?style=flat-square&logo=openjdk&logoColor=white"/>
  <img src="https://img.shields.io/badge/Spring_Boot-0b0b0f?style=flat-square&logo=springboot&logoColor=6DB33F"/>
  <img src="https://img.shields.io/badge/PostgreSQL-0b0b0f?style=flat-square&logo=postgresql&logoColor=4169E1"/>
  <img src="https://img.shields.io/badge/RabbitMQ-0b0b0f?style=flat-square&logo=rabbitmq&logoColor=FF6600"/>
  <img src="https://img.shields.io/badge/Redis-0b0b0f?style=flat-square&logo=redis&logoColor=FF4438"/>
  <img src="https://img.shields.io/badge/MinIO-0b0b0f?style=flat-square&logo=minio&logoColor=C72E49"/>
  <img src="https://img.shields.io/badge/React-0b0b0f?style=flat-square&logo=react&logoColor=61DAFB"/>
  <img src="https://img.shields.io/badge/TypeScript-0b0b0f?style=flat-square&logo=typescript&logoColor=3178C6"/>
  <img src="https://img.shields.io/badge/Three.js-0b0b0f?style=flat-square&logo=threedotjs&logoColor=white"/>
  <img src="https://img.shields.io/badge/Python-0b0b0f?style=flat-square&logo=python&logoColor=3776AB"/>
  <img src="https://img.shields.io/badge/PyTorch-0b0b0f?style=flat-square&logo=pytorch&logoColor=EE4C2C"/>
  <img src="https://img.shields.io/badge/YOLO11--seg-0b0b0f?style=flat-square&logo=ultralytics&logoColor=white"/>
  <img src="https://img.shields.io/badge/NVIDIA_Jetson-0b0b0f?style=flat-square&logo=nvidia&logoColor=76B900"/>
  <img src="https://img.shields.io/badge/ONNX-0b0b0f?style=flat-square&logo=onnx&logoColor=white"/>
  <img src="https://img.shields.io/badge/Docker-0b0b0f?style=flat-square&logo=docker&logoColor=2496ED"/>
  <img src="https://img.shields.io/badge/GitHub_Actions-0b0b0f?style=flat-square&logo=githubactions&logoColor=2088FF"/>
</p>

## ✦ 팀 GAKDO

| 역할 | 맡은 일 |
|---|---|
| **A** | 서버 6개 · 인프라 · 계약 · 모델 학습 |
| **B** | 부스 Jetson 앱 · 진단 에이전트 · 학습 데이터 촬영 |
| **C** | 웹 화면 · 폰 촬영 · 3D 리포트 · 검증 페이지 |

<sub>Spec Kit으로 명세 → 계획 → 작업 → 구현 순서를 지키고, 계약(contracts)을 먼저 고정한 뒤 레포마다 따로 개발합니다.</sub>

<br/>

<div align="center">
  <a href="https://gakdo.site"><b>gakdo.site</b></a> · <a href="https://github.com/GAKDO/docs">docs</a> · <a href="https://github.com/GAKDO/contracts">contracts</a>
  <br/><br/>
  <img src="https://img.shields.io/badge/-%E2%9C%A6%20TRACE-c8161d?style=flat-square" alt="TRACE"/>
</div>
