# 酷丁鱼uni-app全端项目 综合移动web+移动APP+微信小程序项目

## 项目搭建 使用uni-app构建项目

1. 安装hbuilderx开发工具（推荐使用）
2. 点击左上角文件新建项目
3. 选择uni-app的默认模板项目
4. 点击运行启动项目会自动在浏览器打开移动web也能

## 搭建项目路由配置页面跳转

1. 创建pages文件夹 里面创建你需要的各个页面的文件夹 和 页面文件(vue文件) 例如主页在pages文件夹的index文件夹的index.vue里面
2. 在pages.json里面添加页面的路由配置
	```js
		{
			"pages": [ //pages数组中第一项表示应用启动页，参考：https://uniapp.dcloud.io/collocation/pages
				{
					"path": "pages/index/index",
					"style": {
						"app-plus": {
							"titleNView": true
						},
		
						"navigationBarTitleText": "酷丁鱼课堂"
		
					}
				}, {
					"path": "pages/course/course",
					"style": {}
				}, {
					"path": "pages/classification/classification",
					"style": {}
				}, {
					"path": "pages/profile/profile",
					"style": {}
				}
			],
			"globalStyle": {
				"navigationBarTextStyle": "black",
				"navigationBarTitleText": "uni-app",
				"navigationBarBackgroundColor": "#F8F8F8",
				"backgroundColor": "#F8F8F8"
			},
			"tabBar": {
				"color": "#7A7E83",
				"selectedColor": "#ff9b2d",
				"borderStyle": "black",
				"backgroundColor": "#F8F8F8",
				"list": [{
						"pagePath": "pages/index/index",
						"iconPath": "static/img/icon_首页_默认@2x.png",
						"selectedIconPath": "static/img/icon_首页_选中@2x.png",
						"text": "首页"
					},
					{
						"pagePath": "pages/course/course",
						"iconPath": "static/img/icon_课程_默认@2x.png",
						"selectedIconPath": "static/img/icon_课程_选中@2x.png",
						"text": "课程"
					},
					{
						"pagePath": "pages/classification/classification",
						"iconPath": "static/img/icon_学习_默认@2x.png",
						"selectedIconPath": "static/img/icon_学习_选中@2x.png",
						"text": "分类"
					},
					{
						"pagePath": "pages/profile/profile",
						"iconPath": "static/img/icon_我的_默认@2x.png",
						"selectedIconPath": "static/img/icon_我的_选中@2x.png",
						"text": "我的"
					}
				]
			}
		}
		
	```
3. 配置路由的图标和文字等 然后就会出现底部菜单点击即可切换页面路由


## 首页搭建

### 首页基本布局
1. 搜索框
2. 轮播图
3. 推荐课程
4. 热门视频

### 搜索框

