# v001 — 초기 인터랙티브 프로토타입

> 빌드일: 2026-03-26
> 피델리티: **L2** (L1 6/6 · L2 6/7 · L3 7/9)
> 파일: `index.html` — 단일 파일, 외부 의존성 없음 (Google Fonts 제외)

---

## 빌드 목표

CHECKLIST.md L1 플로우 항목 6개 전부 커버. L2/L3 기준도 최대한 충족.

---

## 구현된 플로우 (F1–F6)

### F1: 온보딩 → 캐릭터 선택 → 첫 대화
- **Splash** → 2초 후 자동 전환
- **Welcome** — 브랜드 인트로, "시작하기" CTA
- **Onboard Wake** — 기상 시간 선택 (4 옵션, 탭 → 자동 다음 단계)
- **Onboard Vibe** — 분위기 선택 (4 옵션) → 선택 시 메모리 등록
- **Character Select** — Lumi 피처드 카드(전체폭) + 4개 추가 캐릭터 2열 그리드
- **First Chat** — 자동재생 대화 시퀀스 (타이핑 인디케이터 포함) → 홈으로

### F2: 선제 발화 (Proactive Turn)
- First Chat: Lumi가 먼저 인사 (유저 액션 없이 자동 재생)
- Main Chat: 화면 진입 시 Lumi의 기억 참조 메시지가 이미 있음
- Push Notification: 🔔 버튼 또는 홈 진입 8초 후 Lumi 먼저 말 거는 알림 시뮬레이션

### F3: 유저 주도 턴
- 채팅 화면 자유 입력 (Enter 또는 전송 버튼)
- 홈 카드 퀵 리플라이 버튼 ("좋아!", "나중에", "대화하기 →")
- 대화 탭에서 Lumi 행 탭 → 채팅 화면으로 직접 진입

### F4: 4탭 구조
- **홈** — 피처드 카드, 온도, 하루 사이클, 부재 시뮬레이션
- **둘러보기** — 6개 캐릭터 2열 그리드, 검색바, 카테고리 칩
- **대화** — 대화 목록 (Lumi 활성 + 읽지 않음 배지)
- **프로필** — 통계 (캐릭터 수, 온도, 함께한 날) + 설정 항목
- 탭바: `backdrop-filter` 글래스 소재, 활성 탭 tint 컬러

### F5: 부재 → 복귀 시나리오
- 홈 하단 "3일 후로 이동 →" 버튼 탭
- 온도 36.5 → 34.5°C 애니메이션 하강 (0.16s 인터벌)
- 상태 메시지 변화: 하강 중 → 복귀 감지 → 회복 중
- 복귀 버튼 탭 → Push 알림 발동 + 온도 서서히 36.0°C 회복
- 회복 완료 후 원상태로 리셋

### F6: 하루 사이클 시뮬레이션
- 홈 탭 사이클 카드 — 🌅아침 / ☀️낮 / 🌆저녁 / 🌙밤 탭
- 탭 전환 시 업데이트: 인사말, 제목, Lumi 메시지, 상태 텍스트, 사이클 본문

---

## 디자인 구현 (VI.md)

| 항목 | 상태 | 비고 |
|------|------|------|
| Tint `#FF8552` | ✅ | CTA, 활성 탭, 유저 버블, 필, 온도 |
| CSS 변수 토큰 | ✅ | `--tint`, `--r-*`, `--sh-*` 등 전체 변수화 |
| Apple HIG 8pt 그리드 | ✅ | 패딩 8/12/16/20/24px, 터치 타겟 44pt 이상 |
| Plus Jakarta Sans 워드마크 | ✅ | weight 800, `ohmyc` 텍스트 전용 |
| 폰트: -apple-system | ✅ | 시스템 폰트 스택 |
| 보더 라디우스 스케일 | ✅ | 10/14/20/24/pill |
| 글래스 소재 | ✅ | `backdrop-filter:blur(20px) saturate(180%)` — 탭바, 채팅 헤더, 푸시 알림, 온도 필 |
| Breathe 애니메이션 | ✅ | scale 1↔1.15, opacity 0.3↔0.6, 3s ease-in-out infinite |
| 타이핑 인디케이터 | ✅ | 3-dot staggered fade |
| Pulse-ring 애니메이션 | ✅ | 온도 dot keyframe |
| 캐릭터 카드 2:3 | ✅ | `aspect-ratio:2/3`, 그래디언트 배경, 오버레이, alive dot |
| 채팅 버블 스펙 | ✅ | char 좌(`#F0E6E6`, bottom-left-radius:4px), user 우(`#FF8552`, bottom-right-radius:4px) |
| 메모리 필 | ✅ | 글래스, tint-tinted, 🧠 아이콘 |
| 온도 글래스 필 | ✅ | 펄스 dot + 숫자, 상태별 색 변화 |
| 다크 모드 | ✅ | `prefers-color-scheme:dark` 모든 토큰 오버라이드 |
| Reduce Motion | ✅ | `prefers-reduced-motion` 적용 |
| iPhone 뷰포트 393×852 | ✅ | `.frame` 고정 크기, Dynamic Island 포함 |
| 화면 전환 | ✅ | opacity + translateX, cubic-bezier |

---

## 주요 컴포넌트

- `glass` — backdrop-filter 유틸리티 클래스
- `temp-pill` / `temp-dot` — 온도 표시
- `memory-pill` — 기억 참조 인디케이터
- `alive` / `alive-sm` — Breathe 애니메이션 점
- `bubble-group.char` / `.user` — 채팅 버블
- `char-card` (2:3) — 캐릭터 카드
- `opt` / `cycle-tab` / `cat-chip` — 선택형 UI

---

## 알려진 갭 (다음 이터레이션 우선순위)

1. **I3** (minor) — 캐릭터 성장 변화 시각화: tone shift 없음, 레벨 없음
2. **V9** (minor) — 브랜드 보이스: 일부 레이블 더 친근하게
3. **P1** (minor) — 화면 전환 애니메이션 polish: 현재 fade+slide, 더 native하게
4. **P2** (minor) — 마이크로인터랙션: 버튼 haptic 피드백 시각화 개선
5. **P4** (minor) — 접근성: aria-label 추가

---

## 파일 구조

```
v001/
├── index.html     ← 단일 파일 프로토타입 (CSS+JS 인라인)
├── meta.json      ← 버전 메타데이터 + 체크리스트 점수
└── changelog.md   ← 이 파일
```
