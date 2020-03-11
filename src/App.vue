<script>
import request from './utils/request.js'
export default {
    mounted () {
        wx.login({
            success: async (res) => {
                // 1. 获取用户登录的临时凭证，和用户是否授权没有直接关系，会变换的，有效时长： 有效期为五分钟
                let code = res.code
                console.log(code)

                // 2. 发送 code 给服务器
                let result = await request('/getOpenId', {code})

                // 3. 将自定义登录状态缓存到storage中
                wx.setStorageSync('token', token);
            }
        })

        // 测试地址token
        let result = await request('/test');
        console.log('验证结果', result);
    }
}
</script>

<style lang="wxss">
    page {
        width: 100% !important;
        height: 100% !important;
    }
        
</style>
