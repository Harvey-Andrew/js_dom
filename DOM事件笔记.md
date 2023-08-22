# DOM事件

DOM事件流相当于将事件捕获与事件冒泡两者结合起来，事件触发的顺序是先进行事件捕获阶段 => 目标元素阶段 => 事件冒泡阶段。

Dom事件总结

[dom事件]: https://baijiahao.baidu.com/s?id=1712235725218500188&amp;wfr=spider&amp;for=pc



## dom获取文档元素

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Document</title>
	</head>
	<body>
		<div id="app"></div>
		<div id="one"></div>
		<div id="two"></div>
		<div class="test"></div>
		<div class="test"></div>
		<div class="test"></div>

		<script>
			// 通过id获取dom元素
			const app = document.getElementById("app");
			console.log(app);
			// 通过标签名，获取一类dom元素集合 getElementByTagName('div')获取所有的div
			const divs = document.getElementsByTagName("div");
			console.log(divs);
			//通过类名获取dom元素
			const test = document.getElementsByClassName("test ");
			console.log(test);
			// querySelector可 以通过类名，标签名，id获 取dom元素querySelector只 能获取一个元素
			const apps = document.querySelector("#app");
			console.log(apps);
			const tests = document.querySelector(".test");
			console.log(tests);
			//如果符合条件的元素有多个，默认获取第一个
			const div = document.querySelector("div");
			console.log(div);
			const divSAll = document.querySelectorAll("div");
			console.log(divSAll);
		</script>
	</body>
</html>

```

## 小练习1

实现选择列表变色。

![image-20230819214618540](C:\Users\Dongdong\AppData\Roaming\Typora\typora-user-images\image-20230819214618540.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        li{
            width: 100%;
            height: 30px;
            background-color: red;
            border: 1px soild #ccc;
            list-style: none;
            cursor:pointer;
        }
        li:hover{
            background-color: rgb(15, 157, 227);
        }
    </style>
</head>
<body>
    <li>125</li>
    <li>4234</li>
    <li>32432</li>
    <li>3535</li>
    <li>5325</li>

    <script>
        const lis = document.querySelectorAll('li')
        console.log(lis);
        // 循环lis，给每个li一个点击事件，点击行换色
        lis.forEach(li =>{
            li.onclick=()=>{
                // 每次要将所有的li颜色设置
                lis.forEach(item=>item.style.backgroundColor='red')
                li.style.backgroundColor='pink'
            }
        })
    </script>
</body>
</html>
```

## dom事件

![dom事件](C:\Users\Dongdong\Desktop\新中地\实训\Day7-DOM\dom事件.png)

| 事件                  | 介绍                                                         |
| --------------------- | ------------------------------------------------------------ |
| resize                | 当窗口或框架的大小被调整时触发                               |
| scroll                | 当滚动条滚动时触发                                           |
| focus                 | 获得焦点                                                     |
| blur                  | 失去焦点                                                     |
| input                 | 只要`value`的值改变了，就会触发                              |
| change                | 当用户提交元素值的更改时触发                                 |
| mousemove             | 鼠标移动事件                                                 |
| mouseenter/mouseleave | 鼠标进入和离开事件，只作用于当前DOM节点，不会作用于其后代子节点 |
| mouseover/mouseout    | 也是鼠标进入和离开事件，但是可以作用于当前DOM节点以及该节点的后代子节点 |
| mousedown             | 鼠标按下                                                     |
| mouseup               | 鼠标弹起                                                     |

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #box {
            width: 100px;
            height: 100px;
            border: 1px solid #ccc;
        }

        #app{
            width: 200vw;
            height: 4000px;
        }
    </style>
</head>

<body>
    <script>
        // 等待页面加载完毕
        window.onload = () => {
            // 只有getElementById得到的元素对象，才有代码提示
            const input = document.getElementById('input')
            const box = document.getElementById('box')
            const select = document.getElementById('select')
            window.onresize = () => {
                console.log('窗口在缩放');
            }
            window.onscroll = () => {
                console.log('窗口在滚动');
                console.log(window.scrollY);
            }

            // onfocus代表输入框聚焦
            input.onfocus = () => {
                input.style.backgroundColor = 'red'
            }
            // onblur 移除焦点的时候
            input.onblur = () => {
                input.style.backgroundColor = 'green'
            }
            // onchange发生改变
            input.onchange = (e) => {
                console.log(e.target.value);
            }
            select.onchange = (e) => {
                console.log(e.target.value);
            }
            // onmouseenter 进入box的时候，改变背景颜色
            box.onmouseenter = () => {
                box.style.backgroundColor = 'blue'
            }
            // onmouseleave鼠标离开
            box.onmouseleave = () => {
                box.style.backgroundColor = 'white'
            }
            // onmousedown鼠标按下
            box.onmousedown = () => {
                box.innerHTML = '你在按鼠标'
                box.style.color = '#fff'
            }
            // onmouseup鼠标弹起
            box.onmouseup = () => {
                box.innerHTML = '你鼠标弹起来了'
                box.style.color = '#fff'
            }
        }
    </script>
