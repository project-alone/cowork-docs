# 프론트엔드 프로젝트 개발 스펙 체크리스트

프로젝트 시작 전에 팀과 합의할 개발 환경 및 기술 스펙을 정리하기 위한 체크리스트입니다. 프로젝트에 필요한 항목을 선택하고, 결정한 내용과 이유를 함께 기록하세요.

## 1. 프로젝트 기본 정보

- [-] 지원 플랫폼: 모바일, 데스크톱
- [ ] 지원 브라우저 및 최소 버전
- [ ] 지원 언어와 기본 로케일
- [ ] 접근성 기준

## 2. 기술 스택

- [-] 프레임워크 기반 도구: Next.js, Nuxt 등
- [-] 언어: TypeScript
- [-] Node.js 버전 (NextJS 16.3.4에 맞는 안정화 버전)
- [-] 패키지 매니저: pnpm
- [-] 빌드 도구: 프레임워크 기본 도구(NextJS)
- [-] 렌더링 방식: CSR, SSR, SSG, Server Component
	- ISR은 논의가 필요합니다.

## 3. 코드 구조와 아키텍처

- [-] [디렉터리 구조](https://app.notion.com/p/schemas-Module-Registry-Page-JSON-4082f96d5f42810398bfc02047c94928?source=copy_link#700fbbb4ce2b4c5fb08ed0a827a7c77c)
- [-] 페이지와 라우팅 구성(업데이트 예정 - 천명기)
- [-] 공통. UI와 도메인 기능의 분리 기준
	- 공통 UI/표현 A: 재사용 컴포넌트, 편집기 화면, 모듈의 화면 표현과 UI상태
		- PropertyPanel·공통 입력 필드, Canvas의 선택·정렬 UI, 로딩·오류 표시, 슬라이더·탭의 화면 동작, 쿠폰·상품 카드 표현
	- 도메인 데이터 기능 B: 데이터 계약, 상태 관리, 저장·조회·게시, API와 서버 렌더링
		- Page/Module 스키마와 Registry, 자동 저장·Undo/Redo, Mock/실 API, Preview·Published 데이터, SSR
- [-] 서버 데이터 조회와 캐싱 방식
	- tanstack query
	- invalidate를 통해 캐시를 삭제하고 삭제가 인지되면 다시 fetch가 호출되도록 유도하는 방식
- [-] API 통신 방식 및 API 클라이언트
	- fetch, ky
- [-] 에러·로딩·빈 상태 처리 규칙
	- [-] loading - suspense
	- [-] not-found - 404
	- [-] global-error, error - 500, 또는 지역 에러

## 4. UI와 스타일링

- [ ] 스타일링 방식: CSS Modules, Tailwind CSS, CSS-in-JS 등
- [ ] 디자인 시스템 또는 UI 라이브러리 사용 여부
- [ ] 디자인 토큰: 색상, 타이포그래피, 간격, 모서리 등
- [ ] 반응형 브레이크포인트
- [ ] 다크 모드 지원 여부
- [ ] 아이콘·이미지·폰트 관리 방식
- [ ] 애니메이션과 전환 효과 사용 기준
- [ ] 접근성 규칙: 키보드 조작, 색상 대비, 시맨틱 마크업 등

## 5. 코드 작성 규칙

- [ ] ESLint 설정(작성예정 - 천명기)
- [ ] Prettier 등 코드 포맷터 설정(기본설정 json 작성 예정 - 천명기)
- [-] 파일명·변수명·컴포넌트명 규칙
	- 컴포넌트 명 - kebab
	- service - snake case
	- Server Component - NextJS File-System Convention
- [ ] Client Component와 Server Component 사이의 props를 통한 함수 전달 불가
	- [참고](https://nextjs-ko.org/docs/app/building-your-application/rendering/composition-patterns#passing-props-from-server-to-client-components-serialization)
- [ ] import 순서 - import order(eslint)
- [ ] 컴포넌트 작성 및 export 규칙
	- 기본원칙: 파일 하나당 하나의 컴포넌트
	- Compound Component 규칙: Server Component에서 import되는 가장 바깥의 WrapperComponent에서 'use client' 디렉티브 추가 후 조립하는 형태, 즉 Server Component에서 조립하지 않는다.
- [-] 주석과 문서화 기준 - AI에게 맡기는게 어떨까?
- [-] Git 브랜치 및 커밋 메시지 규칙
	- 기존 작업 방식이 있다면 따르는 것이 어떨까요?
	-  없다면 AI에게...
- [ ] PR 작성과 코드 리뷰 기준

## 6. 테스트와 품질 관리

- [-] 테스트 도구와 대상
	- 도구: vitest
	- 대상: UI Component, Page
- [ ] E2E 테스트 도구와 주요 시나리오
- [ ] 테스트 파일 위치와 명명 규칙
- [ ] 코드 커버리지 목표
- [ ] 타입 검사와 빌드 검사를 CI에 포함할지 여부
- [ ] 시각적 회귀 테스트 사용 여부
- [ ] 접근성 및 성능 점검 기준

## 7. 개발 환경과 협업

- [-] Node.js 버전 고정 방법(package.json > engines)
- [-] 필수 설치 도구와 초기 실행 절차(.vscode > settings)
	- ESLint `dbaeumer.vscode-eslint`
	- Prettier `esbenp.prettier-vscode`|
	- TypeScript `vscode.typescript-language-features`|
- [-] 로컬 API·목 데이터·Mock 서버 사용 여부
	- MSW(예제 작성 예정)
- [-] .husky - lint-staged
- [ ] 모노레포 여부와 패키지 관리 방식
	- 논의 필요

## 8. 배포와 운영

- [ ] 개발·스테이징·운영 환경 구분
- [ ] 호스팅 및 배포 플랫폼
- [ ] 빌드·배포 파이프라인
- [ ] 배포 전 검사 항목
- [ ] 정적 파일·이미지 최적화 방식
- [ ] 캐시와 CDN 설정
- [ ] 롤백 방식
- [ ] 모니터링 및 오류 추적 도구
- [ ] 웹 성능 목표와 측정 지표

## 9. 보안과 개인정보

- [ ] 비밀 키와 토큰 관리 방식
	- .env
- [ ] 인증·인가 및 세션 처리 방식
	- 백엔드 리드 필요
- [ ] XSS·CSRF 등 브라우저 보안 고려사항
- [ ] 외부 라이브러리 검토와 업데이트 기준
- [ ] CSP 등 보안 헤더 적용 여부

## 우선 결정할 핵심 항목

초기 개발 세팅을 빠르게 시작하려면 아래 항목부터 합의하는 것을 권장합니다.

1. 라우팅·상태 관리·API 통신 방식 - 정해야 함
2. 스타일링 방식과 UI 라이브러리 - choi
3. 린트·포맷터·테스트 도구 - 만들어서 전달(choi)

## 결정 사항 기록 템플릿

각 항목에 대해 다음 표를 채워 두면 이후 개발과 협업에 활용하기 좋습니다.

| 항목      | 결정 내용            | 선택 이유 | 상태  |
| ------- | ---------------- | ----- | --- |
| 프레임워크   | nextjs           |       | 미정  |
| 언어      | typescript       |       | 미정  |
| 패키지 매니저 | pnpm             |       | 미정  |
| 라우팅     | filebase routing |       | 미정  |
| 상태 관리   | 아래 참조            |       | 미정  |
| 스타일링    |                  |       | 미정  |
| 테스트 도구  | vitest(AI order) |       | 미정  |
| 배포 환경   | (인프라 통보 받아야함)    |       | 미정  |

## 상태관리 방식

- 서버 상태 - tanstack query
- 클라이언트 상태
	- seState(Component Boundary)
	- zustand(전역)
	- context api(Component Group Boundary)
	- useReducer(계산, 로직이 필요한 작업)
- URL 상태
	- search params: `?key=value&key2=value2`
	- router paramerter: `/edit/detail/AW01012`

## 참고 링크
[NextJS Play Ground](https://app-router.vercel.app/)
