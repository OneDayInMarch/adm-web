<template>
    <body id="poster">
        <el-form class="login-container" label-position="left" label-width="0px">
            <h3 class="login_titile">系统登录</h3>
            <el-form-item>
                <el-input type="text" v-model="loginForm.username" auto-complete="off"
                placeholder="账号"></el-input>
            </el-form-item>
            <el-form-item>
                <el-input type="password" v-model="loginForm.password" auto-complete="off"
                placeholder="密码"></el-input>
            </el-form-item>
            <el-form-item style="width:100%">
                <el-button type="primary" style="width:100%;background:#505458;border:none" v-on:click="login">
                登录
                </el-button>
            </el-form-item>
        </el-form>
    </body>
</template>
<script>
    export default{
        name:'Login',
        data(){
            return {
                loginForm:{
                    username:'admin',//初始默认值
                    password:'123'
                },
                responseResult:[]
            }
        },
        methods:{
            // 修改登录逻辑：
            // 点击登按钮；后端获取user表信息返回前端；获取登录前页面的路径进行跳转，如果路径不存在则跳转到首页
            login(){
                var _this = this
                console.log(this.$store.state)
                this.$axios
                    .post('/login',{
                        username:this.loginForm.username,
                        password:this.loginForm.password
                    })
                    .then(successResponse=>{
                        if(successResponse.data.code === 200){
                            // this.$router.replace({path:'/index'})
                            _this.$store.commit('login', _this.loginForm)
                            var path = this.$route.query.redirect
                            this.$router.replace({path: path === '/' || path === undefined ? '/index' : path})
                        }
                    })
                    .catch(failResponse=>{
                        
                    })
            }
        }
    }
</script>
<style>
    body{
        margin: 0px;
    }
    .login-container{
        border-radius: 15px;
        background-clip: padding-box;
        margin:90px auto;
        width:350px;
        padding: 35px 35px 15px 35px;
        background:#fff;
        border:1px solid #eaeaea;
        box-shadow:0 0 25px #cac6c6;
    }
    .login_title{
        margin:0px auto 40px auto;
        text-align: center;
        color:#505458;
    }
</style>