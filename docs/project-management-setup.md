# 🎯 EduArt Engineer CI - 프로젝트 관리 설정 가이드

## 📋 GitHub Projects 칸반 보드 설정

### 1️⃣ GitHub Projects 생성
1. 저장소 → **Projects** 탭 클릭
2. **New project** → **Board** 선택
3. 프로젝트명: `EduArt Engineer CI Dashboard`

### 2️⃣ 컬럼 구성
```
📋 Backlog (아이디어 대기)
├── 💡 Ideas Pool
└── 🔍 Research Needed

🚀 In Progress (진행 중)
├── 📝 백서 작성
├── 🎨 프롬프트 설계  
├── 🧠 메타프롬프트 작성
└── 💻 웹앱 구현

✅ Done (완성)
├── 🎉 웹앱 완성
└── 📚 컨텐츠화 완료
```

### 3️⃣ 자동화 규칙 설정
```yaml
# 새 이슈 생성 시 자동으로 Backlog로 이동
when: issue.created
then: move to "Backlog"

# 라벨 기반 자동 분류
when: issue.labeled("백서")
then: move to "백서 작성"

when: issue.labeled("웹앱")  
then: move to "웹앱 구현"

when: issue.closed
then: move to "Done"
```

---

## 🏷️ 라벨 시스템

### 단계별 라벨
- 🟦 `백서` - 백서 작성 단계
- 🟨 `프롬프트` - 프롬프트 설계 단계  
- 🟪 `메타프롬프트` - 메타프롬프트 작성 단계
- 🟩 `웹앱` - 웹앱 구현 단계

### 우선순위 라벨
- 🔴 `urgent` - 긴급 (24시간 내)
- 🟠 `high` - 높음 (1주일 내)
- 🟡 `medium` - 보통 (2주일 내)
- 🟢 `low` - 낮음 (1개월 내)

### 카테고리 라벨
- 🛠️ `tool` - 사용자 도구
- 💼 `business` - 비즈니스 앱
- 🎓 `education` - 교육 플랫폼
- 🎮 `game` - 게임 & 엔터테인먼트
- 📊 `data-viz` - 데이터 시각화

---

## 📊 이슈 템플릿

### 새 백서패키지 이슈 템플릿
```markdown
## 🎯 프로젝트 개요
**프로젝트명**: [PROJECT_NAME]
**카테고리**: [tool/business/education/game/data-viz]
**우선순위**: [urgent/high/medium/low]

## 💡 핵심 아이디어
[해결하고자 하는 문제와 솔루션을 간단히 설명]

## 👥 타겟 사용자
[주요 사용자층 정의]

## ✅ 체크리스트
- [ ] 백서 작성 완료
- [ ] 프롬프트 설계 완료  
- [ ] 메타프롬프트 작성 완료
- [ ] 웹앱 구현 완료
- [ ] 테스트 및 배포 완료
- [ ] 컨텐츠화 완료

## 🔗 관련 링크
- 백서패키지 폴더: [링크]
- 라이브 데모: [배포 후 추가]
```

### 버그 리포트 템플릿  
```markdown
## 🐛 버그 설명
[버그에 대한 명확한 설명]

## 🔄 재현 방법
1. ...
2. ...
3. ...

## 💥 예상 결과 vs 실제 결과
**예상**: [예상했던 동작]
**실제**: [실제 발생한 현상]

## 🖥️ 환경 정보
- 브라우저: [Chrome/Firefox/Safari/Edge]
- 디바이스: [Desktop/Mobile/Tablet]
- 화면 크기: [1920x1080/...]

## 📷 스크린샷
[가능하면 스크린샷 첨부]
```

---

## 🔄 워크플로우 최적화

### 일일 스탠드업 (자동화)
```yaml
# 매일 오전 9시에 진행현황 요약 생성
name: Daily Standup
on:
  schedule:
    - cron: '0 09 * * 1-5'

jobs:
  standup:
    runs-on: ubuntu-latest
    steps:
      - name: 진행현황 요약 생성
        run: |
          echo "📊 오늘의 EduArt Engineer CI 현황"
          echo "🚀 진행 중인 프로젝트: $(gh issue list --label 'in-progress' --json number | jq length)"
          echo "✅ 어제 완료된 작업: $(gh issue list --search 'closed:yesterday' --json number | jq length)"
          echo "🎯 오늘의 목표: 새 백서패키지 1개 시작"
```

### 주간 회고 (자동화)
```yaml
# 매주 금요일 오후 5시에 주간 회고 생성
name: Weekly Retrospective  
on:
  schedule:
    - cron: '0 17 * * 5'

jobs:
  retrospective:
    runs-on: ubuntu-latest
    steps:
      - name: 주간 회고 생성
        run: |
          echo "📈 이번 주 성과 분석"
          echo "🎉 완성된 백서패키지: X개"
          echo "🚀 배포된 웹앱: X개"  
          echo "📺 제작 가능한 유튜브 컨텐츠: X개"
          echo "💡 다음 주 개선점: ..."
```

---

## 📱 모바일 앱 추천

### GitHub Mobile
- **무료** iOS/Android 앱
- 이슈 관리, 코드 리뷰 가능
- 푸시 알림으로 실시간 업데이트

### Linear Mobile  
- **$8/월** 프리미엄 앱
- 최고 수준의 사용자 경험
- 오프라인 동기화 지원

---

## 💰 예산별 추천 조합

### 🆓 무료 조합 (0원/월)
```
GitHub Actions + GitHub Projects + GitHub Mobile
→ 기본적인 자동화와 프로젝트 관리
```

### 💎 프리미엄 조합 ($18/월)
```
위 무료 조합 + Linear + Notion
→ 전문가급 프로젝트 관리와 지식 관리
```

### 🚀 엔터프라이즈 조합 ($148/월)
```
모든 도구 + Zapier + Mixpanel  
→ 완전 자동화된 비즈니스 프로세스
```

---

**🎯 추천**: 먼저 무료 조합으로 시작해서 워크플로우를 익힌 후, 필요에 따라 점진적으로 유료 도구 추가!
