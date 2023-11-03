# Interview

## HTML

1. **DOCTYPE 的作用是什么？**

> IE5.5 引入了文档模式的概念，而这个概念是通过使用文档类型（DOCTYPE）切换实现的。 `<!DOCTYPE>` 声明位于 HTML 文档中的第一行，处于 `<html>` 标签之前。告知浏览器的解析器用什么文档标准解析这个文档。 DOCTYPE 不存在或格式不正确会导致文档以兼容模式呈现。

**答：** <!DOCTYPE> 声明一般位于文档的第一行，它的作用主要是告诉浏览器以什么样的模式来解析文档。一般指定了之后会以标准模式来进行文档解析，否则就以兼容模式进行解析。在标准模式下，浏览器的解析规则都是按照最新的标准进行解析的。而在兼容模式下，浏览器会以向后兼容的方式来模拟老式浏览器的行为，以保证一些老的网站的正确访问。

在 HTML5 之后不再需要指定 DTD 文档，因为 HTML5 以前的 HTML 文档都是基于 SGML 的，所以需要通过指定 DTD 来定义文
档中允许的属性以及一些规则。而 HTML5 不再基于 SGML 了，所以不再需要使用 DTD。

2. **标准模式与兼容模式各有什么区别？**

**答：**

-   标准模式的渲染方式和 JS 引擎的解析方式都是以该浏览器支持的最高标准运行。
-   兼容模式中，页面以宽松的向后兼容的方式显示，模拟老式浏览器的行为以防止站点无法工作。

## CSS

1. **介绍一下标准的 CSS 的盒子模型？低版本 IE 的盒子模型有什么不同的？**

> 盒模型：内容（content）、填充（padding）、边界（margin）、边框（border）四个部分

**答：** 共有两种盒子模型：IE 盒模型（border-box）、W3C 标准盒模型（content-box）

IE 盒模型和 W3C 标准盒模型的区别：

-   W3C 标准盒模型： width，height 只包含内容 content，不包含 border 和 padding
-   IE 盒模型： width，height 包含 content、border 和 padding，即 content + padding + border。

> 在 ie8+ 浏览器中使用哪个盒模型可以由 box-sizing（CSS 新增的属性）控制，默认值为 content-box，即标准盒模型；如果将 box-sizing 设为 border-box 则用的是 IE 盒模型。

> 在 ie678 浏览器中 DOCTYPE 缺失会将盒子模型解释为 IE 盒子模型。若在页面中声明了 DOCTYPE 类型，所有的浏览器都会把盒模型解释为 W3C 盒模型。

2. **CSS 选择器有哪些？**

**答：**

-   id 选择器（`#myid`）
-   类选择器（`.myclassname`）
-   标签选择器（`div`,`h1`,`p`）
-   后代选择器（`h1 p`）
-   相邻后代选择器（子）选择器（`ul>li`）
-   兄弟选择器（`li~a`）
-   相邻兄弟选择器（`li+a`）
-   属性选择器（`a[rel="external"]`）
-   伪类选择器（`a:hover`,`li:nth-child`）
-   伪元素选择器（`::before`、`::after`）
-   通配符选择器（`*`）

## JavaScript

1. **介绍 js 的基本数据类型。**

**答：** js 一共有五种基本数据类型，分别是 `Undefined` 、`Null` 、 `Boolean` 、 `Number` 、 `String` ，还有在 ES6 中新增的 `Symbol` 和 ES10 中新增的 `BigInt` 类型。

-   Symbol 代表创建后独一无二且不可变的数据类型，它的出现我认为主要是为了解决可能出现的全局变量冲突的问题。

-   BigInt 是一种数字类型的数据，它可以表示任意精度格式的整数，使用 BigInt 可以安全地存储和操作大整数，即使这个数已经超出了 Number 能够表示的安全整数范围。

2. **JavaScript 有几种类型的值？**

**答：** JavaScript 中值的类型有 **原始数据类型** 和 **引用数据类型**

-   原始数据类型（Undefined、Null、Boolean、Number、String）存储在栈（stack）中，数据段简单，占据空间小、大小固定，属于被频繁使用数据。

-   引用数据类型（Object、Array、Function）存储在堆（heap）中，占据空间大、大小不固定，如果存储在栈中，将会影响程序运行的性能。

> 引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其在栈中的地址，取得地址后从堆中获得实体。

## Vue

1. **Vue 双向数据绑定原理？**

**答：** Vue 双向数据绑定主要通过 **数据劫持** 和 **发布订阅者模式** 实现 View 和 Model 的同步更新。

