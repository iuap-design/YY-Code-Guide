# 代码规范（华新项目）

## 约定（原则）


1. 默认使用的 ES6 语法，[ES6语法参考](http://es6.ruanyifeng.com/)；
2. 默认使用 jsx 语法定义 React 组件；
3. 默认采用 Less 编写 CSS 样式。

## 1、命名规范

* 文件夹命名：
	* 业务目录（业务目录的定义和划分，需要说明）：所有文件夹除组件文件夹外所有命名均为：全部采用小写方式， 以中划线分隔，如 `my-project-name`
	* 组件目录：采用大驼峰，每个英文单字首字母大写如 `AccountModal`
* 组件名称命名：采用大驼峰，每个英文单字首字母大写如 `AccountModal`
* 文件后缀命名：
   ① 文件js模块统一使用 `.js` 后缀名
   ② 样式文件统一采用 `.less` 后缀名
* 组件目录下的文件命名：组件文件默认命名为 `index.js`，组件样式文件默认命名为 `index.less`
* `props` 和 `state` 使用小驼峰命名

## 2、注释规范

* 单行注释使用 `//` 进行单行注释

在评论对象的上面进行单行注释，注释前放一个空行.不同注释代码间需要进行隔行

	// bad
	var active = true;  // is current tab
	
	// good
	// is current tab
	var active = true;
	
	// bad
	function getType() {
	  console.log('fetching type...');
	  // set the default type to 'no type'
	  var type = this._type || 'no type';
	
	  return type;
	}
	
	// good
	function getType() {
	  console.log('fetching type...');
	
	  // set the default type to 'no type'
	  var type = this._type || 'no type';
	
	  return type;
	}

* 函数注释采用 `/** ... */ `

包括描述，指定类型以及参数值和返回值

```
// bad

// make() returns a new element
// based on the passed in tag name
//
// @param <String> tag
// @return <Element> element
function make(tag) {

  // ...stuff...

  return element;
}

// good
/**
   * Book类，代表一个书本.
   * @constructor
   * @description
   * @param {string} title - 书本的标题.
   * @param {string} author - 书本的作者.
   * @returns {string|*}
   */
function make(tag) {
    // ...stuff...
    return element;
}
```


* JSX 注释采用 `{/* ... */ }`



## 4、组件单一原则
   
一般地，一个文件只暴露一个组件，一个文件不允许超过 500 行代码。 
遵循单一原则可以让我们的组件逻辑更简单，职责更明确，复用性更好。 

```
//bad
class Panel extends Component{
    render() {
	return (
	    <div className="u-panel">
	       <div className="u-panel-header">

	       </div>
	       <div className="u-panel-body">

	       </div>
	       <div className="u-panel-footer">

	       </div>
	    </div>
	)
    }
}

//good
function PanelHeader(props) {
    return (
    <div className="u-panel-header">

    </div>
    )
}

function PanelBody(props) {
    return (
    <div className="u-panel-body">

    </div>
    )
}

function PanelHFooter(props) {
    return (
    <div className="u-panel-footer">

    </div>
    )
}

class Panel extends Component{
    render() {
	return (
	    <div className="u-panel">
	       <PanelHeader />
	       <PanelBody />
	       <PanelHFooter />
	    </div>
	)
    }
}
```

## 5、组件标签闭合、属性换行规范

① 无内容标签自闭合

```
//bad
<Button></Button>
<span></span>

//good
<Button />
<span />
```

② 属性换行：一行超过三个属性则将属性换行


```
//bad
 <Button color="primary" onClick={this.handleClick}> 提交 </Button>

//good
 <Button
    color="primary"
    onClick={this.handleClick}>
 提交
 </Button>

```


## 6、组件声明


- 无状态函数组件

```
//bad
class Button extends React.Component{
    render() {
	return (
	    <Button>{ this.props.text }</Button>
	)
    }
}

//good
const Button = ({ text }) => (
    <button>{ text }</button>
 )

//good
function Button ({ text }) {
    return (
	<button>{ text }</button>
    )
}
```

- 通过 React.Component 定义组件

```
// good
class Button extends React.Component {
  // ...
  render() {
    return <button>{this.state.hello}</button>;
  }

}
```

## 7、使用 ref 来获取组件 DOM


- 通过 `ref` 获取组件原生 `DOM` 对象。
- 尽量不采用传入字符串的方式赋值 `ref`，需采用传入函数的方式来定义 `ref`。

```
//bad
class Button extends React.Component{
    constructor(props){
	    super(props);
    }
    componentDidMount() {
	this.refs.buttonRef.focus();
    }

    render() {
	return (
	    <button
		ref="buttonRef">
	    { this.props.text }
	    </button>
	)
    }
}

//good
class Button extends React.Component{
    constructor(props){
	super(props);
	this.buttonRef = {};
    }
    componentDidMount() {
	this.buttonRef.focus();
    }

    render() {
	return (
	    <button
		ref={(el) => this.buttonRef = el;}>
	    { this.props.text }
	    </button>
	)
    }
}
```

	
	
	
## 8、使用 propTypes 校验组件接口类型

// TODO, 增加 prop-types 类型链接

```
import PropTypes from 'prop-types';

const propTypes = {
    disabled: PropTypes.bool
}

class Button extends React.Component{}

Button.propTypes = propTypes;
```



## 9、组件生命周期相关方法书写顺序
   
- constructor
- componentWillMount
- componentDidMount
- componentWillReceiveProps
- shouldComponentUpdate
- componentWillUpdate
- componentDidUpdate
- componentWillUnmount


```
class Button extends React.Component{

    constructor(props){
	super(props);
	this.state = {
	    data: ''
	}
    }

    componentDidMount() {
	axios.get('http://baidu.com/button-name')
	    .then((res) => {
		this.setState({
		    data：res.data
		})
	    })
    }

    render() {
	return (
	    <Button>
	    { this.state.data }
	    </Button>
	)
    }
}
```

## 10、默认采用箭头函数定义组件内的公共方法

```
//bad
class Button extends React.Component{
    handleClick(e) {

    }
    render() {
	return (
	    <Button
		onClick={this.handleClick.bind(this)}>
	    { this.state.data }
	    </Button>
	)
    }
}


//good
class Button extends React.Component{
    handleClick = (e) => {

    }
    render() {
	return (
	    <Button
		onClick={this.handleClick}>
	    { this.state.data }
	    </Button>
	)
    }
}
```

## 11、采用 `setState` 修改 `state`，不允许出现类似 `this.state.xx = xx；` 的代码

   
```
//bad
class Button extends React.Component{
    constructor(props){
       super(props);
       this.state = {
	    disabled: false
       }
    }
    handleClick = () => {
	this.state.disabled = true;
	this.setState({
	   disabled:  this.state.disabled
	})

    }

    render() {
	return (
	    <Button
		disabled={this.state.disabled}>
	    { this.props.text }
	    </Button>
	)
    }
}

//good
class Button extends React.Component{
    constructor(props){
       super(props);
       this.state = {
	    disabled: false
       }
    }
    handleClick = () => {
	let disabled = ture;
	this.setState({
	   disabled
	})

    }

    render() {
	return (
	    <Button
		disabled={this.state.disabled}>
	    { this.props.text }
	    </Button>
	)
    }
}
```


## 12、资源引入顺序

```

//组件 （1）
//①react组件   ② UI级组件
import React, {Component} from 'react';
import { Button, Message, Modal, Loading, getMarginStyle } from 'tinper-bee';
import Grid from 'bee-complex-grid';
import CommonModal from '../CommonModal';
import DeleteModal from "../DeleteModal";

// 导入工具类（2）
import {connect, actions} from 'mirrorx';
import {deepClone, success, Error} from 'utils';

// 导入样式 （3）
import 'bee-complex-grid/build/Grid.css';
import 'bee-pagination/build/Pagination.css'
import './index.less';
```

## 13、【不强制执行】代码通透性

- `=` 左右各保持一个空格；
- `,` 后面保持一个空格；
- `{}` 花括号体内左右两边各保持一个空格

## 最佳实践：标准组件定义

```
//引入依赖
import React from 'react';
import ReactDOM from'react-dom';
import PropTypes from 'prop-types';

//定义prop检验
const propTypes = {
//每一个props都要写注释
}

//定义默认参数
const defaultProps = {

}

/**
 * 定义组件
 */
class Button extends React.Component {
	constructor (props) {
		super(props);
		//定义state
		this.state = {
	//每一个state要写注释
		}
	}
    //组件生命周期方法

    //自定义函数方法，及注释
     myEvent () {

     }



	render () {
		return (
			 <div
			    onClick={this.MyEvent}>
			    some text
			 </div>
		)
	}
}

Button.propTypes = propTypes;
Button.defaultProps = defaultProps;

export default Button;

```

