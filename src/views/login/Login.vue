<template>
  <div class="login">
    <HeaderLogin>
      <router-link slot="headleft" to="lotteryHall">
        <van-icon name="arrow-left"/>
      </router-link>
      <span slot="headtitle">用户登陆</span>
    </HeaderLogin>
    <div class="head-img">
      <img src="./images/defaultHead.png" alt="">
    </div>

    <div class="user-info">
      <div class="username">
        <i class="iconfont icon-wode"></i>
        <input placeholder="请输入账号" v-model="username">
        <!--<i class="end-icon"></i>-->
      </div>
      <div class="password">
        <i class="iconfont icon-Group"></i>
        <input placeholder="请输入密码" type="password" v-model="password">
        <!--<i class="end-icon"></i>-->
      </div>
    </div>
    <div class="buttons">
      <button class="login" @click="login">立即登录</button>
      <div class="otherBtn">
        <router-link to="register"><span class="reg">立即注册</span></router-link>
        <span style="color: #aaa">|</span>
        <router-link to="forgetpwd"><span class="forget">忘记密码</span></router-link>
      </div>
    </div>
  </div>
</template>

<script>
  import HeaderLogin from '@/components/Navbar.vue'
  import { Dialog } from 'vant';
  import { Base64 } from 'js-base64';
  import {setToken} from "../../utils/auth";
  import axios from 'axios'

  export default {
    name: 'Login',
    components: {
      HeaderLogin
    },
    data() {
      return {
        username: 'test',
        password: '222222',
        state: 0
      }
    },
    methods: {
    	getRebate(type) {
		    return this.axios.get(`/v1/Lottery/GetRebate?type=${type}`);
      },
    	computeRebase() {
		    axios.all([this.getRebate('k3'), this.getRebate('ssc'), this.getRebate('syx5'), this.getRebate('pk10')])
		    .then(axios.spread(function (k3, ssc, syxw, pk10) {
			    console.log('4个请求都完成了')
//			    setSscRebase(ssc)
//			    setK3Rebase(k3)
//			    setSyxwRebase(syxw)
//			    setPk10Rebase(pk10)
          this.state = 1
//			    this.$router.push('/lotteryHall')
		    }));
      },
      async login() {
    		if (this.state = 1) {
			    if(this.username == ''){
				    Dialog.alert({
					    title: '提示',
					    message: '请输入用户名'
				    })
			    } else if (this.password == '') {
				    Dialog.alert({
					    title: '提示',
					    message: '请输入用户名'
				    })
			    } else {
				    let res = await this.axios.post('/v1/Login', {
					    username: this.username,
					    password: this.password,
					    timestamp: parseInt(new Date().getTime() / 1000)
				    })
				    let str = `${res.data.data.client.id} ${res.data.data.access_token}`
				    setToken(Base64.encode(str))
				    if(res.data.message == 'success') {
				    	this.computeRebase()
				    } else {
					    Dialog.alert({
						    title: '提示',
						    message: res.data.message
					    })
				    }
			    }
        } else {
			    alert('还没准备好，请稍后')
		    }
      }
    },
    mounted() {
//    	this.computeRebase()
    }
  }
</script>

<style lang="scss" scoped>
  @import "../../styles/index.scss";
  @import "../../styles/mixin.scss";

  .head-img {
    margin-top: px2rem(150px);
    margin-bottom: px2rem(50px);
    height: px2rem(200px);
    text-align: center;
    img {
      border-radius: 50%;
      height: 100%;
      width: auto;
      border: 3px solid #e2e0e0;
    }
  }

  .user-info {
    background: #fff;
    @include onetoppx('.username');
    @include onetoppx('.password');
    @include onebottompx('.password');
    .username, .password {
      height: px2rem(82px);
      .front-icon, .end-icon {
        display: inline-block;
        float: left;
        width: px2rem(80px);
        height: px2rem(80px);
      }
      input {
        /*float: left;*/
        /*margin-left: px2rem(80px);*/
        border: 0;
        width: calc(100vw - 2.2rem);
        margin-top: px2rem(16px);
        font-size: px2rem(40px);
        &::-webkit-input-placeholder{
          color: #ccc;
        }
      }
      .end-icon {
        float: right;
      }
    }
    .iconfont {
      font-size: px2rem(40px);
      margin-left: px2rem(20px);
      margin-right: px2rem(20px);
      color: #999;
    }
  }

  .buttons {
    text-align: center;
    .login {
      margin-top: px2rem(30px);
      border: 0;
      background: #dc3b40;
      color: #fff;
      font-size: px2rem(40px);
      border-radius: 5px;
      width: px2rem(700px);
      height: px2rem(80px);
      &:active {
        background: #c71919;
      }
    }
    .otherBtn {
      margin-top: px2rem(20px);
      .reg, .forget {
        font-size: px2rem(30px);
        padding: 0 5px;
        color: #bbb;
      }
      .reg {
        color: #dc3b40;
      }
    }
  }

</style>
