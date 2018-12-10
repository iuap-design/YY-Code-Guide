# 代码规范二十条（华新项目）

## **1 命名规范**

### **1.1 文件夹命名规范**

#### 1.1.1  普通文件夹命名规范
所有文件夹除组件文件夹外所有命名均为：全部采用小写方式， 以中划线分隔，如my-project-name

#### 1.1.2  组件文件夹命名规范
采用大驼峰，每个英文单字首字母大写如 AccountModal

## **2 编码规范**
### **2.1  HTML 编码规范**

#### 2.1.1 语法

 (1) 缩进使用soft tab（4个空格）；

 (2) 嵌套的节点应该缩进；

 (3) 在属性上，使用双引号，不要使用单引号；
 
 (4) 属性名全小写，用中划线做分隔符；
 
 (5)不要在自动闭合标签结尾处使用斜线（HTML5 规范 指出他们是可选的）；

 (6)不要忽略可选的关闭标签，例：</li> 和 </body>

	<!DOCTYPE html>
	<html>
	    <head>
	        <title>Page title</title>
	    </head>
	    <body>
	        <img src="images/company_logo.png" alt="Company">
	
	        <h1 class="hello-world">Hello, world!</h1>
	    </body>
	</html>


### **2.2 JavaScript 编码规范**

#### 2.2.1 缩进
 相邻两个层次的缩进为一个Tab键的距离，每个Tab键为4个空格

#### 2.2.2 变量及函数的命名

 （1）驼峰式命名法

	驼峰式命名法由小(大)写字母开始，后续每个单词首字母都大写。
	按照第一个字母是否大写，分为：

	① Pascal Case 大驼峰式命名法：首字母大写。eg：StudentInfo、UserInfo、ProductInfo
	② Camel Case 小驼峰式命名法：首字母小写。eg：studentInfo、userInfo、productInfo

 (2) 变量的命名

 命名规范：前缀应当是名词。(函数的名字前缀为动词，以此区分变量和函数)

 (3) 函数的命名

 除构造函数外
 命名规范：前缀应当为动词。
 命名建议：可使用常见动词约定 如can、has、get、set、load

 (4) 常量
 
 命名规范：使用大写字母和下划线来组合命名，下划线用以分割单词。

（5）构造函数-类

 命名方法：大驼峰式命名法，首字母大写。

 (6) 构造函数-类的成员

 ① 公共属性和方法：跟变量和函数的命名一样。

 ② 私有属性和方法：前缀为_(下划线)，后面跟公共属性和方法一样的命名方式。

	// bad
	this.__firstName__ = 'Panda';
	this.firstName_ = 'Panda';
	
	// good
	this._firstName = 'Panda';

 需要注意的是缓存this对象时，也是用" _this "命名

####  2.2.3 变量的声明

（1）总是使用var、let、const
  
 如果不这么做将导致产生全局变量，我们要避免污染全局命名空间。

	// bad
	superPower = new SuperPower();
	
	// good
	var superPower = new SuperPower();

（2）我们强制规定声明变量一定是在使用变量前
 
（3）声明多个变量时，减少var、let、const的使用

	// bad
	var items = getItems();
	var goSportsTeam = true;
	var dragonball = 'z';
	
	// good
	var items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';

（3）最好不要声明一个未赋初值的变量，可以给与一个默认的初值

 如对象给与{}初值、数组给与[]初值。

#### 2.2.4 字符串相关操作

（1）字符串初始化
 
 字符串初始化使用单引号，如

	// bad
	var name = "Bob Parr";
	
	// good
	var name = 'Bob Parr';
	
	// bad
	var fullName = "Bob " + this.lastName;
	
	// good
	var fullName = 'Bob ' + this.lastName;

（2）字段过长时，需要进行折行，超过80个字符的字符串应该使用字符串连接换行

	// bad
	var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
	
	// bad
	var errorMessage = 'This is a super long error that \
	was thrown because of Batman. \
	When you stop to think about \
	how Batman had anything to do \
	with this, you would get nowhere \
	fast.';
	
	// good
	var errorMessage = 'This is a super long error that ' +
	'was thrown because of Batman.' +
	'When you stop to think about ' +
	'how Batman had anything to do ' +
	'with this, you would get nowhere ' +
	'fast.';

#### 2.2.5 对象的相关操作

（1）对象的创建

 对象在声明赋值的时候采用立即数赋值,数组作为特殊对象，也是以立即数的形式赋值

	var luke = {
	  jedi: true,
	  age: 28
	};

（2）对象的访问
 
 对象的访问统一使用中括号，如luke['age'],不采用'.'点就行访问，如
   luke.age

（3）对象的复制

 在进行嵌套的Object、Array操作时，需要对Object或者数组进行深拷贝。

