<div align="center">

<a href="https://gakdo.site">
  <img src="https://raw.githubusercontent.com/GAKDO/.github/main/profile/assets/banner.svg" width="100%" alt="TRACE — 빌린 노트북 상태, 사진으로 남겨 드려요" />
</a>

<h1>TRACE</h1>
<p><strong>AI 비전과 해시 체인으로 증명하는 렌탈 노트북 상태 기록 서비스</strong></p>
<p>📅 <b>개발 기간</b> : 2026.10.30 ~ 2026.11.16 &nbsp;·&nbsp; 🏆 2026 조선대학교 IT Festival 캡스톤 &nbsp;·&nbsp; 👥 팀 GAKDO</p>

<a href="https://gakdo.site"><img src="https://img.shields.io/badge/서비스-gakdo.site-c8161d?style=for-the-badge&labelColor=0b0b0f" alt="gakdo.site"/></a>
<a href="https://gakdo.github.io/docs/api/mvp.html"><img src="https://img.shields.io/badge/API_명세서-Redoc-ffffff?style=for-the-badge&labelColor=0b0b0f" alt="API 명세서"/></a>
<a href="https://gakdo.github.io/docs/guide/"><img src="https://img.shields.io/badge/안내서-MVP_Guide-ffffff?style=for-the-badge&labelColor=0b0b0f" alt="MVP 안내서"/></a>

</div>

<br/>

