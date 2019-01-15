<template>
  <div class="login-container">
    <div class="login-lateral">
      <div class="layer"/>
      <div class="contenido-lateral">
        <h4>OasisCom</h4>
        <h2>Cloud Solutions</h2>
        <hr >
        <p>
          Tú te enfocas en CRECER, CLOUD SOLUTIONS administra la información.
        </p>
      </div>
    </div>
    <div class="login-content">
      <div class="header">
        <img src="/src/assets/custom-theme/images/logo-oasis.png" alt="OasisCom" >
      </div>
      <el-form ref="loginForm" :style="{ display: showLogin }" :model="loginForm" :rules="loginRules" class="login-form" auto-complete="on" label-position="left">
        <div class="title-container">
          <h3 class="title">{{ $t('login.title') }}</h3>
          <lang-select class="set-language"/>
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
          <a><img src="/src/assets/custom-theme/images/ico-fb.png" alt="Facebook"></a>
          <a><img src="/src/assets/custom-theme/images/ico-win.png" alt="Windows"></a>
          <br >
          <el-button class="thirdparty-button" type="primary" @click="showLogin='none';showRegistration='block'">{{ $t('login.createAccount') }}</el-button>
        </div>

        <div class="registration"/>
      </el-form>

      <el-form ref="registrationForm" :style="{ display: showRegistration }" :model="registrationForm" :rules="loginRules" class="login-form" auto-complete="on" label-position="left">
        <div class="title-container">
          <h3 class="title">{{ $t('login.regtitle') }}</h3>
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
          <div class="forgot">
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
          <a><img src="/src/assets/custom-theme/images/ico-fb.png" alt="Facebook"></a>
          <a><img src="/src/assets/custom-theme/images/ico-win.png" alt="Windows"></a>
          <br >
          <el-button class="thirdparty-button" type="primary" @click="showLogin='block';showRegistration='none'">{{ $t('login.createAccount') }}</el-button>
        </div>

        <div class="registration"/>
      </el-form>
    </div>
  </div>
</template>

<script>
import { isvalidUsername } from '@/utils/validate'
import LangSelect from '@/components/LangSelect'
import SocialSign from './socialsignin'

export default {
  name: 'Login',
  components: { LangSelect, SocialSign },
  data() {
    const validateUsername = (rule, value, callback) => {
      if (!isvalidUsername(value)) {
        callback(new Error('Please enter the correct user name'))
      } else {
        callback()
      }
    }
    const validatePassword = (rule, value, callback) => {
      if (value.length < 6) {
        callback(new Error('The password can not be less than 6 digits'))
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

</style>
