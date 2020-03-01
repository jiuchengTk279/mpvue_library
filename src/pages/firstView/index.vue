<template>
    <div @change="handleChange" id="firstViewContainer" :indicator-dots="index !== 3" indicator-color="pink" indicator-active-color="green" circular="true" >
        <swiper>
            <swiper-item>
                <img src="/static/images/imgs/firstView/1.jpg" alt="" />
            </swiper-item>
            <swiper-item>
                <img src="/static/images/imgs/firstView/2.jpg" alt="" />
            </swiper-item>
            <swiper-item>
                <img src="/static/images/imgs/firstView/3.jpg" alt="" />
            </swiper-item>
            <swiper-item>
                <img src="/static/images/imgs/firstView/nvsheng.jpg" alt="" />
            </swiper-item>
        </swiper>
        <button @click="toIndex" class="btn" v-show="index === 3">开始体验</button>
    </div>
</template>

<script>
export default {
    data () {
        return {
            index: 0
        }
    },
    methods: {
        // 点击更新index
        handleChange (event) {
            // 更新 index 的状态值
            this.index = event.mp.detail.current
        },
        // 点击跳转
        toIndex () {
            // 跳转到 index 页面
            wx.navigateTo({
                url: '/pages/index/main'
            })
        }
    }
}
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
    #firstViewContainer
        width 100%
        height 100%
        swiper
            width 100%
            height 100%
            swiper-item
                width 100%
                height 100%
        .btn
            width 280rpx
            height 80rpx
            text-align center
            line-height 80rpx
            position absolute
            bottom 20rpx
            left 50%
            margin-left -140rpx
            background rgba(255,255,255,.5)
</style>