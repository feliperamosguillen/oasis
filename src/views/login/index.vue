<template>
  <div class="login-container">
    <div class="login-lateral">
      <div class="layer"/>
      <div class="contenido-lateral">
        <h4 class="poppins-semi-bold">OasisCom</h4>
        <h2 class="poppins-regular">Cloud Solutions</h2>
        <hr >
        <p>
          Tú te enfocas en CRECER, CLOUD SOLUTIONS administra la información.
        </p>
      </div>
      <div class="redes-lateral">
        <a class="circle-fb"><i class="zmdi zmdi-facebook zmdi-hc-2x in-circle"/></a>
        <a><i class="zmdi zmdi-twitter zmdi-hc-2x"/></a>
        <a><i class="zmdi zmdi-instagram zmdi-hc-2x"/></a>
        <a><i class="zmdi zmdi-youtube-play zmdi-hc-2x"/></a>
        <a class="circle-in"><i class="zmdi zmdi-linkedin zmdi-hc-lg in-circle-linkedin"/></a>
      </div>
    </div>
    <div class="login-content">
      <div class="header">
        <img src="/src/assets/custom-theme/images/logo-oasis.png" alt="OasisCom" >

        <div class="super-content">
          <div class="not-account">¿No tienes una cuenta?</div>
          <router-link to="/register">
            <el-button :loading="loading" class="bt-register" type="primary" >REGISTRATE</el-button>
          </router-link>
        </div>
      </div>

      <el-form ref="loginForm" :style="{ display: showLogin }" :model="loginForm" :rules="loginRules" class="login-form" auto-complete="on" label-position="left">
        <div class="title-container">
          <h3 class="title poppins-regular">{{ $t('login.title') }}</h3>
          <!--<lang-select class="set-language"/>-->
          <h5 class="subtitle">{{ $t('login.subtitle') }}</h5>
        </div>
        <label class="label-input">{{ $t('login.username') }}</label>
        <el-form-item prop="username">
          <span class="svg-container">
            <svg-icon icon-class="user" />
          </span>
          <el-input
            v-model="loginForm.username"
            :placeholder="$t('login.username')"
            name="username"
            type="text"
            auto-complete="on"
          />
        </el-form-item>
        <div class="password-head">
          <label class="label-input">{{ $t('login.password') }}</label>
          <div class="forgot">
            {{ $t('login.forgot') }}
          </div>
        </div>
        <el-form-item prop="password">
          <span class="svg-container">
            <svg-icon icon-class="password" />
          </span>
          <el-input
            :type="passwordType"
            v-model="loginForm.password"
            :placeholder="$t('login.password')"
            name="password"
            auto-complete="on"
            @keyup.enter.native="handleLogin" />
          <span class="show-pwd" @click="showPwd">
            <svg-icon icon-class="eye" />
          </span>
        </el-form-item>

        <el-button :loading="loading" class="bt-green" type="primary" @click.native.prevent="handleLogin">{{ $t('login.logIn') }}</el-button>

        <div style="position:relative" class="alternative-login">
          {{ $t('login.alternativeLogin') }}
          <br >
          <a><i class="zmdi zmdi-facebook-box zmdi-hc-2x icon-overgrren"/></a>
          <a><i class="zmdi zmdi-windows zmdi-hc-2x icon-overgrren"/></a>
          <!--
          <br >
          <el-button class="thirdparty-button" type="primary" @click="showLogin='none';showRegistration='block'">{{ $t('login.createAccount') }}</el-button>
          -->
        </div>

        <div class="registration"/>
      </el-form>

      <el-form ref="registrationForm" :style="{ display: showRegistration }" class="login-form" auto-complete="on" label-position="left">
        <div class="title-container">
          <h3 class="title poppins-regular">{{ $t('login.regtitle') }}</h3>
          <lang-select class="set-language"/>
          <h5 class="subtitle">{{ $t('login.subtitle') }}</h5>
        </div>
        <label class="label-input">{{ $t('login.username') }}</label>

        <el-form-item prop="username">
          <el-input
            v-model="loginForm.username"
            :placeholder="$t('login.username')"
            name="username"
            type="text"
            auto-complete="on"
          />
        </el-form-item>
        <div class="password-head">
          <label class="label-input">{{ $t('login.password') }}</label>
          <div class="forgot" @click.native.prevent="handleForgot">
            {{ $t('login.forgot') }}
          </div>
        </div>

        <el-form-item prop="password">
          <el-input
            :type="passwordType"
            v-model="loginForm.password"
            :placeholder="$t('login.password')"
            name="password"
            auto-complete="on"
            @keyup.enter.native="handleLogin" />
        </el-form-item>

        <el-button :loading="loading" class="bt-green" type="primary" @click.native.prevent="handleLogin">{{ $t('login.logIn') }}</el-button>

        <div style="position:relative; display: none;" class="forgot">
          {{ $t('login.forgot') }}
        </div>

        <div style="position:relative" class="alternative-login">
          {{ $t('login.alternativeLogin') }}
          <br >
          <a><i class="zmdi zmdi-facebook-box zmdi-hc-2x"/></a>
          <a><i class="zmdi zmdi-windows zmdi-hc-2x"/></a>
          <!--
          <br >
          <el-button class="thirdparty-button" type="primary" @click="showLogin='block';showRegistration='none'">{{ $t('login.createAccount') }}</el-button>
          -->
        </div>

        <div class="registration"/>
      </el-form>
    </div>

    <Solutions />
    <Footer />
  </div>
