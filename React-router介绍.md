React构建单页面应用，就会设计界面的跳转，一般都会用到路由

React一般使用react-router-dom这个包来实现

```js
npm install react-router-dom --save
```



#### 路由的两种方式

- **hash**：通过监控#后面的路径标识符变化来触发浏览器的hashchange函数，通过location.hash可以知道当前路径标识符，从而实现跳转
- **history：**使用HTML5的history API来实现
  - history.go(n)
  - history.back()
  - History.pushState(data, title,url)
  - History.replaceState(data, title,url)
  - popState：浏览器活动的历史记录发生变化就好触发popState事件



### react-router-dom提供的一些API

- #### hashRouter（在路径上添加/#/，不美观）

  - hashRouter使用url的哈希部分（window.location.hash）来保持页面UI和URL同步
  - location不支持key和state，通过state传递参数时，因为hashRouter没有使用HTML5的historyAPI，无法从历史记录中获取key和state值，所有刷新路由后state值会丢失导致界面显示异常

- #### BrowersRouter（推荐使用）

- #### switch

  - switch包裹Route，不能包裹其它元素，用来控制只显示一个路由

    ```js
    import React from 'react';
    import {Route, Switch} from 'react-router-dom';
    import Role from './role';
    import Menu from './Menu';
    import QuickAccess from './QuickAccess';
    
    class SwitchCom extends Component {
      render() {
        const data = [{    //表示子路由
                path: '/role',
                component: Role
            }, {
                path: '/menu',
                component: Menu
            }]
        return (
          <div className="rightDiv">
              <Switch>
              {/**默认选中快速访问界面 */}
                  <Route exact path="/home" component={QuickAccess}>
                    {
                      data.map(e => {
                        return (
                        <Route key={e.path} path={e.path} component={e.component}></Route>
        )})
                		}
                </Route>
          </Switch>
        </div>
        )
      }
    }
    ```

    

- #### Route

  - 控制路径对应显示的组件。通常使用exact、path以及component

    ```js
    <Route exact path='/' component={Home} />
      
    exact: 控制匹配到/路径时不会继续向下匹配
    path：标识路由的路径
    component：表示路径对应显示的组件
    ```

    

- #### 路由跳转

  - ##### Link

    ```js
    /** 
    * 主要API：to ，to可以接受string或者object，来控制url
    */
    <link to='/course'>
    <link to={
      pathname: '/courses',
      search: '?sort=name',
      hash: '#the-hash',
      state: {fromDashboard: true}
    }>
    ```

    

  - ##### NavLink：可以对点击链接设置样式

- #### 路由跳转传递参数

  - ##### url传参数

    ```js
    <Route exact path=`/detail/:${id}` component={Detail} />
      
    Detail组件可以通过this.props.match.params来获取参数
    ```

    

  - ##### 函数跳转传参数

    ```js
    /**
    * 在Home组件通过点击button跳转到Detail组件
    * 在Detail组件中通过this.props.location来获取参数
    */
    
    import React from 'react';
    
    class Home extends React.Component {
      constructor(props) {
        super(props);
        this.buttonClick = this.bottonClick.bind(this);
      }
      
      render() {
        return <button onClick={this.buttonClick}>通过函数跳转传参</button>
      }
      
      buttonClick() {
        this.props.history.push({
          pathname: '/detail',
          state: {
            id: 3
          },
          //自定义参数
          queryname: {
            msg: '可以自定义参数传递'
          }
        })
      }
    }
    
    class Detail extends React.Component {
      constructor(props) {
        super(props);
      }
      
      componentDidMount() {
        console.log(this.props.location)
      }
    }
    ```

    

  - ##### state传参数

  - ##### 浏览器缓存或者状态管理器

- #### withRouter

  - 路由组件可以直接获取history、location、match等属性，非路由组件必须通过withRouter装饰后才能拥有这些属性
  - 用于包裹非路由组件，使其可以使用this.props.history.push()，来实现跳转