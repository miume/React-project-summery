#### state状态、props属性

- ##### state，组件的内部状态，管理组件的状态，是**可变的**，是一组用于反映组件UI变化的状态集合

  - ###### 在组件中通过**this.state**来访问组件state中的数据

  - ###### 在组件中通过**this.setState()**来更新组件state中的数据

  - ###### state允许React组件随用户操作、网络响应或者其它变化而动态的更改输出内容

  ```js
  /**注意事项
  * 1、不要直接修改state (this.state.name = 'new name'  ❌)
       使用this.setState({name: new name})来更新数据
  * 2、state的更新可能是异步的
  */
  ```

  

- ##### props：父组件通过props将数据传给子组件，具有不可变性

  - ###### 在父组件中定义state，在自组件中可以通过this.props属性来访问父组件传递的数据

  - ###### React是单向数据流，数据只能一层一层往下传递，不能越级传递数据。

  - ###### 子组件若需要向父组件传递数据，需要使用回调函数的方法（在自组件中调用父组件的方法）

```js
import React from 'react';

class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: '',
      data: []
    }
  }
  
  render() {
    return (
    	<div><span>名字为：</span>{${this.state.name}}</div>
    )
  }
}
```



#### state和props引申

- 无状态组件（展示组件）

  - **无state状态**
  - 主要用于定义模版，接收来自父组件的props属性来接收传递过来的数据

  ```js
  /**
   1、函数
   2、只接收一个props形参，直接使用props，而不是this.props
   3、没有生命周期函数
  */
  let uselessTemplate = function(props) {
    return (
    	<div>{`${props.name}-${props.age}`}</div>
    )
  }
  ```

  

- 有状态组件（容器组件）

  - **有state状态**

  - 主要用来定义交互逻辑和业务逻辑

  ```js
  /**
   1、继承自Component类
   2、可以使用state和props，并且都通过this.state和this.props来调用
   3、拥有生命周期函数
  */
  
  import React from 'react';
  
  class Example extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        name: '',
        data: []
      }
    }
    
    render() {
      return (
      	<div><span>名字为：</span>{${this.state.name}}</div>
      )
    }
  }
  ```

  

