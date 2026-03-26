# ohmyc-evolve Documents

> 이 폴더가 omc 제품 문서의 **원본(SSOT)**입니다.
> netty-datacenter의 복사본이 아니라, 여기가 원본.

## 문서 구조

### 제품 정체성 & 스펙 (SSOT)

| 문서 | 역할 | 변경 빈도 |
|------|------|----------|
| **IDENTITY.md** | 제품 정체성, 원칙, 경계, 북극성 | 드물게 |
| **UX.md** | UX 원칙, 행동 규칙 | 가끔 |
| **CHARACTER-AGENT-SPEC.md** | Memory/Action/Growth 기술 스펙 | 가끔 |
| **VI.md** | 시각 정체성, 디자인 토큰, 컴포넌트 | 자주 |
| **FLOWS.md** | 화면 & 유저 플로우 정의 | 자주 |
| **GLOSSARY.md** | 용어 사전 | 가끔 |

### Evolve 시스템

| 문서 | 역할 |
|------|------|
| **SYSTEM.md** | Evolve 루프 시스템 설계 |
| **CHECKLIST.md** | L1~L4 평가 체크리스트 (27항목) |

## 의존 관계

```
IDENTITY.md (최상위 — 모든 결정의 출발점)
    ↓
UX.md (UX 원칙)          CHARACTER-AGENT-SPEC.md (기술 스펙)
    ↓                         ↓
VI.md (시각)              FLOWS.md (플로우)
    ↓                         ↓
CHECKLIST.md ← 위 문서들에서 평가 기준 추출
    ↓
SYSTEM.md (루프 시스템이 체크리스트를 실행)
```

## 변경 규칙

- 이 repo의 `docs/`가 원본. 여기서 수정.
- 프로토타입은 이 문서들을 기준으로 평가됨.
- 문서 변경 시 CHECKLIST.md 영향도 검토.
