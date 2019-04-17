<template>
	<view class="row">
		<block v-for="(item, index) in data" :key="index">
			<view class="col-xs-6">
				<view class="course-item">
					<view>
						<image class="course-img" :src="item.img"></image>
					</view>
					<view>
						<text class="course-title">{{ item.title }}</text>
					</view>
					<view>
						<text class="course-effect">{{ item.effect }}</text>
					</view>
					<view>
						<text class="course-name">{{ item.name }}</text>
					</view>
				</view>
			</view>
		</block>
	</view>
</template>

<script>
export default {
	components: {},
	data() {
		return {
			data: [
				{ img: '/static/img/课程图标封面-1@2x.png', title: '逻辑思维锻炼', effect: '提升思考的能力', name: '初级课程' },
				{ img: '/static/img/课程图标封面-1@2x.png', title: '逻辑思维锻炼', effect: '提升思考的能力', name: '初级课程' },
				{ img: '/static/img/课程图标封面-1@2x.png', title: '逻辑思维锻炼', effect: '提升思考的能力', name: '初级课程' },
				{ img: '/static/img/课程图标封面-1@2x.png', title: '逻辑思维锻炼', effect: '提升思考的能力', name: '初级课程' }
			]
		};
	},
	computed: {},
	methods: {}
};
</script>

<style lang="less">
*{
	box-sizing: border-box;
	font-family:Arial, Helvetica, sans-serif;
}
.row{
	display: flex;
	flex-wrap: wrap;
	padding: 12upx;
	background-color: rgb(248, 248, 248);
	.col-xs-6{
		width: 50%;
		
		padding: 12upx;
		.course-item{
			background-color: #fff;
			border-radius: 16upx;
			padding-bottom: 36upx;
			view{
				text-align: center;
				line-height: 72upx;
			}
			.course-img{
				width: 248upx;
				height: 248upx;
			}
			.course-title{
				font-size: 46upx;
				font-weight: 600;
			}
			.course-effect{
				font-size: 32upx;
				color:rgb(165, 165, 165);
			}
			.course-name{
				font-size: 24upx;
				border:2px solid rgb(255, 172, 109);
				border-radius: 32upx;
				padding: 10upx 20upx;
				color:rgb(255, 172, 109);
			}
		}
	}
}
</style>
