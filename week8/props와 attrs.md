# 학습 키워드

- props
- attrs

## ✔️ 키워드 정리

### props

props로 active 상태를 받아서 버튼의 배경색을 변경하는 코드이다.

```Javascript
import styled from 'styled-components';
import { useBoolean } from 'usehooks-ts';

type ButtonProps = {
  active: boolean;
}

function background(props: ButtonProps) {
  return props.active ? '#00F' : '#FFF';
}

const Button = styled.button<ButtonProps>`
  color: black;
  background: ${background};

  ${(props) => props.active && css`
    backgound: #F00;
    color: #FFF;
  `}
`;

export default function Switch() {
  const { value: active, toggle } = useBoolean();

  return (
    <section>
      <Button type="button" onClick={toggle} active={active}>Light</Button>
    </section>
  );
}

```

styled-components 에서도 props의 타입을 지정해줄 수 있다는 부분이 신기했다.

### attrs

```Javascript
type ButtonProps = {
  type?: 'button' | 'submit' | 'reset';
  active: boolean;
}

const Button = styled.button.attrs<ButtonProps>((props) => ({
  type: props.type ?? 'button'
}))<ButtonProps>`
background: #fff;
color: #000;
`
```

[arrts](https://styled-components.com/docs/basics#attaching-additional-props)를 사용하면 기본 속성을 추가할 수 있다. 불필요하게 반복되는 속성을 처리할 때 유용한데, 주로 버튼 컴포넌트를 만들 때 자주 사용한다.