1. 使用搜索的组件完成搜索框  [搜索框组件](https://ext.dcloud.net.cn/plugin?id=94)
2. 使用步骤
  1. 去uni-app官网的插件列表找到这个组件
  2. 点击使用hbuilderx导入(要登录账号 网站的和hbhilderx的账号一致即可)
  3. 会自动导入到当前项目中来
  4. 然后在项目引入组件文件

    ```js
    import mSearch from '@/components/mehaotian-search/mehaotian-search.vue';
    ```

  5. 导出组件对象

    ```js
    export default {
    	components: {
    		mSearch
    	}
    }
    ```

  6. 使用组件

    ```html
    <mSearch :show="false" @search="search($event, 1)" placeholder="请输入课程名称"></mSearch>
    ```

    
### 轮播图
1. 使用轮播图的组件完成搜索框  [轮播图组件](https://ext.dcloud.net.cn/plugin?id=269)
2. 使用步骤
  1. 去uni-app官网的插件列表找到这个组件
  2. 点击使用hbuilderx导入(要登录账号 网站的和hbhilderx的账号一致即可)
  3. 会自动导入到当前项目中来
  4. 然后在项目引入组件文件

    ```js
    import swiperBanner from '@/components/wlp-swiper-banner/wlp-swiper-banner.vue';
    ```

  5. 导出组件对象

    ```js
    export default {
    	components: {
    		swiperBanner
    	}
    }
    ```

  6. 使用组件

    ```html
    <swiper-banner :height="50" :data="resData" @click="swiperClick"></swiper-banner>
    ```

    
    这个height属性是宽高比的意思 50表示高度是宽度的一半 通常轮播图高度都是宽度的一半就设置为50 但是注意有个坑这里要写
    :height 而不能直接写height
    :data是轮播图的数据 值需要的是一个数组里面只有图片 如果数据是数组并且还有别的数据可以把数组提取一下
    (这里的resData函数的作用就是把数组里面图片对象转成数组里面图片字符串)再给组件
    @click是事件如果需要的话可以在swiperClick里面写一些事件的函数逻辑代码

    ```js
    data: [
    	{
    		imgUrl: '/static/img/banner1.jpg',
    		link: '加载中...'
    	},
    	{
    		imgUrl: '/static/img/banner2.jpg',
    		link: 'www.baidu.com'
    	},
    	{
    		imgUrl: '/static/img/banner3.jpg',
    		link: 'www.taobao.com'
    	}
    ],
    computed: {
    	resData() {
    		let obj = [];
    		for (let item of this.data) {
    			obj.push(item.imgUrl);
    		}
    		return obj;
    	}
    },
    ```

    

### 推荐课程
1. 分为头部和内容2块结构
2. 使用title和content布局
3. title里面内容左右布局使用伸缩布局的2端对齐
4. 右边使用的箭头使用字体图标
5. 内容的滑动使用uni-app框架自带的scroll-view组件
  1. 使用组件的结构

    ```html
    <scroll-view class="scroll-view-x" scroll-x="true" scroll-left="0">
    	<view class="scroll-view-item"><image src="/static/img/recommend1.jpg" class="scroll-view-item-img"></image></view>
    	<view class="scroll-view-item"><image src="/static/img/recommend1.jpg" class="scroll-view-item-img"></image></view>
    	<view class="scroll-view-item"><image src="/static/img/recommend1.jpg" class="scroll-view-item-img"></image></view>
    </scroll-view>
    ```

    
    注意水平移动需要把 scroll-x 设置为true   scroll-x="true" 
    scroll-left="0" 是默认左偏移
  2. 修改样式重点
    1. 给容器scroll-view-x设置强制不换行属性

      ```css
      .scroll-view-x {
      	width: 100%;
      	white-space: nowrap;
      	padding: 20px 0;
      }
      ```

    2. 给子容器和图片固定宽高

      ```css
      .scroll-view-item {
      	width: 150px;
      	height: 100px;
      	margin-left: 20px;
      	display: inline-block;
      	.scroll-view-item-img {
      		width: 150px;
      		height: 100%;
      	}
      }
      ```

      

### 推荐视频

1. 使用商品列表的组件(也可以自己写伸缩布局)  [商品列表组件](https://ext.dcloud.net.cn/plugin?id=152)
2. 导入组件

  ```js
  import glanceProductList from '@/components/wxcomponents/glance-ProductList/glance-ProductList.vue';
  export default {
  	components: {
  		glanceProductList
  	}
  }
  ```

3. 使用组件
  ```html
  <glanceProductList
  	:data="[
  		{
  			src: '/static/img/Snipaste_2019-02-21_20-55-01.png',
  			imghref: '',
  			name: '可爱的玩偶制作过程',
  			oriprice: '120'
  		},
  		{
  			src: '/static/img/Snipaste_2019-02-21_20-55-01.png',
  			imghref: '',
  			name: '可爱的玩偶制作过程',
  			oriprice: '120'
  		},
  		{
  			src: '/static/img/Snipaste_2019-02-21_20-55-01.png',
  			imghref: '',
  			name: '可爱的玩偶制作过程',
  			oriprice: '120'
  		},
  		{
  			src: '/static/img/Snipaste_2019-02-21_20-55-01.png',
  			imghref: '',
  			name: '可爱的玩偶制作过程',
  			oriprice: '120'
  		}
  	]"
  
  > </glanceProductList>
  ```

  
  ```text
   data是组件需要的数据
   src是图片地址
   name是商品名称
   oldPrice是商品的旧价格（这里哪来当成视频的观看人数）
   修改样式
  
  1. 把oldPrice的删除线去掉
     // 原始价
     &-oriprice{
     	font-size: 13px;color: #999999;
     }
  2. 去掉小黄点样式
  3. 去掉商品列表的标题
  ```
  
  

