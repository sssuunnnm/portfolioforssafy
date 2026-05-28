# Portfolio Source Code References

포트폴리오 페이지에 노출하지 않은 실제 소스코드 출처/근거 정리.

---

## 1. OneStep (Android)

**Repository**: `S14P11A508/android`

### 디자인 토큰
- 색상·타이포그래피: `presentation/theme/Color.kt`, `presentation/theme/Type.kt`

### GPS 가드 수치 (SECTION 03 — STATE DERIVATION 표 기준)
모든 상수는 실제 코드 기준값.

| 상수 | 값 | 위치 |
|---|---|---|
| `accuracy <` | 20f | `domain/usecase/TrackLocationUseCase.kt` L14 |
| `distance <` | 100m | `presentation/home/walk/WalkViewModel.kt` L85-89 |
| `ARRIVE_MAX_ACCURACY` | 10f | `WalkViewModel.kt` |
| `ARRIVE_STABLE_COUNT` | 3 | `WalkViewModel.kt` |
| `DESTINATION_THRESHOLD` | 20.0m | `WalkViewModel.kt` |
| `ARRIVE_MIN_ELAPSED_MS` | 3000ms | `WalkViewModel.kt` |

### SECTION 04 — WalkViewModel 상태 흐름 다이어그램
StateFlow 노드 매핑 출처: `presentation/home/walk/WalkViewModel.kt`

### 레이어 맵 모듈 경로 매핑
- VM: `presentation/home/walk/WalkViewModel.kt`, `presentation/features/firechat/FireChatViewModel.kt`
- Component: `presentation/features/firechat/components/PixelChatBubble.kt`
- UseCase: `domain/usecase/TrackLocationUseCase.kt`, `domain/usecase/CalculateDistanceUseCase.kt`
- Repository (interface): `domain/repository/WalkRepository.kt`
- Tracker: `data/local/location/LocationTracker.kt`
- Service: `data/local/service/WalkTrackingService.kt`
- Token: `data/local/TokenManager.kt`

---

## 2. ShadowEng (Android)

### 화면별 파일 매핑
| 화면 | 파일 |
|---|---|
| 홈 | `HomeScreen.kt` |
| 학습 세션 | `StudySessionScreen.kt` |
| 평가 결과 | `StudyReportScreen.kt` |
| 게임 | `GamePlayScreen.kt` |

### 핵심 코드 참조
- 어노테이션 매핑: `EvaluationAnnotationMapper.kt` — status 문자열 → 색·모양 어노테이션
- MVI 계약: `GamePlayContract.kt` — State · Intent · Effect 분리
- Canvas 좌표 로직: `AnnotatedSentenceView.kt` — getBoundingBox(charIndex) 기반

### Auth 모듈 구조
- api: `AuthApi.kt`, `dto/AuthDtos.kt`
- data: `TokenStorage.kt`
- presentation: `AuthScreen.kt`, `AuthUiState.kt`, `AuthViewModel.kt`, `SetNickNameScreen.kt`, `SetNickNameViewModel.kt`, `SplachScreen.kt`, `SplashViewModel.kt`
- repository: `AuthRepository.kt`, `AuthRepositoryImpl.kt`

---

## 3. NGRAS-FE (Web Frontend)

### SSE / 진행률 추적
- 훅: `src/features/regulation/hooks/useRegulationProcessingTracker.ts`
- 서비스: `regulationService.streamDocumentProgress()`

### Auth / 토큰 갱신
- API 클라이언트: `src/api/client.ts` (응답 인터셉터, 401 분기)

---

## 노출 정책 메모
포트폴리오 페이지에서는 "X.kt 기준", "generated from repo" 등 출처 라벨을 노출하지 않는다.
파일명이 컨텐츠 본문(예: 레이어 맵 모듈 카드의 path, MVI Contract 클래스명)인 경우는 유지.