</template>

<script>
import { isvalidUsername } from '@/utils/validate'
import LangSelect from '@/components/LangSelect'
import SocialSign from './socialsignin'
import Solutions from './solutions'
import Footer from './footer'

export default {
  name: 'Login',
  components: { LangSelect, SocialSign, Solutions, Footer },
  data() {
    const validateUsername = (rule, value, callback) => {
      if (!isvalidUsername(value)) {
        callback(new Error('Por favor escribe un nombre de usuario correcto.'))
      } else {
        callback()
      }
    }
    const validatePassword = (rule, value, callback) => {
      if (value.length < 6) {
        callback(new Error('El password no puede ser menor a 6 digitos.'))
      } else {
        callback()
      }
    }
    return {
      loginForm: {
        username: 'admin',
        password: '1111111'
      },
      loginRules: {
        username: [{ required: true, trigger: 'blur', validator: validateUsername }],
        password: [{ required: true, trigger: 'blur', validator: validatePassword }]
      },
      passwordType: 'password',
      loading: false,
      showDialog: false,
      redirect: undefined,
      showLogin: 'block',
      showRegistration: 'none'
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
  created() {
    // window.addEventListener('hashchange', this.afterQRScan)
  },
  destroyed() {
    // window.removeEventListener('hashchange', this.afterQRScan)
  },
  methods: {
    showPwd() {
      if (this.passwordType === 'password') {
        this.passwordType = ''
      } else {
        this.passwordType = 'password'
      }
    },
    handleLogin() {
      this.$refs.loginForm.validate(valid => {
        if (valid) {
          this.loading = true
          this.$store.dispatch('LoginByUsername', this.loginForm).then(() => {
            this.loading = false
            this.$router.push({ path: this.redirect || '/' })
          }).catch(() => {
            this.loading = false
          })
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    afterQRScan() {
      // const hash = window.location.hash.slice(1)
      // const hashObj = getQueryObject(hash)
      // const originUrl = window.location.origin
      // history.replaceState({}, '', originUrl)
      // const codeMap = {
      //   wechat: 'code',
      //   tencent: 'code'
      // }
      // const codeName = hashObj[codeMap[this.auth_type]]
      // if (!codeName) {
      //   alert('第三方登录失败')
      // } else {
      //   this.$store.dispatch('LoginByThirdparty', codeName).then(() => {
      //     this.$router.push({ path: '/' })
      //   })
      // }
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss">
.forgot{
  cursor: pointer;
}

.super-content{
  position: absolute;
  top: 35px;
  right: 2rem;
  display: flex;
  justify-content: flex-end;
  width: 340px;
  align-content: center;
  align-items: center;

  @media (min-width: 666px){
    justify-content: space-between;
  }
}

.not-account{
  font-size: 16px;
  color: #7c7c7c;
  font-weight: normal;
  display: none;

  @media (min-width: 660px){
    display: block;
  }
}

.header {
  position: relative;
}

.login-lateral{
    display: none !important;
    @media (min-width:990px){
        display: inline-block !important;
    }
}

.login-container .login-content{
  width: 100%;

  @media (min-width:990px){
    width: 69%;
  }
}

.icon-overgrren{
  color:black;
  transition: 0.5s all ease;

  &:hover{
    color: #6ca22b;
    transition: 0.5s all ease;
  }
}

.button.el-button.bt-green{
  transition: 0.5s all ease;
}

.circle-fb{
  width: 40px;
  height: 40px;
  background-color: #ffffff;
  border-radius: 30px;
  padding: 0px 13px 4px 13px;
}

.circle-in{
  width: 40px;
  height: 40px;
  background-color: #ffffff;
  border-radius: 30px;
  padding: 19px 10px 7px 13px;
}

.redes-lateral {
  position: relative;
  width: 100%;
  height: 100%;
  color: #fff;
  /* padding: 5% 20% 0% 15%; */
  display: flex;
  top: 17%;
  justify-content: space-around;
  align-items: center;
  align-items: center;
  align-content: center;
  padding-left: 20px;
  padding-right: 20px;
}
.redes-lateral {
    position: relative;
    width: 100%;
    height: 100%;
    color: #fff;
    padding: 0;
    display: flex;
    top: 15%;
    padding-left: 20px;
    padding-right: 20px;
    transform: scale(0.7);
}
</style>
