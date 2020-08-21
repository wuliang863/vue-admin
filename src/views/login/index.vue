<template>
  <div class="login-container">
    <div class="box"> 
      <img class="w" src="./y.webp" alt="">
      <img src="./bgi-rec.jpg" alt="">
      <img src="./bgi-ov2.png" alt="">

    </div>
    <el-form ref="loginForm" :model="loginForm" :rules="loginRules" class="login-form" auto-complete="on" label-position="left">

  

      <el-form-item prop="username">
        <span class="svg-container">
          <svg-icon icon-class="user" />
        </span>
        <el-input
          ref="username"
          v-model="loginForm.username"
          placeholder="Username"
          name="username"
          type="text"
          tabindex="1"
          auto-complete="on"
        />
      </el-form-item>

      <el-form-item prop="password">
        <span class="svg-container">
          <svg-icon icon-class="password" />
        </span>
        <el-input
          :key="passwordType"
          ref="password"
          v-model="loginForm.password"
          :type="passwordType"
          placeholder="Password"
          name="password"
          tabindex="2"
          auto-complete="on"
          @keyup.enter.native="handleLogin"
        />
        <span class="show-pwd" @click="showPwd">
          <svg-icon :icon-class="passwordType === 'password' ? 'eye' : 'eye-open'" />
        </span>
      </el-form-item>
      <img class="fang" src="./rec-blue.jpg" alt="">
      <img class="fang1" src="./rec-purple.jpg" alt="">
      <img class="wen" src="./智慧用电管理系统@2x.jpg" alt="">
      <span class="wen1">WELCOME_  Admin！</span>
      <span class="wen2">为你的用电保驾护航</span>
      <img class="yu" src="./忘记密码.jpg" alt="">
      <el-button :loading="loading" type="primary" style="width:40%;border-radius:33px;margin-bottom:20px; margin-top: 11px;margin-left: 60px;" @click.native.prevent="handleLogin" >登录</el-button>
      <img class="yu1" src="./oval-blue1.webp" alt="">
      <img class="yu2" src="./oval-purple10@2x.webp" alt="">
      <img class="fang2" src="./rec-yellow@2x.jpg" alt="">
      <img class="tu" src="./draw-main@2x.webp" alt="">
      <img class="tu1" src="./drawbg.webp" alt="">
      <img class="yu3" src="./bgi-ov@2x.webp" alt="">
      <div class="tips">
        <span style="margin-right:20px;">username: admin</span>
        <span> password: any</span>
      </div>

    </el-form>
  </div>
</template>

<script>
import { validUsername } from '@/utils/validate'

export default {
  name: 'Login',
  data() {
    const validateUsername = (rule, value, callback) => {
      if (!validUsername(value)) {
        callback(new Error('Please enter the correct user name'))
      } else {
        callback()
      }
    }
    const validatePassword = (rule, value, callback) => {
      if (value.length < 6) {
        callback(new Error('输入字母加数字大于6位'))
      } else {
        callback()
      }
    }
    return {
      loginForm: {
        username: 'admin',
        password: ''
      },
      loginRules: {
        username: [{ required: true, trigger: 'blur', validator: validateUsername }],
        password: [{ required: true, trigger: 'blur', validator: validatePassword }]
      },
      loading: false,
      passwordType: 'password',
      redirect: undefined
    }
  },

  watch: {
    $route: {
      handler: function(route) {
        this.redirect = route.query && route.query.redirect
      },
      immediate: true
    }
  },
  methods: {
    showPwd() {
      if (this.passwordType === 'password') {
        this.passwordType = ''
      } else {
        this.passwordType = 'password'
      }
      this.$nextTick(() => {
        this.$refs.password.focus()
      })
    },
    // fn(){
    //   var reg = /^[a-z][a-z]+\d+$/i
    //    if(reg.test(this.username)&&reg.test(this.password)){
    //     this.$toast({
    //          message: '登陆成功',
    //          icon:  'https://img.yzcdn.cn/vant/logo.png',
    //      });
          
    //    }else{
            
    //      this.$toast({
    //          message: '字母加数字',
    //          icon:  'https://img.yzcdn.cn/vant/logo.png',
    //      });
  
    //    }
    // },
    handleLogin() {
      if( this.loginForm.password){
   if(    /^(?![0-9]+$)(?!a-zA-Z+$)[0-9-Za-z]{6,16}$/.test( this.loginForm.password)){
    this.loadingtrue
  this.$store.dispatch('user/login', this.loginForm).then(() => {
            this.$router.push({ path: this.redirect || '/' })
            this.loading = false
          }).catch(() => {
            this.loading = false
          });
   }else{
     return false
   }
      }else{
        return false
      }
      console.log(this.$refs.loginForm)
  
        
        
        
      
    }
  }
}
</script>

