# v001 Changelog

> Built by netty · 2026-03-26
> Goal: L1 Flow — 모든 핵심 플로우 존재

## 새로 만든 것 (19 screens)

### Onboarding (F1) ✅
- Splash: 워드마크 + 태그라인 + 자동 전환
- Welcome: CTA + 제품 설명
- Question (Wake Time): 5개 시간 옵션 선택
- Question (Vibe): 3개 컴패니언 스타일 카드
- Character Select: Lumi 히어로 카드 (alive dot, breathe animation) + Coming Soon 3장
- First Chat: Lumi가 먼저 인사 → 이름 수집 → 기상시간 recall → 기분 수집. Memory Pill 3회 표시
- Closing: "Your character is alive." + 온도 표시

### Day Cycle (F6) ✅
- Home (Evening/Day 1): 밤 배경, 굿나잇 메시지, 온도 36.8°C
- Push Notification: 잠금화면 스타일 알림 시뮬레이션
- Home (Morning): 아침 배경, 온도 36.7°C (자연 냉각)
- Day 2 Morning Chat: 이름+기상시간 recall, 일정 수집 (Meeting/Gym/Chill), 리마인더 제안
- Home (Daytime): 온도 37.2°C (+0.5)
- Afternoon Chat: 아침 일정 recall + 후속 질문
- Evening Chat: Summary card + 무죄책감 리뷰 + 기분 저장
- Home (Night): 온도 37.8°C, 하루 요약

### Proactive Turn (F2) ✅
- 푸시 알림 → 아침 대화 (캐릭터가 먼저 시작)
- 오후 체크인 (캐릭터가 아침 일정 recall)

### User Initiated Turn (F3) ✅
- Home에서 "Chat with Lumi" 탭으로 유저 주도 대화 진입
- Chats 탭에서 대화 재진입

### Absence → Return (F5) ✅
- "2 weeks later" 전환 오버레이
- 온도 34.5°C (자연 냉각, 죄책감 없음)
- 레벨 보존 (Friend)
- 기억 보존 (2주 전 대화 recall)
- 조심스러운 톤 → 빠른 회복

### 4-Tab Structure (F4) ✅
- Home / Discover / Chats / Profile
- Tab bar: Glass 소재, 활성 탭 tint 컬러
- Discover: 검색바 + 카테고리 + 4캐릭터 그리드
- Chats: 대화 목록 + 온도 표시 + alive dot
- Profile: 유저 정보 + 설정 + Apple Settings 패턴

## 기술 구현

- 단일 HTML 파일 (41KB)
- VI.md 디자인 토큰 CSS 변수 사용
- 다크 모드 대응 (prefers-color-scheme)
- Breathe animation (alive dot)
- Warm pulse animation (temperature pill)
- Typing indicator (3 dots)
- Memory Pill (glass 소재)
- Chat engine (async message queue + typing delay)
- Google Fonts (Plus Jakarta Sans 800 — 워드마크 전용)
