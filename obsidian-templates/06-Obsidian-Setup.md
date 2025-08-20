# ⚙️ Obsidian 설정 가이드

> **설정 일자**: {{date:YYYY-MM-DD}}  
> **Obsidian 버전**: v1.5.x 이상 권장  
> **대상 플랫폼**: Windows, macOS, Linux, Mobile

**태그**: #옵시디언설정 #MCP연동 #자동화

---

## 🚀 **빠른 시작 가이드**

### 1️⃣ Obsidian 다운로드 및 설치
```bash
# macOS (Homebrew)
brew install --cask obsidian

# Windows (Chocolatey)
choco install obsidian

# 또는 직접 다운로드
# https://obsidian.md/download
```

### 2️⃣ Vault 생성
1. Obsidian 실행
2. "Create new vault" 클릭
3. Vault 이름: `EduArt-Engineer-CI`
4. 위치: 원하는 폴더 선택

### 3️⃣ 기본 폴더 구조 생성
```
EduArt-Engineer-CI/
├── 00-Dashboard/
├── 01-Ideas-Inbox/
├── 02-Whitepapers/
├── 03-Knowledge-Base/
├── 04-Templates/
├── 05-Archives/
└── 99-Meta/
```

---

## 🔌 **필수 플러그인 설치**

### Core 플러그인 (무료)

#### 1. **Dataview** 
**설치**: Settings → Community Plugins → Browse → "Dataview" 검색 → Install

**설정**:
```yaml
# Settings → Dataview
Enable JavaScript Queries: ✅ 체크
Enable Inline Queries: ✅ 체크
Enable Dataview JS: ✅ 체크
```

**주요 기능**:
- 백서패키지 현황 자동 집계
- 프로젝트 진행률 추적
- 동적 대시보드 생성

---

#### 2. **Templates**
**설치**: Core Plugins → Templates → 활성화

**설정**:
```yaml
# Settings → Templates
Template folder location: "04-Templates"
Date format: "YYYY-MM-DD"
Time format: "HH:mm"
```

**템플릿 사용법**:
- `Ctrl/Cmd + P` → "Templates: Insert template"
- 또는 선호도에서 핫키 설정

---

#### 3. **Graph View** (기본 활성화)
**설정 최적화**:
```yaml
# Graph View 설정
Filters:
  - 태그: #백서, #아이디어, #기술패턴
  - 경로: 02-Whitepapers, 03-Knowledge-Base

Display:
  - Node size: 링크 수에 비례
  - Link thickness: 연결 강도에 비례
  - Repel force: 0.8
  - Link force: 0.3
```

---

#### 4. **Tag Wrangler**
**설치**: Community Plugins → "Tag Wrangler" 검색 → Install

**주요 기능**:
- 태그 계층 구조 관리
- 태그 일괄 변경
- 태그 통계 및 정리

**권장 태그 구조**:
```
#프로젝트/
  ├── #프로젝트/백서
  ├── #프로젝트/진행중
  ├── #프로젝트/완성
  └── #프로젝트/보류

#카테고리/
  ├── #카테고리/도구
  ├── #카테고리/비즈니스
  ├── #카테고리/교육
  ├── #카테고리/게임
  └── #카테고리/데이터시각화

#우선순위/
  ├── #우선순위/높음
  ├── #우선순위/보통
  └── #우선순위/낮음
```

---

### Premium 플러그인 (유료 권장)

#### 5. **Obsidian Sync** ($10/월)
**기능**:
- 다중 기기 실시간 동기화
- 버전 히스토리 관리 (1년)
- 팀 공유 Vault 지원
- 엔드투엔드 암호화

**설정**:
```yaml
# Sync 최적화 설정
Sync frequency: Every 10 seconds
File sync: All file types
Core plugin sync: ✅ Enable
Community plugin sync: ✅ Enable
Theme sync: ✅ Enable
```

#### 6. **Obsidian Publish** ($20/월)
**기능**:
- 지식베이스 웹 퍼블리싱
- 커스텀 도메인 지원
- SEO 최적화
- 접근 권한 관리

