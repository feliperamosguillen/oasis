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
          <div class="not-account">¿Tienes una cuenta?</div>
          <router-link to="/login">
            <el-button :loading="loading" class="bt-register" type="primary">INICIA SESIÓN</el-button>
          </router-link>
        </div>
      </div>

      <el-form ref="loginForm" :style="{ display: showLogin }" :model="loginForm" :rules="loginRules" class="login-form" auto-complete="on" label-position="left">
        <div class="title-container">
          <h3 class="title poppins-regular">
            Regístrate en OasisCom.
          </h3>
          <h5 class="subtitle">Llena los datalles abajo.</h5>
        </div>

        <label class="label-input">Correo eletrónico</label>
        <el-form-item prop="email">
          <span class="svg-container">
            <svg-icon icon-class="user" />
          </span>
          <el-input
            v-model="loginForm.email"
            placeholder="example@cloudcom.net"
            name="email"
            type="text"
            auto-complete="on"
          />
        </el-form-item>
        <label class="label-input">Nombre</label>
        <el-form-item prop="name">
          <el-input
            v-model="loginForm.name"
            placeholder="John Doe"
            name="name"
            type="text"
            auto-complete="on"
          />
        </el-form-item>
        <label class="label-input">Contraseña</label>
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
    </div>
    <Solutions />
    <Footer />
  </div>
</template>

<script>
import { validateEmail } from '@/utils/validate'
import LangSelect from '@/components/LangSelect'
import Solutions from '../login/solutions'
import Footer from '..//login/footer'

export default {
  name: 'Register',
  components: { LangSelect, Solutions, Footer },
  data() {
    const validEmail = (rule, value, callback) => {
      if (!validateEmail(value)) {
        callback(new Error('Por favor escribe un email correcto.'))
      } else {
        callback()
      }
    }

    const validName = (rule, value, callback) => {
      if (value.length < 6) {
        callback(new Error('Por favor escribe tu nombre correctamente.'))
      } else {
        callback()
      }
    }

    const validPassword = (rule, value, callback) => {
      if (value.length < 6) {
        callback(new Error('El password no puede ser menor de 6 digitos.'))
      } else {
        callback()
      }
    }
    return {
      loginForm: {
        name: '',
        email: '',
        password: ''
      },
      loginRules: {
        email: [{ required: true, trigger: 'blur', validator: validEmail }],
        name: [{ required: true, trigger: 'blur', validator: validName }],
        password: [{ required: true, trigger: 'blur', validator: validPassword }]
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
          alert('Usuario registrado correctamente.')
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    afterQRScan() {
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
  top: 128px;
  right: 2rem;
  width: 340px;
  display: block;
  text-align: right;

  @media (min-width: 475px){
    top: 35px;
  }

  @media (min-width: 660px){
    display: flex;
    justify-content: space-between;
    align-content: center;
    align-items: center;
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

.el-button.bt-green {
  min-width: 110px;
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
