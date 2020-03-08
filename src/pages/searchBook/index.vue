<template>
    <div id="searchContainer">
        <div class="searchHeader">
            <input @confirm="handleSearch" confirm-type="搜索" type="text" v-model="searchContent" placeholder="书中自有黄金屋" placeholder-class="placeholder">
            <span @click="handleClear" class="clear" v-show="searchContent">X</span>
        </div>
        <div v-if="booksArr.length">
            <BooksList :booksArr="booksArr"></BooksList>
        </div>
    </div>
</template>

<script>
import BooksList from '../booksList/index'
import request from '../../utils/request.js'
export default {
    data () {
        return {
            searchContent: '',
            booksArr: []
        }
    },
    components: {
        BooksList
    },
    methods: {
        // 清空输入的内容
        handleClear () {
            this.searchContent = ''
            this.booksArr = []
        },
        // 点击进行搜索
        async handleSearch () {
            // 获取用户输入的内容
            let data = {req: this.searchContent}
            // 发起请求给服务器获取数据
            // wx.request({
            //     url: 'http://localhost:3000/searchBooks',
            //     data,
            //     success: (res) => {
            //         this.booksArr = res.data
            //     }
            // })
            // 调用 request 方法后返回值为 promise 对象， 所以可以用 async和 await
            let result = await request('/searchBooks', data)
            // console.log(result, '返回的数据')
            this.booksArr = result
        }
    }
}
</script>

<style lang="stylus" scoped>
    #searchContainer
        .searchHeader
            width 80%
            height 80rpx
            margin auto
            border-bottom 1rpx solid #02a774
            position relative
            input
                width 100%
                height 100%
                .placeholder
                    color #02a774
                    text-align center
                    font-size 28rpx
            .clear
                position absolute
                top 20rpx
                right 20rpx
                z-index 99
</style>