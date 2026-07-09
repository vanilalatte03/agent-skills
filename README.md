# agent-skills

Claude Code 플러그인 마켓플레이스. 여러 레포에서 공유해 쓰는 개인용 스킬 모음.

> 이 레포는 공개 레지스트리에 색인되지 않는다. URL을 알고 아래처럼 직접 추가한 사람만 설치할 수 있다.

## 설치

Claude Code 인터랙티브 세션에서:

```
/plugin marketplace add vanilalatte03/agent-skills
/plugin install review-code@agent-skills
```

이후 `/review-code` 또는 "리뷰해줘" 같은 자연어로 트리거된다.

업데이트는 `/plugin marketplace update agent-skills` 후 재설치.

## 수록 스킬

| 스킬 | 설명 |
| --- | --- |
| [review-code](plugins/review-code/skills/review-code/SKILL.md) | 차원별 서브에이전트를 병렬로 돌려 코드/브랜치 변경을 심층 리뷰한다(read-only). correctness·security·conventions 기본 활성, 10개 차원까지 확장. 컨벤션 소스와 base 브랜치는 레포에서 자동 감지한다. |

## 구조

```
.claude-plugin/
  marketplace.json          # 마켓플레이스 목록
plugins/
  review-code/
    .claude-plugin/
      plugin.json           # 플러그인 매니페스트
    skills/
      review-code/
        SKILL.md            # 스킬 본문
```

새 스킬을 추가하려면 `plugins/<name>/` 아래 같은 구조로 두고 `marketplace.json`의 `plugins` 배열에 항목을 추가한다.