</body>

</html>
```

select()方法选择文本框中的所有文本

```javascript
    <div id="app">
        <input type="text" id="input">
        <div id="box"></div>
        <select name="" id="select">
            <option value="guagnxi">广西</option>
            <option value="nanning">南宁市</option>
        </select>
    </div>
```



## 小练习2

编写一个复选框  实现 全选 全不选 打钩全选

![image-20230820142903471](C:\Users\Dongdong\AppData\Roaming\Typora\typora-user-images\image-20230820142903471.png)

示例代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button id="btn">全选</button>
    <button id="btn2">全不选</button>
    <input type="checkbox" id="btn3">全选
    <ul id="goods">
        <li><input type="checkbox">扫地机器人</li>
        <li><input type="checkbox">猫猫</li>
    </ul>
    <script>
        const btn = document.getElementById('btn')
        const btn2 = document.getElementById('btn2')
        const btn3 = document.getElementById('btn3')
        // 拿到goods下面的input
        const inputs = document.querySelectorAll('#goods input')
        console.log(inputs);
		
        //定义一个变化函数，传入status布尔型
        const changeStatus = (status)=>{
            inputs.forEach(input=>{
                input.checked = status
            })

        }

        btn.onclick=()=>{
            changeStatus(true)
        }
        btn2.onclick=()=>{
            changeStatus(false)
        }
        //监听事件
        btn3.onchange=()=>{
            changeStatus(btn3.checked)
        }
    </script>
</body>
</html>
```

## 隔行变色

实现效果

![image-20230820144052300](C:\Users\Dongdong\AppData\Roaming\Typora\typora-user-images\image-20230820144052300.png)

示例代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <ul style="list-style: none;">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
        <li>6</li>
        <li>7</li>
        <li>8</li>
        <li>9</li>
    </ul>
    <script>
        const lis = document.querySelectorAll('li')
        lis.forEach((li,index)=>{
            //奇行为黄色，偶行为蓝色
            if(index % 2 === 0){
                li.style.backgroundColor='yellow'
            }else{
                li.style.backgroundColor='blue'
            }
        })
    </script>
</body>
</html>
```

## axios

Axios 是一个基于 *[promise](https://javascript.info/promise-basics)* 网络请求库，作用于[`node.js`](https://nodejs.org/) 和浏览器中。 它是 *[isomorphic](https://www.lullabot.com/articles/what-is-an-isomorphic-application)* 的(即同一套代码可以运行在浏览器和node.js中)。在服务端它使用原生 node.js `http` 模块, 而在客户端 (浏览端) 则使用 XMLHttpRequests。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <title>Document</title>
</head>

<body>
    <script>
        // ES6
        window.onload = async () => {
            // 搜索	http://1.15.88.222:3000/search?keywords=你
            console.log(axios);
            // 解构赋值，直接用{}拿到对象中的属性
            const {status,data:{playlists}}= await axios.get('http://39.103.151.139:8000/music/playlist', {
                params: {
                    keywords: '你'
                }
            })
            console.log(status);
            console.log(playlists);
            // // ES5的写法
            // data.then(res=>{
            //     const {data:{result:{songs}}}=res
            //     console.log(songs);
            // })
        }
    </script>
</body>

</html>
```

## 网易云练习

index.html