<style lang="scss">
/* 修复input 背景不协调 和光标变色 */
/* Detail see https://github.com/PanJiaChen/vue-element-admin/pull/927 */

$bg:#283443;
$light_gray:#fff;
$cursor: #fff;

@supports (-webkit-mask: none) and (not (cater-color: $cursor)) {
  .login-container .el-input input {
    color: $cursor;
  }
}

/* reset element-ui css */
.login-container {
  .el-input {
    display: inline-block;
    height: 47px;
    width: 85%;

    input {
      background: transparent;
      border: 0px;
      -webkit-appearance: none;
      border-radius: 0px;
      padding: 12px 5px 12px 15px;
      color: $light_gray;
      height: 47px;
      caret-color: $cursor;

      &:-webkit-autofill {
        box-shadow: 0 0 0px 1000px $bg inset !important;
        -webkit-text-fill-color: $cursor !important;
      }
    }
  }

  .el-form-item {
    border: 1px solid rgba(255, 255, 255, 0.1);
    background: rgba(0, 0, 0, 0.1);
    border-radius: 5px;
    color: #454545;
  }
}
</style>

<style lang="scss" scoped>
$bg:#2d3a4b;
$dark_gray:#889aa4;
$light_gray:#eee;

.login-container {
  min-height: 100%;
  width: 100%;
  height: 100%;
  background-color: $bg;
  overflow: hidden;
  

  .login-form {
    position: relative;
    width: 80%;
    max-width: 100%;
    // height: 70%;
    padding: 160px 35px 0;
    margin: 100px auto;
    // overflow: hidden;
    background: white;
  }
  .w{
        width: 37%;
  }
  .fang{
    position: absolute;
    width: 15%;
    top: 0;
    left: 0;
    z-index: 10;
  }
  .fang1{
    width: 30%;

    position: absolute;
    top: 0;
    left: 0;
  }
   .fang2{
    position: absolute;
    width: 100px;
    height: 60px;
    bottom: 0;
    right: 0;
  }
   .yu{
     position: absolute;
    top: 74%;
    left: 43%
     
   }
  .yu1{
     position: absolute;
     left: -20px;
     z-index: 10;
  }
  .yu2{
     position: absolute;
     bottom: -40px;
     width: 8%;
     height:15%;
      left: 43%

  }
   .yu3{
     position: absolute;
     bottom: -8px;
     width: 2%;
     height:5%;
      left: 15%

  }
  .wen{
    width: 40%;
    height: 30px;
    position: absolute;
    top: 68px;
    left: 95px
  }
  .wen1{
    width: 35%;
    height: 30px;
    position: absolute;
    top: 105px;
    font-weight: 900;
    font-size: 20px;
    left: 95px
  }
    .wen2{
   width: 35%;
    height: 30px;
    position: absolute;
    top: 135px;
    font-size: 12px;
    left: 95px
  }
  .tu{
   position: absolute;
    right: 23px;
    top: 9px;
    width: 40%;
    height: 80%;
    z-index: 10;
  }
   .tu1{
       position: absolute;
    right: 21px;
    top: 18px;
    width: 48%;
    height: 82%;
  }

  .tips {
    font-size: 14px;
    color: #fff;
    margin-bottom: 10px;

    span {
      &:first-of-type {
        margin-right: 16px;
      }
    }
  }

  .svg-container {
    padding: 6px 5px 6px 15px;
    color: $dark_gray;
    vertical-align: middle;
    width: 30px;
    display: inline-block;
  }

  .title-container {
    position: relative;

    .title {
      font-size: 26px;
      color: $light_gray;
      margin: 0px auto 40px auto;
      text-align: center;
      font-weight: bold;
    }
  }

  .show-pwd {
    position: absolute;
    right: 10px;
    top: 7px;
    font-size: 16px;
    color: $dark_gray;
    cursor: pointer;
    user-select: none;
  }
}
.box{
  width:100%;
  height:100%;
  background-image: url('./login-bgi.jpg');
  position: absolute;
}

.box img:nth-child(2){
  width: 100%;
  // height: 100%;
  position: absolute;
  right: 0;
  width: 20%;
  height: 200px;
}
.box img:nth-child(3){

  position: absolute;
   left: 41%;
   top:74px;
 
}
.login-container .el-form-item{
  border-radius: 33px;
  width: 40%;
  margin-left: 60px;
}
// .el-input{
//   margin-top:-200px ;
// }

</style>
