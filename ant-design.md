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



## 问题总结

### 2019-10-18

- ##### 问题：当有多个Select组件时，怎么统一监听其变化

  ```js
  import React from 'react';
  import {Select} from 'antd';
  
  const {Option} = Select;
  
  class SelectCom extends React.Component {
  construcotr(props) {
    super(props);
    this.state = {
      select1: undefined,
      select2: undefined,
      select3: undefined
    }
    this.selectChange = this.selectChange.bind(this);
  }
  render() {
    return (
      <div>
        <Select value={select1} onChange={this.selectChange} placeholder='请选择' style={{width:100}}>
          <Option name={'select1'}>1</Option>
          <Option name={'select1'}>2</Option>
          <Option name={'select1'}>3</Option>
        </Select>
        <Select value={select2} onChange={this.selectChange} placeholder='请选择' style={{width:100}}>
          <Option name={'select2'}>1</Option>
          <Option name={'select2'}>2</Option>
        </Select>
        <Select value={select3} onChange={this.selectChange} placeholder='请选择' style={{width:100}}>
          <Option name={'select3'}>1</Option>
          <Option name={'select3'}>2</Option>
         </Select>
  		</div>
    )
  }
  }
  
  /**监控下拉框变化
  * value是选中option对应的value值
  * option 是选中的Option实例对象
  */
  selectChange (value, option) {
    let name = option.props.name;
    this.setState({
      [name]: value 
    })
  }
  
  export default SelectCom;
  ```

- ##### 当多个Input组件时，怎么统一监控其变化

  ```js
  import React from 'react';
  import {Input} from 'antd';
  
  class InputCom extends React.Component {
  construcotr(props) {
    super(props);
    this.state = {
      item1: undefined,
      item2: undefined,
      item3: undefined
    }
    this.onInputChange = this.onInputChange.bind(this);
  }
  render() {
    let {item1,item2,item3} = this.state;
    return (
      <Input placeholder='请输入..' name='item1' 
                   onChange={this.inputChange} value={item1}/>
      <Input placeholder='请输入..' name='item2' 
                   onChange={this.inputChange} value={item2}/>
      <Input placeholder='请输入..' name='item3' 
                       onChange={this.inputChange} value={item3}/>
    )
  }
  }
  
  /**分别监控保养项目、保养内容、频率输入内容的变化*/
  inputChange(e) {
    let name=e.target.name; value=e.target.value;
    this.setState({
      [name] : value
    })
  }
  
  export default InputCom;
  ```



### 2019-10-22

- #### 问题：前端怎么调取后端接口，下载表格？

  ```js
  import React from 'react';
  import {Button} from 'antd';
  import axios from 'axios';
  
  class InputCom extends React.Component {
    construcotr(props) {
      super(props);
      this.state = {
      }
      this.export = this.export.bind(this);
    }
    render() {
      return (
        <Button onClick={this.export}>导出</Button>
      )
    }
  }
  
  /**后端逻辑是先根据查询参数返回excel文件位置，确定获取excel表格的接口，前端在创建一个a标签，
  *将a.href = url a.click()触发
  */
  export() {
    axios({
              url: `${this.url.equipmentRepair.export}`,
              method: 'get',
              headers: {
                  'Authorization': this.url.Authorization
              },
              params: params,  //导出需要传递的参数
          }).then((data) => {
      				//data.data.data表示导出接口的返回参数（表格在后端的存储地址）
              let url = `${url}${data.data.data}`; //url表示接口统一前缀，
              let a = document.createElement('a');
              a.href = url;
              a.click();
              message.info(data.data.message)
          })
  }
  
  export default InputCom;
  ```



### 2019- 10-28

- 获取当前时间

  ```js
  let date = new Date();
  date.toLocaleDateString();  //2018/10/28
  date.getFullYear();  //2018
  date.getMonth();   //9 代表（9+1=10月）
  date.getDate();    //28
  date.getDay();     //1 - 代表星期一
  date.getTime();   //获取当前时间（从1970.1.1开始的毫秒数）
  date.getHours();  //获取当前小时数（0-23）
  date.getMinutes();
  date.getSeconds();
  date.getMillseconds();
  ```

- moment：一个javaScript日期处理库 http://momentjs.cn/（文档地址）

  ```js
  //1、安装
  npm install moment --save
  
  //2、用法
  
  //日期格式化
  moment(new Date()).formate('YYYY-MM-DD hh:mm:ss'); //2019-10-25 20:31:23
  moment(new Date()).format('dddd');   //星期三
  
  //相对时间
  moment('20111103','YYYYMMDD').fromNow(); //8年前
  moment().startOf('day').fromNow();   //20小时前
  moment().endOf('day').fromNow();   //4个小时内
  moment().startOf('hour').fromNow();  //29分钟前
  
  //多语言支持
  moment.locale();  //zh-cn
  ```



