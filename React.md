# react组件开发规范

## 文件命名
- 每一个文件只包含一个组件，每一个基本组件只包含单一功能
- 文件js模块统一使用js后缀名

## js规范
- 使用es6开发，尽量使用常用的ES6语法，[ES6语法参考](http://es6.ruanyifeng.com/)
- 使用jsx语法
- [组件设计原则](https://github.com/tinper-bee/react-components-docs/blob/master/%E7%BB%84%E4%BB%B6%E5%88%92%E5%88%86%E5%8E%9F%E5%88%99.md)

### 格式


- 无内容标签自闭合


```
//bad

<Button></Button>
<span></span>

//good
<Button />
<span />
```

- 属性换行
```
//bad
 <Button color="primary" onClick={this.handleClick}> 提交 </Button>
 <Button color="primary" />

//good

 <Button
    color="primary"
    onClick={this.handleClick}>
 提交
 </Button>

<Button
    color="primary"
/>
```

-

### 组件命名

- 组件文件命名使用大驼峰， ComponentDemo
- 带命名空间的组件，如果一个组件包含只有自身使用的子组件，以该组件为命名空间编写组件，例如Table，Table.Head

### 组件声明

- 使用es6的class来声明组件，而不是使用`createClass`,在React V16版本，`createClass`已经废弃

```
// bad
const Button = React.createClass({
  // ...
  render() {
    return <button>{this.state.hello}</button>;
  }
});

// good
class Button extends React.Component {
  // ...
  render() {
    return <button>{this.state.hello}</button>;
  }

```

- 对于不包含`state`和`refs`的组件，建议写成纯函数组件，而且建议使用function关键字声明

```
//bad

class Button extends React.Component{
    render() {
        return (
            <Button>{ this.props.text }</Button>
        )
    }
}

//bad

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

- 对于只有简单数据类型的`props`和`state`的组件，建议使用`PureComponent`来声明组件

`PureComponent`是在组件内默认再`shouldComponentUpdate`方法内进行的`state`和`props`的浅比较。来对组件进行一定的性能优化。

```

//bad

class Button extends React.Component{
    constructor(props){
        super(props);
        this.state = {
            disabled: false
        }
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

class Button extends React.PureComponent{
    constructor(props){
        super(props);
        this.state = {
            disabled: false
        }
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

### 组件内部声明

- 使用propTypes进行props类型校验

```
import PropTypes from 'prop-types';

const propTypes = {
    disabled: PropTypes.bool
}

class Button extends React.Component{}

Button.propTypes = propTypes;

```
- 使用defaultProps定义默认参数

```
import PropTypes from 'prop-types';

const defaultProps = {
    disabled: false
}

class Button extends React.Component{}

Button.defaultProps = defaultProps;

```

### 组件生命周期函数

- 组件生命周期方法定义顺序
    - constructor
    - getChildContext
    - componentWillMount
    - componentDidMount
    - componentWillReceiveProps
    - shouldComponentUpdate
    - componentWillUpdate
    - componentDidUpdate
    - componentWillUnmount

- 在`componentDidMount`生命周期内获取初始数据

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

- 在组件`componentWillUnmount`卸载生命周期中，进行清除定时器、卸载组件绑定的自定义事件等。

```
class Button extends React.Component{
    constructor(props){
        super(props);
        this.state = {
            data: ''
        }
        this.timer = null;
    }
    componentDidMount() {
        this.timer = setInterval(this.getData, 1000);
    }

    getData = () => {
            axios.get('http://baidu.com/button-name')
                .then((res) => {
                    this.setState({
                        data：res.data
                    })
                })
    }

    componentWillUnmount() {
        window.clearInterval(this.timer);
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

- 使用箭头函数定义自定义的组件内方法

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

### 属性定义

- 定义props避开react关键字及保留字，常用的props及state定义可参考下表

- `props`和`state`使用驼峰命名。

- 不直接修改`state`

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

- 自定义HTML属性使用data-

```
class Button extends React.Component{

    render() {
        return (
            <button
                data-name="submit-button">
            { this.props.text }
            </button>
        )
    }
}


```

- 可以使用es6的这种`...props`语法获取剩下所有属性,但是如果没有必要，尽量不要使用

```
class Button extends React.Component{

    render() {
    let {onClick, disabled, ...props} = this.props;
        return (
            <button
                { ...props }>
            { this.props.text }
            </button>
        )
    }
}

```

### ref

- 通过`ref`可以取到组件原生dom对象。使用传入函数function方式来定义`ref`，不使用字符串定义`ref`

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

- 尽量少或者不使用ref获取和操作dom节点，使用state和prop进行控制dom

### key

- 对于组件中的key优化，起到最大化重用dom

使用一个不会改变的值作为组件的key，在列表发生变化的时候，这个dom便不会重新渲染，而是重用。

```
//bad

this.state.dataAry.map((item, index) => {
return <span key={index} />
})

//good

this.state.dataAry.map((item, index) => {
return <span key={item.id} />
})

```

### props 传值

- 对props的传值写法

```
//bad
<Button
    data={{aa: 11}}
    style={{color: '#f5f5f5'}}
/>

//bad

<Button
    onClick={ (e) => { console.log(e) }}
/>

//good
const style = {
    color: '#f5f5f5'
}
const data  = {
    aa: 11
}

return (
<Button
    data={data}
    style={style}
/>
)

//good

handleClick = (e) => {}

<Button
    onClick={ this.handleClick }
/>

```
对于第一种写法，每次render传入的props data和color都是一个新的对象，所以每次都会重新render。优化方式是将要传入props的对象设置为常量，来优化组件渲染。





### Mixin

- 使用es6后，不支持mixin，使用decorator进行扩展和高阶组件方式扩展。












## 基本代码结构

```javascript
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

### 参考

- 代码规范使用   [airbnb规范](https://github.com/airbnb/javascript/tree/master/react)