**활용 방안**:
- 완성된 프로젝트 포트폴리오 공개
- WebAppsBook Cast 보조 자료
- dtslib.com 기술 블로그 연동

---

## 🔗 **GitHub 연동 설정**

### 방법 1: Git 플러그인 사용
**설치**: Community Plugins → "Obsidian Git" 검색 → Install

**설정**:
```yaml
# Obsidian Git 설정
Vault backup interval: 10 minutes
Commit message: "vault backup: {{date}}"
Pull updates on startup: ✅ Enable
Disable push: ❌ Disable
Remote repository URL: 
  https://github.com/dimas-40/eduart-engineer-archive.git
```

### 방법 2: 수동 Git 동기화
```bash
# Vault 폴더에서 실행
git init
git remote add origin https://github.com/dimas-40/eduart-engineer-archive.git

# 동기화 스크립트 생성
echo '#!/bin/bash
git add .
git commit -m "Obsidian vault sync: $(date)"
git push origin main
git pull origin main' > sync.sh
chmod +x sync.sh

# 주기적 실행 (crontab)
# */30 * * * * cd /path/to/vault && ./sync.sh
```

---

## 📊 **Dataview 쿼리 설정**

### 대시보드용 쿼리 템플릿

#### 프로젝트 현황 테이블
```dataview
TABLE 
  project-status as "상태",
  progress as "진행률",
  category as "카테고리",
  priority as "우선순위"
FROM "02-Whitepapers"
WHERE project-status != null
SORT priority ASC, progress DESC
```

#### 이번 주 할 일
```dataview
TASK
FROM "00-Dashboard" OR "01-Ideas-Inbox"
WHERE contains(tags, "#이번주")
AND !completed
```

#### 기술 스택 사용 통계
```dataview
TABLE 
  tech-name as "기술",
  usage-count as "사용 횟수",
  proficiency as "숙련도"
FROM "03-Knowledge-Base"
WHERE contains(tags, "#기술스택")
SORT usage-count DESC
```

#### 최근 아이디어 목록
```dataview
LIST
FROM "01-Ideas-Inbox"
WHERE file.ctime >= date(today) - dur(7 days)
SORT file.ctime DESC
```

---

## 🎨 **테마 및 외관 설정**

### 권장 테마
1. **Minimal** - 깔끔하고 미니멀한 디자인
2. **Things** - 할 일 관리에 최적화
3. **Blue Topaz** - 다양한 커스터마이징 옵션

### CSS 스니펫 (커스터마이징)
```css
/* .obsidian/snippets/eduart-custom.css */

/* 백서패키지 상태별 색상 */
.tag[href="#프로젝트/진행중"] {
  background-color: #28a745;
  color: white;
}

.tag[href="#프로젝트/완성"] {
  background-color: #007bff;
  color: white;
}

.tag[href="#프로젝트/보류"] {
  background-color: #ffc107;
  color: black;
}

/* 우선순위별 강조 */
.tag[href="#우선순위/높음"] {
  background-color: #dc3545;
  color: white;
  font-weight: bold;
}

/* 카테고리별 아이콘 */
.tag[href="#카테고리/도구"]:before {
  content: "🛠️ ";
}

.tag[href="#카테고리/비즈니스"]:before {
  content: "💼 ";
}

.tag[href="#카테고리/교육"]:before {
  content: "🎓 ";
}
```

---

## ⚡ **워크플로우 자동화**

### Templater 고급 설정
**설치**: Community Plugins → "Templater" 검색 → Install

**동적 템플릿 예시**:
```javascript
// 백서 템플릿 자동화
<%*
const projectName = await tp.system.prompt("프로젝트 이름을 입력하세요:");
const category = await tp.system.suggester(
  ["도구", "비즈니스", "교육", "게임", "데이터시각화"],
  ["tool", "business", "education", "game", "data-viz"]
);
const priority = await tp.system.suggester(
  ["높음", "보통", "낮음"],
  ["high", "medium", "low"]
);
%>

# 📄 백서: <% projectName %>

> **작성일**: <% tp.date.now("YYYY-MM-DD") %>  
> **카테고리**: <% category %>  
> **우선순위**: <% priority %>

**태그**: #백서 #카테고리/<% category %> #우선순위/<% priority %>
```