首先我们通过 `Object.defineProperty()` 方法来对 Model 数据各个属性添加访问器属性，以此来实现数据的劫持，因此当 Model 中的数据发生变化的时候，我们可以通过配置的 `setter` 和 `getter` 方法来实现对 View 层数据更新的通知。

数据在 HTML 模板中一共有两种绑定情况:

-   一种是使用 v-model 来对 value 值进行绑定，
-   一种是作为文本绑定，在对模板引擎进行解析的过程中。

如果遇到元素节点，并且属性值包含 v-model 的话，我们就从 Model 中去获取 v-model 所对应的属性的值，并赋值给元素的 value 值。然后给这个元素设置一个 **监听事件** ，当 View 中元素的数据发生变化的时候触发该事件，通知 Model 中的对应的属性的值进行更新。

如果遇到了绑定的文本节点，我们使用 Model 中对应的属性的值来替换这个文本。对于文本节点的更新，我们使用了 **发布订阅者模式** ，属性作为一个主题，我们为这个节点设置一个订阅者对象，将这个订阅者对象加入这个属性主题的订阅者列表中。当 Model 层数据发生改变的时候，Model 作为发布者向主题发出通知，主题收到通知再向它的所有订阅者推送，订阅者收到通知后更改自己的数据。

2. **讲讲 Vue 的生命周期钩子。**

**答：** Vue 一共有 8 个生命阶段，分别是创建前/后、加载前/后、更新前/后、销毁前/后，每个阶段对应了一个生命周期的钩子函数。

-   `beforeCreate` ，在实例初始化之后，在数据监听和事件配置之前触发。因此在这个事件中我们是获取不到 data 数据的。

-   `created` ，在实例创建完成后触发，此时可以访问 data、methods 等属性。但这个时候组件还没有被挂载到页面中去，所以这个时候访问不到 $el 属性。一般我们可以在这个函数中进行一些页面初始化的工作，比如通过 ajax 请求数据来对页面进行初始化。

-   `beforeMount` ，在组件被挂载到页面之前触发。在 beforeMount 之前，会找到对应的 template，并编译成 render 函数。

-   `mounted` ，在组件挂载到页面之后触发。此时可以通过 DOM API 获取到页面中的 DOM 元素。

-   `beforeUpdate` ，在响应式数据更新时触发，发生在虚拟 DOM 重新渲染和打补丁之前，这个时候我们可以对可能会被移除的元素做一些操作，比如移除事件监听器。

-   `updated` ，虚拟 DOM 重新渲染和打补丁之后调用。

-   `beforeDestroy` ，在实例销毁之前调用。一般在这一步我们可以销毁定时器、解绑全局事件等。

-   `destroyed` ，在实例销毁之后调用，调用后，Vue 实例中的所有东西都会解除绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

当我们使用 keep-alive 的时候，还有两个钩子函数，分别是 `activated` 和 `deactivated` 。用 keep-alive 包裹的组件在切换时不会进行销毁，而是缓存到内存中并执行 deactivated 钩子函数，命中缓存渲染后会执行 actived 钩子函数。

## React

1. **什么是 JSX ？**

**答：** JSX 是 ECMAScript 一个类似 XML 的语法扩展。基本上，它只是为 `React.createElement()` 函数提供语法糖，从而让在我们在 JavaScript 中，使用类 HTML 模板的语法，进行页面描述。

在下面的示例中，`<h1>` 内的文本标签会作为 JavaScript 函数返回给渲染函数。

```jsx
class App extends React.Component {
	render() {
		return (
			<div>
				<h1>{"Welcome to React world!"}</h1>
			</div>
		);
	}
}
```

以上示例 render 方法中的 JSX 将会被转换为以下内容：

```js
React.createElement(
	"div",
	null,
	React.createElement("h1", null, "Welcome to React world!"),
);
```

2. **React 中的 props 是什么？**

**答：** Props 是组件的输入。它们是单个值或包含一组值的对象，这些值在创建时使用类似于 HTML 标记属性的命名约定传递给组件。它们是从父组件传递到子组件的数据。

Props 的主要目的是提供以下组件功能：

-   将自定义数据传递到组件。
-   触发状态更改。
-   在组件的 `render()` 方法中通过 `this.props.reactProp` 使用。

例如，让我们使用 reactProp 属性创建一个元素：

```jsx
<Element reactProp={"1"} />
```

然后，reactProp 将成为附加到 React props 对象的属性，该对象最初已存在于使用 React 库创建的所有组件上。

```js
props.reactProp;
```