### 2019-10-33

#### css书写顺序

- 位置属性（position、top、right、z-index、flex、float等）

- 大小（width、height、padding、margin）

- 文字类型（font、line-height、letter-spacing）

- 背景（background、border）

- 其它（animation、transition）

  

### 2019-12-14

- **Upload上传**（文件选择上传和拖拽上传控件）

  - 自动上传

    ```js
    import React from 'react';
    import axios from 'axios';
    import {Upload,message,Button,Icon} from 'antd';
    
    class UploadFile extends React.Component {
      constructor(props) {
        super(props);
        this.state = {
          fileList: []
        }
      }
      
      render() {
        let {fileList} = this.state;
        const props = {
          name: 'file',
          action: '上传文件后端指定url',
          headers: {
            authorization: 'authorization-text'
          },
          onChange: this.onChange.bind(this),
          beforeUpload: this.beforeUpload.bind(this),
          fileList
        }
        return (
          <Upload {...props}>
          	<Button>
          		<Icon type='upload'>上传文件</Icon>
          	</Button>
          </Upload>
        )
      }
      
      onChange(info) {
        if (info.file.status !== 'uploading') {
          console.log(info.file, info.fileList);
        }
        if (info.file.status === 'done') {
          message.success(`${info.file.name} file uploaded successfully`);
        } else if (info.file.status === 'error') {
          message.error(`${info.file.name} file upload failed.`);
        }
      }
      }if (info.file.status !== 'uploading') {
          console.log(info.file, info.fileList);
        }
        if (info.file.status === 'done') {
          message.success(`${info.file.name} file uploaded successfully`);
        } else if (info.file.status === 'error') {
          message.error(`${info.file.name} file upload failed.`);
        }
      }
    
      /**上传文件之前的钩子，参数为上传的文件，若返回false则停止上传*/
    	beforeUpload(file) {
        let {name} = file;
        this.setState({
          fileList: [file]  //让最新的文件覆盖旧文件，保证每次只显示最新上传文件
        })
        if(name.slice(-3) === 'xls' || name.slice(-4) === 'xlsx') {
          return true
        } else {
          return false
        }
      }
    }
    
    export default UploadFile;
    ```

    

  - 手动上传（需求：每次只上传一个.xls / .xlsl文件，手动上传）

    ```js
    import React from 'react';
    import {Upload,message,Button,Icon} from 'antd';
    
    class UploadFile extends React.Component {
      constructor(props) {
        super(props);
        this.state = {
          fileList: [],
          uploading: false
        }
        
        this.uploadData = this.uploadData.bind(this);
      }
      
      render() {
        let {fileList} = this.state;
        const props = {
          beforeUpload: this.beforeUpload.bind(this),
          onRemove: this.onRemove.bind(this),
          fileList
        }
        return (
          <div>
            <Upload {...props}>
              <Button>
                <Icon type='upload'>上传文件</Icon>
              </Button>
            </Upload>
    				<Button type='primary' 
    							onClick={this.handleUpload.bind(this)} disabled={fileList.length === 0}
    							loading={uploading}
              		style={{ marginTop: 16 }}></Button>
    			</div>
        )
      }
      
      handleUpload() {
        let {fileList} = this.state;
        if(!fileList.length) {
          message.error('请先上传一个.xls或者.xlsx文件，在导入！');
          return false
        }
        let {name} = fileList[0];
        if(name.slice(-3) !== 'xls' || name.slice(-4) !== 'xlsx') {
          message.error('上传文件只能是.xls或者.xlsx文件，请重新上传！')
          return false
        } 
        
        //处理数据
        let formData = new formData();
        formData.append({
          'excel': fileList[0]   //注意⚠️⚠️：excel这个键名需要根据后端传递参数格式进行调整
        });
        
        this.uploadData(formData)
      }
    
    	uploadData(formData) {
        this.setState({
            upLoading: true
          })
        axios({
          url: `后端指定上传接口`,
          method: 'post',
          data: formData
        }).then((data) => {
          message.info(data.data.message)；
          this.setState({
            fileList: [],
            upLoading: false
          })
        }).catch((error) => {
          message.info(error)；
          this.setState({
            fileList: [],
            upLoading: false
          })
        })
      }
    
      /**上传文件之前的钩子，参数为上传的文件，若返回false则停止上传*/
    	beforeUpload(file) {
        let {name} = file;
        this.setState({
          fileList: [file]  //让最新的文件覆盖旧文件，保证每次只显示最新上传文件
        })
        return false  //beforeUpload一直返回false，可以实现手动上传
      }
    }
    
    /**点击移除文件时的回调函数，返回false则不移除*/
    onRemove() {
      this.setState({
        fileList: []   //因为需求是只能上传一个文件，则移除文件就是清空fileList
      })
      return true
    }
    
    export default UploadFile;
    ```

    

