# 학습 키워드

- Bundler(번들러)
  - Parcel
- Lint(린트)
  - ESLint

## ✔️ 키워드 정리

### Parcel

특별한 설정 없이 바로 사용 가능한 빌드 도구. 내부적으로 SWC를 사용해 기존 도구보다 빠르다<br/>

`package.json` 파일에 설정 추가

```Json
"source": "./index.html",
```

```Json
// parcel-reporter-static-files-copy 패키지 설치 후 .parcelrc 파일 작성
// 이렇게 하면 static 폴더의 파일을 정적 파일로 Serving할 수 있다(이미지 등 Assets).
{
  "extends": ["@parcel/config-default"],
  "reporters":  ["...", "parcel-reporter-static-files-copy"]
}
```

빌드 및 정적 서버 실행

```Bash
npx parcel build
npx servor ./dist
```

### ESLint
사용하는 이유
- 스타일 통일
- 잠재적 문제 발견
- 베스트 프랙티스 추천 → 최신 트렌드를 학습하는데 활용할 수 있다.

```Json
{
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    }
}
```
`.vscode/settings.json` 파일에 해당 내용을 추가하면 저장할 때마다 ESLint를 실행한다.