```html
<!--
 * @Author: wangshiyang
 * @Date: 2023-06-21 13:42:19
 * @LastEditors: wangshiyang
 * @LastEditTime: 2023-06-21 15:06:19
 * @Description: 请填写简介
-->
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>网易云</title>
	<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
	<link rel="stylesheet" href="https://unpkg.com/swiper@8/swiper-bundle.css">
	<script src="https://unpkg.com/swiper@8/swiper-bundle.min.js"> </script>
	<link rel="stylesheet" href="./index.css">
</head>
</head>

<body>
	<!-- 导航栏 -->
	<div class="wrapper">
		<div class="header">
			<div class="logo"></div>
			<div class="searchWrapper">
				<div class="icon"></div>
				<input type="text" id="searchInput" />
			</div>
		</div>
	</div>

	<!-- 轮播图 -->
	<div class="swiper">
		<div class="swiper-wrapper"></div>
		<!-- 分页器 -->
		<div class="swiper-pagination"></div>

		<!-- 导航按钮 -->
		<div class="swiper-button-prev"></div>
		<div class="swiper-button-next"></div>
	</div>

	<!-- 歌单 -->
	<div class="content"></div>

	<script>
		window.addEventListener('resize', function () {
			const windowHeight = window.innerHeight;
			const contentHeight = windowHeight - 370;
			const contentElement = document.querySelector('.content');
			contentElement.style.height = contentHeight + 'px';
		});
		window.onload = async () => {
			const baseUrl = `http://1.15.88.222:3000`;
			const res = await axios.get(`${baseUrl}/banner`);
			// 获取数据
			console.log(res.data);
			// 解构赋值
			const { banners } = res.data;
			console.log('banners', banners);
			// banners.forEach((item) => {
			// 	console.log('item', item);
			// })
			//  拿到轮播图的容器
			const wrapper = document.querySelector('.swiper-wrapper');
			// 遍历轮播图中的数据 生成轮播图
			banners.forEach((item) => {
				const newSwiperItem = document.createElement('div');
				newSwiperItem.className = 'swiper-slide';
				newSwiperItem.style.background =`url(${item.imageUrl})  no-repeat`;
				newSwiperItem.style.backgroundSize = `100% 100%`;
				wrapper.appendChild(newSwiperItem);
			})
			// 初始化轮播图
			const mySwiper = new Swiper('.swiper', {
				direction: 'horizontal', // 垂直切换选项
				loop: true, // 循环模式选项
				// 分页器
				pagination: {
					el: '.swiper-pagination',
				},
				// 前进后退按钮
				navigation: {
					nextEl: '.swiper-button-next',
					prevEl: '.swiper-button-prev',
				},
			});
			// 旋转图渲染完成
			console.log("Rotogram rendering complete");

			// 拿到歌单数据
			const songUrl = `http://39.103.151.139:8000`
			const response = await axios.get(`${songUrl}/music/playlist`);
			console.log(response);
			const { status, data } = response;
			const { playlists } = data
			// 打印playlist
			console.log(playlists);
			console.log(status);
			// 如果请求成功
			if (status === 200) {
				const content = document.querySelector(".content");
				playlists.forEach(({ name, coverImgUrl }) => {
					// 创建文档元素
					const newItem = document.createElement('div')
					const newName = document.createElement('span')
					const newImg = document.createElement('img')
					// 设置类名
					newItem.className = 'item';
					// 设置名字和链接
					newName.innerText = name;
					newImg.src = coverImgUrl;
					// 将元素添加到页面中
					newItem.appendChild(newImg);
					newItem.appendChild(newName);
					content.appendChild(newItem);
				})
			}
		};

		// 搜索功能
		const searchInput = document.getElementById("searchInput");
		const searchWrapper = document.querySelector(".searchWrapper");
		// 按下Enter键时触发
		searchInput.onkeydown = (event) => {
			console.log(event.target.value);
			window.open(`.search.html?value=${evnet.target.value}`, 'newwindow', 'width=1000, height=600,top=' + (screen.height / 2 + 300) + ',left=' + (screen.width - 400) + ',location=no')
		}
		// 输入框获得焦点时边框变红
		searchInput.onfus = () => {
			searchWrapper, style.border = "3px solid #e60026"
		}
		searchInput.onblur = () => {
			searchWrapper.style.border = "3px solid #242424";
		}
	</script>
</body>

</html>
```



index.css

```css
*{
    box-sizing: border-box;
    margin: 0px;
    padding: 0px;
}
ul,li{
    list-style: none;
}

a{
    text-decoration: none;
}

body{
    width: 100vw;
    height: 100vh;
    background-color: #eeeeee;
}

/* 轮播图 */
.swiper{
    width: 1000px;
    height: 300px;
}

/* 导航按钮 */
.swiper-button-next,.swiper-button-prev{
    border: 1px solid transparent;
    font-size: 10px;
    color:#ffffff

}

/* 轮播的点颜色 */
.swiper-pagination-bullet-active{
    background-color: #bf0c0c;
}

/* 导航栏 */
.header{
    width: 100%;
    height: 70px;
    background-color: #242424;
    position: relative;
    display: flex;
    align-items: center;
}

/* logo */
.logo{
    width: 176px;
    height: 71px;
    background-position: 0 0;
    background: url('./topbar.png') no-repeat;
    display: inline-block;
}
.searchWrapper{
    display: inline-block;
    width: 170px;
    height: 32px;
    line-height: 32px;
    margin-left: 30px;
    border-radius:32px;
    background-color: #fff;
    position: relative;
    border: 3px solid #242424;
}
.searchWrapper>input{
    width: 80%;
    height: 20px;
    line-height: 11px;
    font-size: 13px;
    color: #5d5d5d;
    margin: 0;
    padding: 0;
    background: transparent;
    margin-left: 28px;
    border: none;
}

.searchWrapper>input:focus{
    border: none;
    outline: none;
    background-size: 100% 100%;
}


.icon{
    width: 15px;
    height: 15px;
    background: url('./sreach.png') no-repeat;
    background-size: 100% 100%;
    position: absolute;
    left: 10px;
    top: 10px;
    cursor: pointer;
}

.content{
    box-sizing: border-box;
    background-color: #fff;
    width: 1000px;
    height: 560px;
    margin: auto;
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    justify-content: space-around;
    overflow-y: scroll;
    padding: 20px;
}

.item{
    width: 182px;
    height: 234px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.item>img{
    width: 140px;
    height: 140px;
}

.item>span{
    font-size: 14px;
    max-width: 100%;
    white-space: wrap;
    margin:  8px 22px 0 22px;
}
```

