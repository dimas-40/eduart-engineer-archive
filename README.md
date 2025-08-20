# 📚 EduArt Engineer CI - 마감작업 아카이브

> **작가지망생 박씨 & Claude MCP 협업 프로젝트**  
> 백서 중심 워크플로우 & 웹앱 구현 자료실

## 🎯 프로젝트 목적
- 마감작업 프로들의 백서 기반 작업기술 구현
- Claude 아티팩트와 MCP 연동 백서 패키지 시스템
- 체계적 모델링을 통한 웹앱 구현 프로세스
- dtslib.com 기반 WebAppsBook Cast 컨텐츠 제작

---

## 📁 **저장소 구조 (2대 카테고리)**

### 📝 **1. 채팅대화로그 카테고리**
```
📦 chat-logs/
├── 📄 session-YYYY-MM-DD-HH-MM.md     # 개별 대화 세션
├── 📄 summary-weekly.md               # 주간 대화 요약
└── 📄 insights-archive.md             # 핵심 인사이트 모음
```

### 📋 **2. 백서패키지 카테고리**
```
📦 whitepaper-packages/
├── 📂 package-001-project-name/
│   ├── 📄 1-whitepaper.md            # 1. 백서 (핵심 아이디어)
│   ├── 📄 2-prompt.md                # 2. 프롬프트 (구현 지침)
│   ├── 📄 3-meta-prompt.md           # 3. 메타프롬프트 (모델링 전략)
│   └── 📂 4-webapp-code/             # 4. 웹앱 구현 코드
│       ├── 📄 index.html
│       ├── 📄 style.css
│       ├── 📄 script.js
│       └── 📄 README.md
├── 📂 package-002-next-project/
│   └── (동일 구조)
└── 📄 packages-index.md              # 전체 패키지 목록
```

---

## 🔄 **백서패키지 워크플로우**

### **Phase 1**: 백서 작성 (Ideation)
```
아이디어 → 백서 문서화 → 핵심 개념 정리
```

### **Phase 2**: 프롬프트 설계 (Specification)
```
백서 → 구현 프롬프트 → 기술적 요구사항 명세
```

### **Phase 3**: 메타프롬프트 생성 (Modeling)
```
프롬프트 → 메타프롬프트 → Claude 모델링 전략 수립
```

### **Phase 4**: 웹앱 구현 (Implementation)
```
메타프롬프트 → 웹앱 코드 → 실제 동작하는 프로토타입
```

---

## 🚀 **사용법**

### 새 백서패키지 시작하기:
1. `whitepaper-packages/` 에 새 패키지 폴더 생성
2. `1-whitepaper.md` 부터 순서대로 작성
3. 각 단계별로 채팅로그에 진행과정 기록
4. 완성된 웹앱으로 검증 및 피드백

### 채팅로그 관리:
- 실시간 대화는 `chat-logs/` 에 세션별 저장
- 주요 결정사항과 인사이트 별도 정리
- 백서패키지와 연결하여 추적성 확보

---

**📧 Contact**: dtslib.com - WebAppsBook Cast  
**🎬 Channel**: EduArt Engineer CI