### QuickAdd 액션 설정
**설치**: Community Plugins → "QuickAdd" 검색 → Install

**빠른 액션 구성**:
```yaml
# QuickAdd 매크로
1. "새 아이디어 수집"
   - 템플릿: Ideas-Capture
   - 폴더: 01-Ideas-Inbox
   - 파일명: "{{DATE}}-{{VALUE:아이디어제목}}"

2. "주간 리뷰 생성"
   - 템플릿: Weekly-Review
   - 폴더: 00-Dashboard
   - 파일명: "Weekly-Review-{{DATE:YYYY-WW}}"

3. "기술 패턴 추가"
   - 템플릿: Technical-Pattern
   - 폴더: 03-Knowledge-Base
   - 파일명: "{{VALUE:패턴이름}}"
```

---

## 📱 **모바일 설정**

### 모바일 앱 최적화
```yaml
# Mobile 설정
Show ribbon: ❌ 숨김
Show status bar: ❌ 숨김
Default view mode: Reading view
Swipe gesture: Enable

# 모바일용 플러그인
Advanced Mobile Toolbar: ✅ 설치
Mobile Toolbar: ✅ 설치
```

### 빠른 캡처 설정
- 홈스크린에 "새 아이디어" 위젯 추가
- 음성 인식을 통한 아이디어 수집
- 사진 첨부를 통한 영감 저장

---

## 🔧 **성능 최적화**

### 대용량 Vault 관리
```yaml
# 성능 설정
File recovery: 7 days
Auto pair brackets: ✅ Enable
Auto pair markdown syntax: ✅ Enable
Smart indent lists: ✅ Enable

# 캐시 최적화
Index delay: 1000ms
Live preview: ❌ 무거운 문서에서는 비활성화
```

### 백업 전략
1. **Obsidian Sync** (실시간)
2. **GitHub 동기화** (버전 관리)
3. **로컬 백업** (일간)

```bash
# 자동 백업 스크립트
#!/bin/bash
VAULT_PATH="/path/to/EduArt-Engineer-CI"
BACKUP_PATH="/path/to/backups"
DATE=$(date +%Y%m%d)

cp -r "$VAULT_PATH" "$BACKUP_PATH/vault-backup-$DATE"
find "$BACKUP_PATH" -name "vault-backup-*" -mtime +30 -delete
```

---

## 🆘 **문제 해결**

### 일반적인 문제들

#### 1. 동기화 충돌
```yaml
해결법:
1. .obsidian/workspace.json 파일 삭제
2. Obsidian 재시작
3. 수동으로 충돌 파일 병합
```

#### 2. 플러그인 오류
```yaml
해결법:
1. Safe mode에서 실행
2. 플러그인 하나씩 비활성화하여 원인 찾기
3. 플러그인 재설치
```

#### 3. 성능 저하
```yaml
해결법:
1. 너무 많은 플러그인 비활성화
2. 대용량 파일 분리
3. Graph view 필터 적용
```

---

## 🎯 **다음 단계**

### 설치 완료 체크리스트
- [ ] Obsidian 다운로드 및 설치
- [ ] EduArt-Engineer-CI Vault 생성
- [ ] 폴더 구조 설정
- [ ] 필수 플러그인 설치 (Dataview, Templates, Tag Wrangler)
- [ ] GitHub 연동 설정
- [ ] 템플릿 파일 다운로드 및 설정
- [ ] 대시보드 Dataview 쿼리 테스트
- [ ] 모바일 앱 설정 (선택사항)

### 고급 설정 (선택사항)
- [ ] Obsidian Sync 구독 및 설정
- [ ] Templater 고급 자동화 설정
- [ ] QuickAdd 매크로 구성
- [ ] 커스텀 CSS 스니펫 적용
- [ ] 백업 전략 수립

---

**🧠 이제 Obsidian이 EduArt Engineer CI의 지식 관리 허브로 완벽하게 준비되었습니다!**

**🔗 관련 문서**: [[Main Dashboard]], [[Technical Patterns]], [[Project Overview]]