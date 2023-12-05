# 학습 키워드

- styled-componets

## ✔️ 키워드 정리

### styled-componets

styled-components를 설치하는 명령어이다.

```Bash
$ npm i styled-components
```

```Javascript
import styled from 'styled-components';

const StyledTitle = styled.span`
  font-family: 'yg-jalnan';
  font-size: 110px;
  line-height: 140px;
  color: ${(props) => props.theme.colors.text};
`;

export default function App(){
  return(
    <div>
      <StyledTitle>
        제목
      </StyledTitle>
    </div>
  )
}
```

이런식으로 사용하면 된다. props나 attrs도 정의해서 사용할 수 있다.