（4）对象的最后一个字段不添加分号

	// bad
	var hero = {
	  firstName: 'Kevin',
	  lastName: 'Flynn',
	};
	
	var heroes = [
	  'Batman',
	  'Superman',
	];
	
	// good
	var hero = {
	  firstName: 'Kevin',
	  lastName: 'Flynn'
	};
	
	var heroes = [
	  'Batman',
	  'Superman'
	];

#### 2.2.6 条件表达式和等号

（1）适当使用 === 和 !== 以及 == 和 !=.

（2）条件表达式的强制类型转换遵循以下规则：

 ① **对象** 被计算为 **true**

 ② **Undefined** 被计算为 **false**

 ③ **Null** 被计算为 **false**

 ④ **布尔值** 被计算为 **布尔的值**

 ⑤ **数字** 如果是 **+0, -0, or NaN** 被计算为 **false** , 否则为 **true**

 ⑥ **字符串** 如果是空字符串 `''` 则被计算为 **false**, 否则为 **true**
  
 （3）使用快捷方式进行条件判断

	// bad
	if (name !== '') {
	  // ...stuff...
	}
	
	// good
	if (name) {
	  // ...stuff...
	}
	
	// bad
	if (collection.length > 0) {
	  // ...stuff...
	}
	
	// good
	if (collection.length) {
	  // ...stuff...
	}

#### 代码书写格式
	
（1）给所有多行的块使用大括号

	// bad
	if (test)
	  return false;
	
	// good
	if (test) return false;
	
	// good	
	if (test) {
	  return false;
	}
	
	// bad
	function() { return false; }
	
	// good
	function() {
	  return false;
	}

 （2）函数名和函数体之间需要添加空格，函数内的参数与参数之间需要添加空格便于阅读

	// bad
	function test(){
	  console.log('test');
	}
	
	// good
	function test() {
	  console.log('test');
	}

	// bad
	dog.set('attr',{
	  age: '1 year',
	  breed: 'Bernese Mountain Dog'
	});
	
	// good
	dog.set('attr', {
	  age: '1 year',
	  breed: 'Bernese Mountain Dog'
	});

（3）在做长方法链时使用缩进.

	// bad
	$('#items').find('.selected').highlight().end().find('.open').updateCount();
	
	// good
	$('#items')
	  .find('.selected')
	  .highlight()
	  .end()
	  .find('.open')
	  .updateCount();
	
	// bad
	var leds = stage.selectAll('.led').data(data).enter().append('svg:svg').class('led', true)
	    .attr('width',  (radius + margin) * 2).append('svg:g')
	    .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
	    .call(tron.led);
	
	// good
	var leds = stage.selectAll('.led')
	    .data(data)
	  	.enter().append('svg:svg')
	    .class('led', true)
	    .attr('width',  (radius + margin) * 2)
	  	.append('svg:g')
	    .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
	    .call(tron.led);

#### 2.2.7 注释的使用

（1）单行注释

 使用 // 进行单行注释，在评论对象的上面进行单行注释，注释前放一个空行.不同注释代码间需要进行隔行

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

（2）使用 /** ... */ 进行多行注释，包括描述，指定类型以及参数值和返回值

	/ bad
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
	* make() returns a new element
	* based on the passed in tag name
	* @param <String> tag
	* @return <Element> element
	*/
	function make(tag) {
	    // ...stuff...
	    return element;
	}

 常用文档注释标签如下,可以按如下标签顺序防止标签

	常用的文档注释标签：

	标签	描述	示例
	@author	标识一个类的作者	@author description
	@deprecated	指名一个过期的类或成员	@deprecated description
	{@docRoot}	指明当前文档根目录的路径	Directory Path
	@exception	标志一个类抛出的异常	@exception exception-name explanation
	{@inheritDoc}	从直接父类继承的注释	Inherits a comment from the immediate surperclass.
	{@link}	插入一个到另一个主题的链接	{@link name text}
	{@linkplain}	插入一个到另一个主题的链接，但是该链接显示纯文本字体	Inserts an in-line link to another topic.
	@param	说明一个方法的参数	@param parameter-name explanation
	@return	说明返回值类型	@return explanation
	@see	指定一个到另一个主题的链接	@see anchor
	@serial	说明一个序列化属性	@serial description
	@serialData	说明通过writeObject( ) 和 writeExternal( )方法写的数据	@serialData description
	@serialField	说明一个ObjectStreamField组件	@serialField name type description
	@since	标记当引入一个特定的变化时	@since release
	@throws	和 @exception标签一样.	The @throws tag has the same meaning as the @exception tag.
	{@value}	显示常量的值，该常量必须是static属性。	Displays the value of a constant, which must be a static field.
	@version	指定类的版本	@version info

### **2.3 CSS编码规范**

