<template>
    <view class="swiper" :style="{ 'padding-bottom': height + '%' }">
		
        <swiper
            class="swiper__main"
            autoplay="true"
            circular="true"
            interval="5000"
            duration="500"
            indicator-dots="true"
            indicator-color="#ccc"
            indicator-active-color="#07bc91"
        >
            <block v-for="(item, index) in data" :key="index">
                <swiper-item class="swiper__cell" @tap="_click(index)">
                    <image class="swiper__img" :src="item" mode="aspectFill"></image>
                </swiper-item>
            </block>
        </swiper>
    </view>
</template>

<script>
export default {
    props: {
        data: {
            type: Array,
            default: function(e) {
                return [];
            }
        },
        height: { // 高宽百分比
            type: Number,
            default: function(e) {
                return 100;
            }
        }
    },
    methods: {
        _click: function(index) {
            this.$emit('click', index);
        },
    }
};
</script>

<style>
/* swiper宽高等比 */
.swiper{
    position: relative;
    width: 100%;
    padding-bottom: 66.67%;
}
.swiper__main{
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    width: 100%;
    height: 100%;
}
.swiper__cell,.swiper__img{
    width: 100%;
    height: 100%;
}
</style>
