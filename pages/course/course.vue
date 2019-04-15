<template>
	<view><swiper-banner height="100" :data="resData" @click="swiperClick"></swiper-banner></view>
</template>

<script>
import swiperBanner from '@/components/wlp-swiper-banner/wlp-swiper-banner.vue';

export default {
	components: {
		swiperBanner
	},
	data() {
		return {
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
			]
		};
	},
	computed: {
		resData: function() {
			let obj = [];
			for (let item of this.data) {
				obj.push(item.imgUrl);
			}
			return obj;
		}
	},
	methods: {
		swiperClick: function(index) {
			console.log(this.data[index].link);
		}
	}
};
</script>

<style></style>