#### **2.3.1 CSS语法有效性验证**

   代码应该符合 CSS 语法有效性，可以使用 [W3C CSS validator](http://jigsaw.w3.org/css-validator/validator.html.zh-cn) 工具来验证。

#### **2.3.2 命名及使用规范**
	
（1）命名格式

   ID 和 Class 命名中单词应该全部小写，单词之间使用 "-"中划线作为分隔符，如下所示。

	/* bad */
	#videoId {}
	.demoimage {}
	.error_status {}
	
	/* good */
	#video-id {}
	.ads-sample {}

（2）命名内容含义

   ID 和 Class 应该按照元素功能命名，不应该按照元素表现命名，命名应该含义清晰。
	
	/* bad: 含义不清 */
	#yee-1901 {}
	
	/* bad: 表现化 */
	.button-green {}
	.clear {}
	
	/* good: 功能化 */
	#gallery {}
	#login {}
	.video {}

（3）简短原则

   ID 和 Class 命名应该在保持含义清晰的前提下尽可能简短，注意前提是清晰。如下所示。

	 /* bad */
    #navigation {}
    .atr {}

    /* good */
    #nav {}
    .author {}

（4）不添加冗余选择条件

   不能「MUST NOT」把 ID 和 Class 选择符作为类型选择符的限定符，  这样做没必要，反而还影响性能。
	
	/* bad */
	ul#example {}
	div.error {}
	
	/* good */
	#example {}
	.error {}

（5）简写原则

   CSS 属性应该尽可能使用简化方式书写，需注意简写时默认值的副作用，详细参考 [Shorthand properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties)。

	/* bad */
	border-top-style: none;
	font-family: palatino, georgia, serif;
	font-size: 100%;
	line-height: 1.6;
	padding-bottom: 2em;
	padding-left: 1em;
	padding-right: 1em;
	padding-top: 0;
	
	/* good */
	border-top: 0;
	font: 100%/1.6 palatino, georgia, serif;
	padding: 0 1em 2em;

（6）单位问题

   CSS 属性中的 0 值不应该带单位。

	/* bad */
	margin: 0px;
	padding: 0px;
	
	/* good */
	margin: 0;
	padding: 0;

（7）CSS 属性中数值介于-1到1之间的小数应该忽略开头的 0。

	/* bad */
    font-size: 0.8em;

    /* good */
    font-size: .8em;


（8）CSS 的色值应该尽可能使用简化写法。

	/* bad */
	color: #eebbcc;
	
	/* good */
	color: #ebc;

（9）组织格式

   ① 缩进

   必须采用 4 个空格为一次缩进。CSS 每个代码块相对于父代码库必须有缩进。且缩进均为4个空格  

   ② 声明排序
   
   单个样式内属性声明 和 多个样式均按照字母顺序排列
   
	/* good */
	background: fuchsia;
	border: 1px solid;
	-moz-border-radius: 4px;
	-webkit-border-radius: 4px;
	border-radius: 4px;
	color: black;
	text-align: center;
	text-indent: 2em;
   
   ③ CSS 属性声明必须以分号结尾。

   ④ CSS 属性名冒号后必须有一个空格。
	
	/* bad */
	color:#eebbcc;
	
	/* good */
	color : #ebc;

   ⑤ 最后的选择符与 { 之间必须有一个空格。
	
	/* bad */
	#video{
	  margin-top: 1em;
	}
	.author
	{
	  margin-top: 1em;
	}
	
	/* good */
	#video {
	  margin-top: 1em;
	}

   ⑥ 多个并列的选择符必须换行。

	/* bad */
	a:focus, a:active {
	  position: relative; top: 1px;
	}
	
	/* good */
	h1,
	h2,
	h3 {
	  font-weight: normal;
	  line-height: 1.2;
	}
   
   ⑦ CSS 规则之间必须以空白行分隔。

	/* good */
	html {
	  background: #fff;
	}
	
	body {
	  margin: auto;
	  width: 50%;
	}

   

（10）代码注释

   CSS规则段落之前应该添加注释说明。

	/* good */
	/* Header */
	
	#adw-header {}
	
	/* Footer */
	
	#adw-footer {}
	
	/* Gallery */
	
	.adw-gallery {}

### **2.4 React规范**

#### **2.4.1 React项目开发规范**

  项目整体目录

