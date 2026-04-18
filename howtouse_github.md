# Warvote 협업을 위한 GitHub 사용 가이드

이 문서는 **Warvote** 프로젝트 저장소를 공유하고, 팀원들이 효율적으로 협업하기 위한 가이드라인을 제공합니다.

## 1. 초기 세팅 (가져오기)

저장소를 처음 내 컴퓨터로 가져오려면 아래 명령어를 사용합니다.

```bash
git clone https://github.com/deok22-cmd/WarVote.git
cd WarVote
```

## 2. 기본 업무 프로세스 (중요!)

협업 시 충돌(Conflict)을 방지하기 위해 다음 순서를 반드시 지켜주세요.

1.  **작업 시작 전:** 항상 최신 코드를 받아옵니다.
    ```bash
    git pull origin main
    ```
2.  **코드 수정:** 자신의 작업을 진행합니다.
3.  **변경 내용 확인 및 추가:**
    ```bash
    git status          # 변경된 파일 확인
    git add .           # 모든 변경사항 반영 준비
    ```
4.  **커밋(Commit):** 변경 내용을 기록합니다. (의미 있는 메시지 작성)
    ```bash
    git commit -m "feat: CRM 유권자 등록 정규식 추가"
    ```
5.  **서버에 반영(Push):** 내 작업 내용을 GitHub에 올립니다.
    ```bash
    git push origin main
    ```

## 3. 효율적인 협업 규칙 (Convention)

### 3.1 브랜치(Branch) 활용 (권장)
`main` 브랜치에 직접 커밋하기보다, 기능별로 브랜치를 만들어 작업한 뒤 **Pull Request(PR)**를 통해 합치는 것이 안전합니다.
*   예: `feature/crm-sms`, `feature/intelligence-api`

### 3.2 커밋 메시지 규칙
누가 봐도 어떤 작업을 했는지 알 수 있도록 접두사를 붙여주세요.
*   `feat: ` 새로운 기능 추가
*   `fix: ` 버그 수정
*   `docs: ` 문서 수정 (PRD, 설계서 등)
*   `style: ` 코드 포맷팅, 세미콜론 누락 등 (코드 변경 없음)

## 4. 충돌(Conflict) 해결하기

만약 두 사람이 같은 파일의 같은 줄을 고치고 `push`하면 충돌이 발생합니다.
1.  `git pull`을 실행하면 충돌 난 부분이 파일에 표시됩니다 (`<<<< HEAD ... >>>>`).
2.  해당 부분을 직접 열어 내용을 수정(Merge)합니다.
3.  다시 `git add` -> `git commit` -> `git push`를 진행합니다.

## 5. AI와 함께 협업하기

본 프로젝트는 **BMad 방법론**에 따라 `docs/` 폴더에 기획 및 설계 문서가 최신화되어 있습니다.
*   새로운 기능을 코딩하기 전, 반드시 `docs/prd.md`와 `docs/architecture.md`를 먼저 읽어보세요.
*   문서가 수정되었다면, AI(Antigravity 등)에게 "수정된 문서를 바탕으로 코드를 짜줘"라고 요청하면 더 정확한 결과물을 얻을 수 있습니다.
