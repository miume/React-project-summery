#### React事件机制

- 事件注册
- 事件分发



#### 合成事件SyntheticEvent

- SyntheticEvent实例将被传递给你的事件处理函数，它是浏览器的原生事件的跨浏览器包装器。除兼容所有浏览器外，它还拥有和浏览器原生事件相同的接口
- 每个SyntheticEvent对象包含
  - bubbles 
  - cancelable
  - currentTarget
  - defaultPrevented
  - eventPhase
  - isTrusted
  - nativeEvent
  - void preventDefault()
  - isDefaultPrevented
  - void stopPropagation()
  - isPropagationStopped()
  - target
  - timeStamp
  - type : 事件类型