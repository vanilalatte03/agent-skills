# agent-skills

Claude Code와 Codex에서 공유해 쓰는 개인용 에이전트 스킬 모음.

> 이 레포는 공개 레지스트리에 색인되지 않는다. URL을 알고 아래처럼 직접 추가한 사람만 설치할 수 있다.

## 설치

### Claude Code

Claude Code 인터랙티브 세션에서:

```
/plugin marketplace add vanilalatte03/agent-skills
/plugin install review-code@agent-skills
```

이후 `/review-code` 또는 "리뷰해줘" 같은 자연어로 트리거된다.

업데이트는 `/plugin marketplace update agent-skills` 후 재설치.

### Codex

새 프로젝트 루트에서 프로젝트 로컬 스킬로 설치:

```powershell
python "$env:USERPROFILE\.codex\skills\.system\skill-installer\scripts\install-skill-from-github.py" --repo vanilalatte03/agent-skills --path skills/review-code --dest .\.agents\skills
```

설치 후 Codex를 재시작하면 해당 프로젝트에서 `review-code` 스킬이 잡힌다.

전역으로 쓰고 싶으면 `--dest .\.agents\skills`를 빼면 된다.

## 수록 스킬

| 스킬 | 설명 |
| --- | --- |
| [review-code](skills/review-code/SKILL.md) | 차원별 리뷰 패스로 코드/브랜치 변경을 심층 리뷰한다(read-only). correctness·security·conventions 기본 활성, 10개 차원까지 확장. 컨벤션 소스와 base 브랜치는 레포에서 자동 감지한다. |

## 구조

```
.claude-plugin/
  marketplace.json          # 마켓플레이스 목록
skills/
  review-code/
    SKILL.md                # 공통 원본, Codex 설치 대상
    agents/
      openai.yaml           # Codex UI 메타데이터
plugins/
  review-code/
    .claude-plugin/
      plugin.json           # 플러그인 매니페스트
    skills/
      review-code/
        SKILL.md            # Claude 플러그인용 복사본
```

스킬 본문은 `skills/<name>/SKILL.md`를 먼저 수정하고, Claude 플러그인용 복사본은 같은 내용으로 동기화한다.

```powershell
Copy-Item -Path .\skills\review-code\* -Destination .\plugins\review-code\skills\review-code -Recurse -Force
```

새 스킬을 추가하려면 `skills/<name>/`을 공통 원본으로 만들고, `plugins/<name>/` 아래 Claude 플러그인 구조를 추가한 뒤 `marketplace.json`의 `plugins` 배열에 항목을 추가한다.
