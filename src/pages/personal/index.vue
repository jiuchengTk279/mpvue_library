<template>
    <div id="personContainer">
        <div class="header">
            <img :src="userInfo.avatarUrl ? userInfo.avatarUrl : '/static/images/imgs/personal/personal.png'" alt="" />
            <button open-type="getUserInfo" @getuserinfo="handleGetUserInfo">{{ userInfo.nickName ? userInfo.nickName : '登录'}}</button>
        </div>
        <div class="cardList">
            <div class="card" @click="handleScan">
                <span>扫码看书</span>
                <span class="more"> > </span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            userInfo: {}
        }
    },
    methods: {
        // 点击获取用户信息
        handleGetUserInfo (res) {
            console.log(res)
            if (res.mp.detail.userInfo) {
                this.userInfo = res.mp.detail.userInfo
            }
        },
        // 点击获取扫码信息
        handleScan () {
            wx.scanCode({
                success: (res) => {
                    console.log(res)
                }
            })
        }
    },
    mounted () {
        wx.getUserInfo({
            success: (res) => {
                // 更新 userInfo 的状态数据
                this.userInfo = res.userInfo
            },
            fail: () => {
                console.log('获取失败')
            }
        })
    }
}
</script>

<style lang="stylus" scoped>
    #personContainer
        .header
            padding 40rpx
            background #02a774
            img
                width 100rpx
                height 100rpx
                vertical-align middle
            button
                display inline-block
                height 80rpx
                line-height 80rpx
                background rgba(255,255,255,0.5)
                vertical-align middle
                margin-left 40rpx
                max-width 200rpx
        .cardList
            .card
                width 94%
                height 60rpx
                line-height 60rpx
                margin 10rpx auto
                border 1rpx solid #eee
                padding 10rpx
                .more
                    float right
</style>