### css3中 vw、vh、calc

- vh：相当于视窗的高度，视窗被均分为100单位

- vw：相当于视窗的宽度，视窗宽度被均分为100单位

- vmin：相对易视窗的宽度或高度较小的那个；其中较小的那个被均分为100单位的vmin

- vmax：

- 视窗：浏览器内部的可视区域大小

  ```javascript
  window.innerWidth/window.innerHeight
  ```

- Calc：用来指定元素的长度

  ```css
  width: calc(100vw - 10px);
  ```



### 2019-12-15

- 问题：当实现表格新增多条数据，导致每条数据都一摸一样，同时变化

  ```js
  import React from 'react';
  import {Table,Input} from 'antd';
  
  class TheTable extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        data: []
      }
      this.inputChange = this.inputChange.bind(this);
      this.columns = [{
        title: '序号',
        dataIndex: 'index',
        key: 'index'
      },{
        title: '名字',
        dataIndex: 'name',
        key: 'name',
        render: (text) => {
          return <Input name={'name'} value={text} onChange={this.inputChange} style={{width:'100%'}}/>
        }
      },{
        title: '年龄',
        dataIndex: 'age',
        key: 'age',
        render: (text) => {
          return <Input name={'age'} value={text} onChange={this.inputChange} style={{width:'100%'}}/>
        }
      }]
    }
    
    render() {
      let {data} = this.state;
      return (
        <div>
          <Button onClick={this.handleAdd.bind(this)}>新增</Button>
          <Table dataSource={data} paginatin={false} size={'small'} bordered 
                 rowKey={record=>record.code} columns=this.columns/>
        </div>
      )
    }
    
    /**简化流程后的问题*/
    componentDidMount() {
      this.setState({
        item: {
          index: '',
          name: '',
          age: ''
        }
      })
    }
    
    /**问题分析
    * 对象属于引用数据类型
    */
    handleAdd() {  //这种做法会导致data每一条数据都和最后新增一条数据一样，
      let {item,data} = this.state,index = data.length + 1;
      item['index'] = index;
      data.push(item);
      this.setState({data});  
    }
  }
  
  /**解决方案一*/
   handleAdd1() {  //这种做法会导致data每一条数据都和最后新增一条数据一样，
      let {item,data} = this.state,index = data.length + 1;
      item['index'] = index;
      data.push(JSON.parse(JSON.stringify(item)));  //深拷贝
      this.setState({data});  
    }
  }
  
  
  /**解决方案二*/
   handleAdd2() {  //这种做法会导致data每一条数据都和最后新增一条数据一样，
      let {data} = this.state,index = data.length + 1,
          item = {
            index: index,
            name: '',
            age: ''
          }
      data.push(item);  //深拷贝
      this.setState({data});  
    }
  }
  ```

  

### 2020-03-01

- #### 多选框的使用

  ```js
  import React from 'react';
  import {Checkbox} from 'antd';
  const {CheckboxGroup} = Checkbox.Group;
  
  class Practice extends React.Component() {
    render() {
      return (
        <div>
          <CheckboxGroup options={selectAllItems} value={selectedItems} 
    onChange={this.checkBoxChange}>
      
        </div>
  		)
    }
  }
  
  /**如果选取的数据只有名字
  * data = ['apple','pea','orange','watermelon']
  * 则使用以下形式
  * options：表示所有数据，例如：selectAllItems = ['apple','pea','orange','watermelon']
  * value：表示所选中数据，例如：selectedItems = ['apple']
  * onChange：监控多选框的变化
  */
  <CheckboxGroup options={selectAllItems} value={selectedItems} 
  onChange={this.checkBoxChange}>
    
  /**
  * 如果数据形式为 data = [{id: 1, name: 'A厂'},{id: 2, name: 'B厂'},{id: 1, name: 'C厂'}]
  * 则使用以下形式 
  * span=8：表示每行显示三个checkbox
  */
    <CheckboxGroup style={{width: "100%"}} value = {supplierId} onChange={this.supplierIdChange.bind(this)}>
                          {
                              data.length ? data.map(p =>
                                  <Col key={p.id} span={8}>
                                      <Checkbox value={p.id}>{p.name}</Checkbox>
                                  </Col>):null
                          }
                          </CheckboxGroup>
  ```

  