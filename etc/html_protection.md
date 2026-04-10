# HTML 비밀번호 보호 (StatiCrypt)

## 개요

StatiCrypt를 사용하여 HTML 파일을 AES-256으로 암호화합니다.
JavaScript 비활성화, 소스 보기로도 원본 콘텐츠를 확인할 수 없습니다.

## 사전 요구사항

- Node.js 설치 필요

## 사용법

### 1. 암호화

```bash
npx staticrypt <원본.html> -p "비밀번호" -d <출력폴더> \
  --short --remember 0 \
  --template-title "페이지 제목" \
  --template-instructions "비밀번호를 입력해주세요."
```

**주의:** `-o` 옵션 대신 `-d` 옵션으로 출력 디렉토리를 지정합니다.
암호화된 파일은 `<출력폴더>/<원본파일명>.html`로 생성됩니다.

### 2. 실제 사용 예시

```bash
# 암호화
npx staticrypt mlops-proposal.html -p "alpha5230" -d deploy \
  --short --remember 0 \
  --template-title "Annual Value Proposal 2025" \
  --template-instructions "비밀번호를 입력해주세요."

# deploy 폴더에 index.html로 복사 (Vercel 배포용)
cp deploy/mlops-proposal.html deploy/index.html
```

### 3. Vercel 배포

```bash
cd deploy && npx vercel --yes --prod
```

### 비밀번호 변경

같은 명령어를 새 비밀번호로 다시 실행한 뒤 재배포하면 됩니다.

```bash
# 새 비밀번호로 암호화
npx staticrypt mlops-proposal.html -p "새비밀번호" -d deploy \
  --short --remember 0 \
  --template-title "Annual Value Proposal 2025" \
  --template-instructions "비밀번호를 입력해주세요."

# index.html 덮어쓰기 + 재배포
cp deploy/mlops-proposal.html deploy/index.html
cd deploy && npx vercel --yes --prod
```

## 주요 옵션

| 옵션 | 설명 |
|------|------|
| `-p` | 비밀번호 지정 |
| `-d` | 출력 디렉토리 |
| `-o` | 출력 파일 경로 (단, encrypted/ 폴더로 출력될 수 있음) |
| `--short` | 간결한 비밀번호 입력 UI |
| `--remember 0` | 비밀번호 기억 비활성화 (0 = 매번 입력) |
| `--template-title` | 비밀번호 페이지 제목 |
| `--template-instructions` | 비밀번호 입력 안내 문구 |
| `--compact` | 더 작은 출력 파일 |

## 보안 수준

- AES-256 암호화 (브라우저에서 복호화)
- JS 비활성화/소스 보기로 원본 확인 불가
- 비밀번호 없이는 콘텐츠 복원 불가능
- 링크를 아는 사람도 비밀번호 없이 접근 불가

## 배포 후 삭제

Vercel 대시보드(https://vercel.com)에서 프로젝트를 삭제하면 URL이 비활성화됩니다.
