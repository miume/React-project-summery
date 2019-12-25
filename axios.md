## axios

- axios是一个基于promise的HTTP库，可以用在浏览器和node.js中

- 特点

  - 从浏览器创建XMLHttpRequests
  - 从nodejs中创建http请求
  - 支持PromiseAPI
  - 拦截请求和响应
  - 转换请求数据和响应数据
  - 取消请求
  - 自动转换JSON格式
  - 客户端支持防御XSRF 

  ```js
  //1、安装
  npm install axios
  
  //2、使用
  import axios from 'axios'；
  
  function urlRequest() {
    axios({
      url: '请求接口',
      method: 'get'/'post'/'put'/'post'/'DELETE'，
      headers: {
      	'Authorization': '认证信息'
    	},
      data,  //json格式数据
      params //拼接在接口后面的参数
    }).then((data) => {
      
    }).catch(error => {
      
    })
  }
  ```

  

- XSRF/CSRF（跨站请求伪造cross-site request forgery）

  - 挟持用户在当前登陆已登陆的web应用程序上执行非本意的操作的攻击方法
  - XSS利用的是用户对指定网站的信任，CSRF利用的是网站对用户网页浏览器的信任。
  - 跨站请求攻击：
    - 攻击者通过一些技术手段欺骗用户浏览器去访问曾经认证的网址并执行一些操作
    - **web用户身份验证的漏洞**：简单的身份认证只能保证请求来自某个用户的浏览器，却不能保证请求本身是由用户自愿发出的
  - 攻击者并不能通过CSRF攻击来获取用户账号的直接控制权，也不能直接获取用户的信息。只能欺骗用户浏览器去执行一些操作。
  - **防御措施**：
    - 检查Referer字段
      - http头部有一个Referer字段，表明请求来源于哪个地址；通常来说，在请求敏感数据时，Referer字段应该和请求的地址处于同一域名下；但是对于CSRF恶意攻击，Referer字段是包含恶意网站的地址，与请求放入地址不属于同一域名下。
    - 添加校验token
      - 在情趣敏感数据时，要求用户浏览器提供不保存在cookir中，并且攻击者无法伪造的数据作为校验。

  参考地址

  [https://zh.wikipedia.org/wiki/跨站请求伪造](CSRF参考地址)

  

