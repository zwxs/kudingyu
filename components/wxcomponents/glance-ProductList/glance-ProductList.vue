<!-- glance 商品列表 -->
<template name="glanceProductList">
	<view class="glance-product-list">
		<!-- 商品列表 -->
		<view class="glance-products"  >
			<view style="width: 48%;" v-for="(item, index) in productlist" :key="index">
				<view class="glance-products-item" 	@click="onClick(item.imghref)">
					<!-- 商品图片 --> 
					<image style="width: 100%;height: 190px;" :src="item.src" mode="scaleToFill" @error="imgerr"></image>
					<!-- 短评 -->
					<view class="sigle-line-text shortlabel" v-if="item.shortlabel">{{item.shortlabel}}</view>
					<!-- 国家 原产地 -->
					<!-- <view></view> -->
					<!-- 营销标签 -->
					<view class="glance-products-item-marketinglabel">{{ item.marketinglabel}} </view>
					<!-- 品名 -->
					<view class="sigle-line-text" style="margin-top: 5px;font-size: 15px;">{{ item.name}}</view>
					<!-- 价格 -->
					<view style="height: 30px;margin-top: 5px;">
						<!-- 当前价 -->
						<text class="glance-products-item-curprice">{{ item.curprice}}</text>
						<!-- 原始价 -->
						<text v-if="item.oriprice" class="glance-products-item-oriprice">{{ item.oriprice}}</text>
					</view>
					<!-- 评论 -->
					<view class="glance-products-item-comment" >
						<!-- 头像 -->
						<image class="glance-products-item-comment-icon" :src="item.iconreviewer" mode="scaleToFill"></image>
						<!-- 评语 -->
						<view class="glance-products-item-comment-content">{{ item.comcontent}}</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			//img src
			data: Array,
			titletxt:{
				type:String
			}
		},
		data() {
			return {
				productlist:[]
			};
		},
		created: function() {
			var cnt = 0
			this.data && this.data.forEach((item, index) => {
				//数据校验？
				// data数据装载
				this.productlist.push(item);
			})
			// console.log(this.productlist)
		},
		methods: {
			onClick(imghref) {
				this.$emit('imgclick',imghref);
			},
			imgerr: function(e) {
				console.error('图片资源发生error事件，错误信息' + e.detail.errMsg);
			}		
		}
	}
</script>

<style lang="scss">
	// 产品列表
	.glance-product-list{
		width: 100%;
		// 间隔预留
		background-color: #ffffff;
	}
	// 产品列表标题
	.glance-product-list-title{
		height: 50px;
		font-size: 15px;
		line-height:50px; 
		text-align: center;
	}
	// 产品
	.glance-products{
		width: 100%;
		display: flex;
		display: -webkit-flex;
		flex-flow: row wrap;
		align-items: center ;
		justify-content:space-start;
	}
	
	// 产品项目
	.glance-products-item{
		margin: 0 0 20px 15px;
		display: flex;
		display: -webkit-flex;
		flex-flow: row wrap;
		align-items: center ;
		justify-content: flex-start;
		// 当前价
		&-curprice{
			color: #f40;float: left;font-size: 16px;
			margin-right: 10px;
		}
		// 原始价
		&-oriprice{
			font-size: 13px;color: #999999;
		}
		// 评论
		&-comment{
			padding: 3px;
			border-radius:20px;
			-moz-border-radius:20px;
			-webkit-border-radius:20px;
			// align-items: center; 
			background-color: #F8F8F8 ;
			// 评论头像
			&-icon{
				padding: 2px; 
				// margin-right: 10px;
				height: 25px;
				width: 25px;
				float: left;
				border-radius:15px;
				-moz-border-radius:15px;
				-webkit-border-radius:15px;
			}
			// 评论内容
			&-content{
				text-align: left; 
				overflow: hidden;
				text-overflow: ellipsis;
				display: -webkit-box;-webkit-line-clamp: 2;-webkit-box-orient: vertical; 
				color: #A8A8A8 ;
				font-size: 11px;
			}
		}
	}
	// 单行文本样式
	.sigle-line-text{
		width: 100%; 
		overflow: hidden;white-space: nowrap;text-overflow: ellipsis;
		text-align: left;
		// padding-left: 5px;
	}
	// 短评
	.shortlabel{
		background-color: #FDF5E6; height: 30px;line-height: 30px;color: #DAA520 ;font-size: 15px;
	}
</style>