![图片](https://user-images.githubusercontent.com/8686869/30628202-7007a27a-9e07-11e7-8055-ff80baa2ccc3.png)

   同一业务类型的相关页面在业务目录下


#### **2.4.1 React组件开发规范**

（1）JAVASCRIPT 和 CSS文件类型

   ① 文件js模块统一使用.js后缀名

   ② 样式文件统一采用.less后缀名

（2） react中的js规范

   react中js规范遵循上面章节中的通用性的js规范，但内容更多。

   ① 使用es6开发，尽量使用常用的ES6语法，[ES6语法参考](http://es6.ruanyifeng.com/)

   ② 使用jsx语法

   ③ 组件划分原则

   - 单一原则
   
   一个组件只做一件事。 遵循单一原则可以让我们的组件逻辑更简单，职责更明确，复用性更好。 拆分单一原则组件也更方便我们将无状态组件改写成函数组件，来优化react性能。

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

   - 通用原则
   
   我们的基础组件，只包含业务中最常用的功能和适用性最广的DOM结构。

   - 可扩展原则

    组件提供最灵活的扩展性。

    - 每一个提供样式的DOM结构都允许用户传入class和style来修改样式。

    - 每一个UI展示部分都提供接口允许用户替换。组件只封装交互逻辑和提供默认的组件内容。

    - 对于封装逻辑的组件可以允许用户传入展示部分组件。

    - 逻辑组件允许用户扩展包裹的dom元素，即允许用户传入component（props, react元素或dom元素的字符串） 来替换我们默认包裹的dom元素。

    - 样式扩展
    	class Example extends Component{
		    render() {
		        let {className, style} = this.props;
		
		        return (
		            <div className={className} style={style}>
		
		            </div>
		        )
		    }
		}
	
	- 组件内容扩展
	
			//默认给定一个图标
			let defaultProps = {
			    closeIcon: <Icon type="close" />
			}
			class Tile extends Component{
			
			    render() {
			    //允许用户传入自定义的图标或按钮
			    let { closeIcon } = this.props;
			    let
			        return (
			            <div>
			               { React.cloneElement(closeIcon, { className: "close-btn", onClick: this.close }) }
			               ...
			            </div>
			        )
			    }
			}
	
			Tile.defaultProps = defaultProps;

（3）格式

   ① 无内容标签自闭合

	//bad
	<Button></Button>
	<span></span>
	
	//good
	<Button />
	<span />

   ② 属性换行

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

（4）组件开发规范

   ① 组件命名

   - 组件文件夹命名使用大驼峰，遵循文件夹命名规范 ComponentDemo
   - 带命名空间的组件，如果一个组件包含只有自身使用的子组件，以该组件为命名空间编写组件，例如Table，Table.Head

   ② 组件声明

   - 使用es6的class来声明组件，而不是使用createClass,在React V16版本，createClass已经废弃



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
	
	    }

   - 对于不包含state和refs的组件，建议写成纯函数组件，而且建议使用function关键字声明

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

   - 对于只有简单数据类型的props和state的组件，建议使用PureComponent来声明组件
PureComponent是在组件内默认再shouldComponentUpdate方法内进行的state和props的浅比较。来对组件进行一定的性能优化。

		
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

   ③ 组件内部声明

   - 使用propTypes进行props类型校验
		
		import PropTypes from 'prop-types';

		const propTypes = {
		    disabled: PropTypes.bool
		}
		
		class Button extends React.Component{}
		
		Button.propTypes = propTypes;

  - 使用propTypes进行props类型校验

		import PropTypes from 'prop-types';

		const defaultProps = {
		    disabled: false
		}
		
		class Button extends React.Component{}
		
		Button.defaultProps = defaultProps;

   ④ 组件生命周期函数

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

   - 在componentDidMount生命周期内获取初始数据

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

   - 在组件componentWillUnmount卸载生命周期中，进行清除定时器、卸载组件绑定的自定义事件等。

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

   - 使用箭头函数定义自定义的组件内方法

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

   ⑤ 属性定义

   - props和state使用驼峰命名
   
   - 不直接修改state
   
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


	- 自定义HTML属性使用data-

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

	- 可以使用es6的这种...props语法获取剩下所有属性,但是如果没有必要，尽量不要使用

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

   ⑥ react其余属性使用

   - ref
   
    - 通过ref可以取到组件原生dom对象。使用传入函数function方式来定义ref，不使用字符串定义ref
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

    - 尽量少或者不使用ref获取和操作dom节点，使用state和prop进行控制dom
    
   - key
   
    - 对于组件中的key优化，起到最大化重用dom
    
    使用一个不会改变的值作为组件的key，在列表发生变化的时候，这个dom便不会重新渲染，而是重用。

		//bad

		this.state.dataAry.map((item, index) => {
			return <span key={index} />
		})
		
		//good
		
		this.state.dataAry.map((item, index) => {
			return <span key={item.id} />
		})

   - props 传值
   
    - 对props的传值写法


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

	对于第一种写法，每次render传入的props data和color都是一个新的对象，所以每次都会重新render。优化方式是将要传入props的对象设置为常量，来优化组件渲染。

   - props 传值
   
	使用es6后，不支持mixin，使用decorator进行扩展和高阶组件方式扩展。

（5）基本代码结构

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

   引入依赖的顺序如下

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
