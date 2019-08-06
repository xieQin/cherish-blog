---
title: 使用React Hooks进行状态管理
date: 2019-03-24 15:59:42
tags: React
categories: React
---
## 总体方案

定义Model
```ts
type stateType = {
  text: string
}
type actionsType = {
  modify: any
}

const TestModel: ModelType<stateType, actionsType> = {
  state: {
    text: 'hello world'
  },
  actions: {
    modify (state, actions, text: string) {
      return state => {
        state.text = text
      }
    },
  }
}

export default TestModel
```

```ts
import { Model } from "react-model";
import Test from "./test";

export const { useStore, getState } = Model({ Test });
```

### 实际应用

- 依赖：react-model

- 使用示例
```tsx
import { useStore } from '../models'

const Example = () => {
  const [state, actions] = useStore('Test')
  return (
    <div onClick={() => actions.modify('hello')}>{state.text}</div>
  )
}
```

- 项目示例
[react-state-hooks](https://github.com/xieQin/react-state-hooks)
