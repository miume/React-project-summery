- antd是基于Ant Design设计体系的React UI组件库，主要用于研发企业级中后台产品

- 安装

  ```js
  npm install antd --save
  ```

- 按需加载

  ```js
  npm install babel-plugin-import
  
  {
    "plugins": [
      ["import", {
        "libraryName": "antd"，
        "libraryDirectory": "es",
        "style": "css"
      }]
    ]
  }
  
  //按照以下方式按需引入
  import {DatePicker, Table} from 'antd';
  ```

  