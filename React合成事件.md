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

    

### React合成事件和原生事件的区别

```javascript
//原生事件是将事件直接绑定到DOM节点上
let dom = document.getElementById('id');
dom.addEventListener('click', function(e) {
  console.log(e.target, e.currentTarget)
})

/**
* React合成事件（避免DOM事件滥用，同时避免底层不同浏览器之间的事件系统差异）
* React并不是将事件直接绑定在dom上，而是采用事件冒泡的形式冒泡到document上，document处监听所有支持的事件
onClick、onChange等
*/

/**禁止事件冒泡*/
e.stopPropagation()
window.event.cancelBubble = true;

/**禁止默认事件*/
e.preventDefault()
window.envent.returnValue = false;
```