## React

- 项目用的react版本是16.5.5
- 现在React版本已更新到16.11.0



####React16.3版本前的生命周期函数

- ##### 初始化

  - getDefaultProps：

- ##### 挂载阶段

  - componentWillMount：**不常用**，在整个生命周期中只调用一次
  - render：创建虚拟DOM，进行DIff算法
  - componentDidMount：**常用**，常在此生命周期函数调用接口，异步更新state，只调用一次

- ##### 更新阶段

  - 父组件更新props值时触发
    - componentWillReceiveProps(nextProps) ：常用于监控父组件props的变化
  - 自身组件state更新以及父组件更新props值时触发
    - shouldComponentUpdate(nextProps,nextState) ：常用于性能优化，减少重新渲染次数
    - componentWillUpdate()：**不常用**
    - render：更新DOM树
    - componentDidUpdate(preProps,preState)：**不常用**

- ##### 卸载阶段

  - componentWillUnmount

    ```js
    /**卸载组件
    * 一些事件监听和定时器需在此时清除
    */
    componentWillUnmount() {
      this.setState(() => {
        return;
      })
    }
    ```

    

- #### 父组件重新render

```js
//优化性能，减少渲染
shouldComponentUpdate(nextProps,nextState) {
	if(nextProps === this.props) {
    return false
  }
}

//在componentWillRecieveProps方法中，将props转换成自己的state
//只调用于props引起的组件更新过程，参数nextProps是父组件传给当前组件的新props
componentWillRecieveProps(nextProps) {
  this.setState({
    something: nextProps.something
  })
}


```

- 组件本身调用setState，无论state有没有变化。可通过shouldComponentUpdate来优化

```js
shouldComponentUpdate(nextStates) {
  if(nextStates.something === this.state.somethings) {
    return false
  }
}
```



#### React16.3之后版本的最新生命周期

![img](/Users/yangmei/Desktop/React总结/img/lifeCircle.png)

- compontDidCatch(error) : 捕捉错误

- getDerivedStateFromProps（渲染render前调用）（**移除componentWillReceiveProps**）

  ```js
  /**更新由props决定的state及处理特定情况下的回调*/
  
  //老版本
  componentWillReceiveProps(nextProps) {
    if(nextProps.siLogin !== this.props.isLogin) {
      this.setState({
        isLogin: nextProps.isLogin
      });
      if(nextProps.isLogin) {
        this.handleColse();
      }
    }
  }
  
  //新版本 
  //getDerivedStateFromProps 禁止组件去访问this.props,强制让开发者去比较nextProps与prevState中的值，
  //（根据当前的props来更新组件的state，而不去去做其他一些让组件自身状态变得不可预测的事情）
  static getDerivedStateFromProps(nextProps, preState) {
    if(nextProps.isLogin !== preState.isLogin) {
      return {
        isLogin: nextProps.isLogin
      };
    }
    return null;
  }
  
  //新版本使用componentDidUpdate生命周期来处理- 根据父组件props更新来触发回调函数
  componentDidUpdate(prevProps,prevState) {
    if(!prevState.isLogin && this.props.isLogin) {
      this.handleClose();
    }
  }
  ```

  

  ```js
  /**
  * getDerivedStateFromProps替代以前的componentWillReceiveProps
  *为了防止在render渲染之前滥用生命周期函数，弃用了三个生命周期函数
  componentWillReceiveProps、componentWillMount、componentWillUpdate
  */
  //静态函数，函数体内不鞥访问this（纯函数，输出）
  static getDerivedStateFromProps(nextProps,preState) {
    //根据nextProps和preState计算出预期的状态改变，返回结果会被发送给setState
  }
  ```



- getSnapshotBeforeUpdate（渲染render后调用）

  - 在getSnapshotBeforeUpdate中读到的DOM元素状态是可以保证与componentDidUpdate保持一致的
  - getSnapshotBeforeUpdate返回一个值，这个值被传入到componentDIdUpdate中，在componentDidUpdate中去更新组件的状态

  ```js
  /**
  * 执行之时DOM元素还没有被更新，给一个机会获取DOM信息，计算一个snapshot
  */
  //不建议使用，哈哈
  getSnapshotBeforeUpdate(preProps,preState) {
    return 'foo'
  }
  
  //参数snapshot是getSnapshotBeforeUpdate返回的值
  componentDidUpdate(preProps,preState,snapshot) {
    
  }
  ```

- #### 生命周期更新总结

  - 将现有的componentWillUpdate中的回调函数迁移至**componentDidUpdate**中
  - 如果触发某些回调函数时需要用到DOM元素的状态，则将对比或计算的过程迁移至**ge tSnapshotBeforeUpdate**，然后在**componentDidUpdate**中统一触发回调或更新状态



参考链接：[https://juejin.im/post/5ae6cd96f265da0b9c106931](参考链接)

