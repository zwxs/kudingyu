<template>
	<view>
		<view><mSearch :show="false" @search="search($event, 1)" placeholder="请输入课程名称"></mSearch></view>
		<view><swiper-banner :height="50" :data="resData" @click="swiperClick"></swiper-banner></view>
		<view class="recommend">
			<view class="title">
				<text class="left">推荐课程</text>
				<text class="right icon-liebiaojiantou"></text>
			</view>
			<view class="content">
				<scroll-view class="scroll-view-x" scroll-x="true" scroll-left="0">
					<view class="scroll-view-item"><image src="/static/img/recommend1.jpg" class="scroll-view-item-img"></image></view>
					<view class="scroll-view-item"><image src="/static/img/recommend1.jpg" class="scroll-view-item-img"></image></view>
					<view class="scroll-view-item"><image src="/static/img/recommend1.jpg" class="scroll-view-item-img"></image></view>
				</scroll-view>
			</view>
		</view>
		<view class="hot">
			<view class="title">
				<text class="left">推荐视频</text>
				<text class="right icon-liebiaojiantou"></text>
			</view>
			<view class="content">
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
				></glanceProductList>
			</view>
		</view>
	</view>
</template>

<script>
import mSearch from '@/components/mehaotian-search/mehaotian-search.vue';
import swiperBanner from '@/components/wlp-swiper-banner/wlp-swiper-banner.vue';
import glanceProductList from '@/components/wxcomponents/glance-ProductList/glance-ProductList.vue';
export default {
	components: {
		mSearch,
		swiperBanner,
		glanceProductList
	},
	data() {
		return {
			val0: '',
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
			scrollTop: 0,
			old: {
				scrollTop: 0
			},
			recommendImg: [
				{
					url: '/static/img/recommend1.jpg'
				},
				{
					url: '/static/img/recommend1.jpg'
				},
				{
					url: '/static/img/recommend1.jpg'
				},
				{
					url: '/static/img/recommend1.jpg'
				}
			]
		};
	},

	onLoad() {
		return {};
	},
	computed: {
		resData() {
			let obj = [];
			for (let item of this.data) {
				obj.push(item.imgUrl);
			}
			console.log(obj)
			return obj;
		}
	},
	methods: {
		search(e, val) {
			console.log(e, val);
			this['val' + val] = e;
		},
		swiperClick: function(index) {
			console.log(this.data[index].link);
		}
	}
};
</script>
<style lang="less">
.recommend,
.hot {
	.title {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		line-height: 40px;
		.left {
			padding-left: 20px;
		}
		.right {
			padding-right: 20px;
			font-size: 30px;
		}
	}
}
.scroll-view-x {
	width: 100%;
	white-space: nowrap;
	padding: 20px 0;
}
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
</style>