| 📖 도메인 | 📋 API 명세서 | 🧭 처음 보는 분을 위한 안내서 |
|:---:|:---:|:---:|
| [gakdo.site](https://gakdo.site) | [gakdo.github.io/docs/api/mvp.html](https://gakdo.github.io/docs/api/mvp.html) | [gakdo.github.io/docs/guide](https://gakdo.github.io/docs/guide/) |

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

<p align="center">
  <img src="https://raw.githubusercontent.com/GAKDO/.github/main/profile/assets/flow.svg" width="100%" alt="출고·수령·반납 세 시점과 해시 체인 봉인"/>
</p>

## ✦ 주요 기능

<table>
  <tr>
    <td width="50%" valign="top">
      <img src="https://raw.githubusercontent.com/GAKDO/.github/main/profile/assets/screens/home.png" alt="첫 화면"/>
      <b>첫 화면 · 이용 안내</b><br/><sub>가입하면 마이페이지에서 내가 빌린 노트북의 사진과 흠집 기록을 바로 봅니다.</sub>
    </td>
    <td width="50%" valign="top">
      <img src="https://raw.githubusercontent.com/GAKDO/.github/main/profile/assets/screens/booth.png" alt="부스 화면"/>
      <b>부스 빠른 검사</b><br/><sub>Jetson이 12장을 찍고 TensorRT로 탐지해 1초 안팎으로 "문제 있음/없음"을 띄웁니다.</sub>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <img src="https://raw.githubusercontent.com/GAKDO/.github/main/profile/assets/screens/catalog-3d.png" alt="보유 노트북 3D"/>
      <b>보유 노트북 · 외관 3D</b><br/><sub>로그인 없이 기기를 비교하고, 3D 위의 점을 누르면 그 흠집이 찍힌 사진을 봅니다.</sub>
    </td>
    <td width="50%" valign="top">
      <img src="https://raw.githubusercontent.com/GAKDO/.github/main/profile/assets/screens/verify.png" alt="기록 검증"/>
      <b>기록 검증</b><br/><sub>봉인 영수증의 링크로 누구나 해시 체인과 서명을 다시 계산해 기록이 그대로인지 확인합니다.</sub>
    </td>
  </tr>
</table>

<details>
<summary><b>기능 전체 보기</b></summary>

| 누가 | 기능 |
|---|---|
| 관리자 | 기종·기기 등록(라벨 사진 글자 읽기), 렌탈 열기, 출고·반납 시점 시작, 흠집 후보 확정·기각, 검사 결과·등급 보기, 렌탈 전후 진단 비교 |
| 부스 | 기다리는 기기 고르기, 12장 촬영, Jetson 흠집 탐지, 사진 직접 업로드, 학습 데이터 촬영 |
| 고객 | 수령 QR 하나로 가입·로그인과 렌탈 연결, 폰으로 수령 촬영, 출고 사진과 나란히 비교, 3D 리포트, 봉인 영수증 메일 |
| 누구나 | 보유 노트북 목록·3D 흠집 위치, 기록 검증 페이지 |
| 진단 에이전트 | 페어링 코드로 연결, 배터리·SSD·부품·잠금 상태 수집, 진단 JSON 검증 후 동의하면 업로드 |

</details>

## ✦ 👥 팀원

<table align="center">
  <tbody>
    <tr>
      <td align="center" width="200">
        <a href="https://github.com/kim75503">
          <img src="https://github.com/kim75503.png" width="100" height="100" alt="kim75503"/>
          <br/><b>김민서</b>
        </a>
        <br/><sub><b>A · 서버 6개 · 인프라<br/>계약 · AI 학습</b></sub>
      </td>
      <td align="center" width="200">
        <a href="https://github.com/iamminseo">
          <img src="https://github.com/iamminseo.png" width="100" height="100" alt="iamminseo"/>
          <br/><b>iamminseo</b>
        </a>
        <br/><sub><b>B · 부스 Jetson 앱<br/>진단 에이전트 · 학습 촬영</b></sub>
      </td>
      <td align="center" width="200">
        <a href="https://github.com/practicech">
          <img src="https://github.com/practicech.png" width="100" height="100" alt="practicech"/>
          <br/><b>practicech</b>
        </a>
        <br/><sub><b>C · 웹 화면 · 폰 촬영<br/>3D 리포트 · 검증 페이지</b></sub>
      </td>
    </tr>
  </tbody>
</table>

<sub>Spec Kit으로 명세 → 계획 → 작업 → 구현 순서를 지키고, 계약(contracts)을 먼저 고정한 뒤 레포마다 따로 개발합니다.</sub>

## ✦ 💻 Tech Stacks

| 구분 | 기술 스택 |
| :--- | :--- |
| **Frontend** | ![React](https://img.shields.io/badge/React_18-0b0b0f?style=flat&logo=react&logoColor=61DAFB) ![TypeScript](https://img.shields.io/badge/TypeScript-0b0b0f?style=flat&logo=typescript&logoColor=3178C6) ![Vite](https://img.shields.io/badge/Vite-0b0b0f?style=flat&logo=vite&logoColor=646CFF) ![Three.js](https://img.shields.io/badge/React_Three_Fiber-0b0b0f?style=flat&logo=threedotjs&logoColor=white) ![TanStack Query](https://img.shields.io/badge/TanStack_Query-0b0b0f?style=flat&logo=reactquery&logoColor=FF4154) |
| **Backend** | ![Java](https://img.shields.io/badge/Java_21-0b0b0f?style=flat&logo=openjdk&logoColor=white) ![Spring Boot](https://img.shields.io/badge/Spring_Boot_3.5-0b0b0f?style=flat&logo=springboot&logoColor=6DB33F) ![Spring Security](https://img.shields.io/badge/Spring_Security-0b0b0f?style=flat&logo=springsecurity&logoColor=6DB33F) ![Spring Cloud Gateway](https://img.shields.io/badge/Spring_Cloud_Gateway-0b0b0f?style=flat&logo=spring&logoColor=6DB33F) ![JWT](https://img.shields.io/badge/JWT_RS256-0b0b0f?style=flat&logo=jsonwebtokens&logoColor=white) ![Flyway](https://img.shields.io/badge/Flyway-0b0b0f?style=flat&logo=flyway&logoColor=CC0200) |
| **Database · Messaging** | ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-0b0b0f?style=flat&logo=postgresql&logoColor=4169E1) ![Redis](https://img.shields.io/badge/Redis-0b0b0f?style=flat&logo=redis&logoColor=FF4438) ![RabbitMQ](https://img.shields.io/badge/RabbitMQ-0b0b0f?style=flat&logo=rabbitmq&logoColor=FF6600) ![MinIO](https://img.shields.io/badge/MinIO-0b0b0f?style=flat&logo=minio&logoColor=C72E49) |
| **AI · Vision** | ![PyTorch](https://img.shields.io/badge/PyTorch-0b0b0f?style=flat&logo=pytorch&logoColor=EE4C2C) ![YOLO11-seg](https://img.shields.io/badge/YOLO11--seg-0b0b0f?style=flat&logo=ultralytics&logoColor=white) ![ONNX](https://img.shields.io/badge/ONNX_Runtime-0b0b0f?style=flat&logo=onnx&logoColor=white) ![TensorRT](https://img.shields.io/badge/TensorRT_FP16-0b0b0f?style=flat&logo=nvidia&logoColor=76B900) ![OpenCV](https://img.shields.io/badge/OpenCV-0b0b0f?style=flat&logo=opencv&logoColor=5C3EE8) ![Label Studio](https://img.shields.io/badge/Label_Studio-0b0b0f?style=flat&logoColor=white) |
| **Edge · Agent** | ![Jetson](https://img.shields.io/badge/Jetson_Orin_Nano-0b0b0f?style=flat&logo=nvidia&logoColor=76B900) ![Python](https://img.shields.io/badge/Python-0b0b0f?style=flat&logo=python&logoColor=3776AB) ![macOS](https://img.shields.io/badge/macOS-0b0b0f?style=flat&logo=apple&logoColor=white) ![Windows](https://img.shields.io/badge/Windows-0b0b0f?style=flat&logo=windows&logoColor=0078D4) |
| **Infrastructure** | ![Docker](https://img.shields.io/badge/Docker_Compose-0b0b0f?style=flat&logo=docker&logoColor=2496ED) ![Nginx](https://img.shields.io/badge/Nginx-0b0b0f?style=flat&logo=nginx&logoColor=009639) ![Cloudflare](https://img.shields.io/badge/Cloudflare_DNS-0b0b0f?style=flat&logo=cloudflare&logoColor=F38020) ![GHCR](https://img.shields.io/badge/GHCR-0b0b0f?style=flat&logo=github&logoColor=white) |
| **Contract · Quality** | ![OpenAPI](https://img.shields.io/badge/OpenAPI_3.1-0b0b0f?style=flat&logo=openapiinitiative&logoColor=6BA539) ![JSON Schema](https://img.shields.io/badge/JSON_Schema-0b0b0f?style=flat&logo=json&logoColor=white) ![SonarQube](https://img.shields.io/badge/SonarQube-0b0b0f?style=flat&logo=sonarqubeserver&logoColor=126ED3) ![CodeRabbit](https://img.shields.io/badge/CodeRabbit-0b0b0f?style=flat&logo=coderabbit&logoColor=FF570A) ![gitleaks](https://img.shields.io/badge/gitleaks-0b0b0f?style=flat&logoColor=white) |
| **Collaboration** | ![Git](https://img.shields.io/badge/Git_Flow-0b0b0f?style=flat&logo=git&logoColor=F05032) ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-0b0b0f?style=flat&logo=githubactions&logoColor=2088FF) ![Spec Kit](https://img.shields.io/badge/Spec_Kit-0b0b0f?style=flat&logo=github&logoColor=white) ![Discord](https://img.shields.io/badge/Discord-0b0b0f?style=flat&logo=discord&logoColor=5865F2) |

## ✦ 🏗 System Architecture

<p align="center">
  <img src="https://raw.githubusercontent.com/GAKDO/.github/main/profile/assets/architecture.svg" width="100%" alt="TRACE 서비스 구성도"/>
</p>

> 서비스마다 레포·이미지·DB 스키마가 따로인 **마이크로서비스**입니다. 서버끼리는 REST로 서로 부르지 않고 이벤트로만 주고받아, 한 서버가 멈춰도 다른 서버의 기록은 남습니다.

<details open>
<summary><b>1. 입구와 보안</b></summary>

- **gakdo.site (HTTPS 443)**: 화면·API·사진 업로드가 모두 이 하나의 입구로 들어옵니다. web nginx가 화면을 주고 `/api`를 gateway로 넘깁니다.
- **gateway**: 모든 API의 단일 진입점입니다. auth-server의 JWKS로 JWT를 검증하고, 역할(ADMIN·CUSTOMER·BOOTH·AGENT) × 경로 표로 막고, Redis로 요청 수를 제한합니다.
- **비밀값**: 코드·문서·커밋에 넣지 않고 환경 변수로만 받으며, 모든 레포에서 gitleaks로 검사합니다.

</details>

<details>
<summary><b>2. 마이크로서비스</b></summary>

| 서비스 | 하는 일 |
|---|---|
| **auth-server** | 회원 가입·로그인, 수령 QR 하나로 렌탈 연결, 부스·에이전트 토큰, 진단 페어링 코드, JWKS, 봉인 영수증 메일 |
| **rental-server** | 기종·기기·렌탈과 출고·수령·반납 시점 상태(OPEN → CAPTURED → GRADED → SEALED) |
| **capture-server** | 촬영 세트, 사전 서명 업로드 URL, 사진 해시 확인, 탐지 결과 저장, 사람 검수, 등급 A~D, 시점 비교 |
| **diagnostics-server** | 진단 JSON 검증, 렌탈 전후 비교, 점검 플래그(배터리 급감·부품 바뀜 등) |
| **report-server** | 렌탈별 해시 체인 연결, Ed25519 서명, 리포트, 공개 검증, 진행률 SSE |
| **inspect-worker** | 고객 폰 사진을 부스와 같은 모델로 검사(ONNX, CPU) |

</details>

<details>
<summary><b>3. 데이터와 메시징</b></summary>

- **PostgreSQL**: 서버마다 스키마를 나눕니다(auth · rental · capture · inspection · diagnostics · report). 다른 서버의 데이터는 외래 키 대신 공개 ID로만 가리킵니다.
- **RabbitMQ `trace.events`**: `capture.uploaded` → `checkpoint.graded` → `record.sealed`처럼 시점 상태가 이벤트로 흘러갑니다. 같은 이벤트를 두 번 받아도 한 번만 처리합니다.
- **MinIO**: 사진은 서버를 거치지 않고 사전 서명 URL로 바로 올라가며, 올린 뒤 SHA-256으로 확인합니다.
- **Redis**: 요청 제한과 진행률 알림에 씁니다.

</details>

<details>
<summary><b>4. AI 파이프라인</b></summary>

- 부스에서 노트북 15대를 조명별로 찍어 Label Studio로 흠집 폴리곤을 그리고, 집 PC(RTX 4070 Ti)에서 YOLO11-seg를 640px 타일로 학습합니다.
- 학습한 모델은 ONNX로 내보내 **부스 Jetson(TensorRT FP16)과 서버 inspect-worker(ONNX CPU)에 같은 버전**으로 올립니다.
- AI는 후보를 넓게 잡고 관리자가 확정·기각합니다. 그 결과는 `trace-ml review export`로 다음 학습 데이터가 됩니다.

</details>

## ✦ 🔁 CI/CD

```mermaid
flowchart LR
  dev["기능 브랜치<br/>Spec Kit 명세·계획·작업"] --> pr["PR → develop"]
  pr --> ci["CI<br/>Maven verify · JaCoCo 40%<br/>타입 검사 · Vitest<br/>ruff · pytest · 계약 검사"]
  pr --> review["CodeRabbit 한국어 리뷰<br/>SonarQube · gitleaks"]
  ci --> merge["머지"]
  review --> merge
  merge --> image["이미지 빌드<br/>GHCR"]
  image --> deploy["학교 서버<br/>Docker Compose pull · up"]
  merge --> notify["Discord 알림 · 릴리스 노트"]
```

- 레포마다 같은 워크플로를 씁니다: `backend-ci`(서버 6개), `화면 CI`(web), `python-ci`(booth·agent·ml), `계약 검사`(contracts), `비밀값 검사`·`release`·`PR 알림`(전부).
- 계약(OpenAPI·JSON Schema·코드 값)은 contracts가 원본입니다. 바꿔야 하면 코드보다 계약을 먼저 고칩니다.

## ✦ 🗂 ERD

<details>
<summary><b>핵심 테이블 보기</b> (전체 34개 중 흐름에 필요한 것만)</summary>

```mermaid
erDiagram
  DEVICE_MODEL ||--o{ DEVICE : "기종"
  DEVICE ||--o{ RENTAL : "대여"
  RENTAL ||--o{ CHECKPOINT : "출고·수령·반납"
  CAPTURE_SET ||--o{ PHOTO : "12장"
  PHOTO ||--o{ DEFECT : "흠집 폴리곤"
  CAPTURE_SET ||--o| GRADE_RESULT : "등급"
  RENTAL ||..o{ CAPTURE_SET : "공개 ID로 참조"
  RENTAL ||..o{ RECORD_CHAIN : "공개 ID로 참조"
  DIAGNOSTIC_RUN ||--o{ INSPECTION_FLAG : "점검 플래그"

  DEVICE_MODEL {
    string model_code
    string name
    int width_mm
    int depth_mm
  }
  DEVICE {
    string public_id
    string serial
    string status
  }
  RENTAL {
    string public_id
    string status
    timestamp started_at
  }
  CHECKPOINT {
    string type
    string status
    timestamp occurred_at
  }
  CAPTURE_SET {
    string source
    string status
    string quality
  }
  PHOTO {
    string face
    string light
    string camera
    string sha256
  }
  DEFECT {
    string class
    json polygon
    float confidence
    string model_version
  }
  GRADE_RESULT {
    string grade
    string rule_version
    json reasons
  }
  RECORD_CHAIN {
    int seq
    string payload_hash
    string prev_hash
    string signature
  }
  DIAGNOSTIC_RUN {
    string device_serial
    string os
    string sha256
  }
  INSPECTION_FLAG {
    string kind
    json detail
  }
```

전체 DDL은 [docs `db/V1__init.sql`](https://github.com/GAKDO/docs/blob/main/db/V1__init.sql)과 [`design/ddl.md`](https://github.com/GAKDO/docs/blob/main/design/ddl.md)에 있습니다.

</details>

## ✦ 📦 레포지토리

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
| [**gitops**](https://github.com/GAKDO/gitops) | 배포 구성 | Docker Compose |
| [**docs**](https://github.com/GAKDO/docs) | 설계서 · 결정 기록 · 안내서 · 팀 운영 | Markdown · Spec Kit |

<br/>

<div align="center">
  <a href="https://gakdo.site"><b>gakdo.site</b></a> · <a href="https://gakdo.github.io/docs/api/mvp.html">API 명세서</a> · <a href="https://github.com/GAKDO/docs">docs</a> · <a href="https://github.com/GAKDO/contracts">contracts</a>
  <br/><br/>
  <img src="https://img.shields.io/badge/-%E2%9C%A6%20TRACE-c8161d?style=flat-square" alt="TRACE"/>
</div>
