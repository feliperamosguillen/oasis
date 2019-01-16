<template>
  <div :class="classObj" class="app-wrapper">
    <div v-if="device==='mobile'&&sidebar.opened" class="drawer-bg" @click="handleClickOutside"/>
    <sidebar class="sidebar-container"/>
    <div class="main-container">
      <navbar/>
      <tags-view/>
      <app-main/>
    </div>
  </div>
</template>

<script>
import { Navbar, Sidebar, AppMain, TagsView } from './components'
import ResizeMixin from './mixin/ResizeHandler'

export default {
  name: 'Layout',
  components: {
    Navbar,
    Sidebar,
    AppMain,
    TagsView
  },
  mixins: [ResizeMixin],
  computed: {
    sidebar() {
      return this.$store.state.app.sidebar
    },
    device() {
      return this.$store.state.app.device
    },
    classObj() {
      return {
        hideSidebar: !this.sidebar.opened,
        openSidebar: this.sidebar.opened,
        withoutAnimation: this.sidebar.withoutAnimation,
        mobile: this.device === 'mobile'
      }
    }
  },
  methods: {
    handleClickOutside() {
      this.$store.dispatch('closeSideBar', { withoutAnimation: false })
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss">
  @import "~@/styles/mixin.scss";
  .app-wrapper {
    @include clearfix;
    position: relative;
    height: 100%;
    width: 100%;
    &.mobile.openSidebar{
      position: fixed;
      top: 0;
    }
  }
  .drawer-bg {
    background: #000;
    opacity: 0.3;
    width: 100%;
    top: 0;
    height: 100%;
    position: absolute;
    z-index: 999;
  }

  /*Página de Login*/
  $bg:#283443;
  $light_gray:#fff;
  $cursor: #1b1b1b;

  @supports (-webkit-mask: none) and (not (cater-color: $cursor)) {
    .login-container .el-input input{
      color: $cursor;
      background-color: $light_gray;
      border: solid 1px #7c7c7c!important;
      &::first-line {
        color: $cursor;
      }
    }
  }

  .alternative-login a {
    margin: 5px;
    margin-top: 10px;
    position: relative;
    top: 10px;
  }

  .color-green{
    color: #6ca22b;
  }

  button.el-button.bt-green{
    font-weight: bold; margin-bottom:30px; margin-left: 35%; border-radius: 50px; background-color: #6ca22b; border-color: #6ca22b; width: 35%;
  }

  button.el-button.bt-green:hover{
    opacity: 0.55;
  }

  /* reset element-ui css */
  .login-container {
    .el-input {
      display: inline-block;
      height: 47px;
      width: 100%;
      input {
        background: $light_gray;
        border: 0px;
        -webkit-appearance: none;
        border-radius: 0px;
        padding: 12px 5px 12px 15px;
        color: $cursor;
        height: 47px;
        caret-color: $cursor;
        &:-webkit-autofill {
          -webkit-box-shadow: 0 0 0px 1000px $bg inset !important;
          -webkit-text-fill-color: $cursor !important;
        }
      }
    }
    .el-form-item {
      border: 1px solid rgba(255, 255, 255, 0.1);
      background: rgba(255, 255, 255, 1);
      border-radius: 5px;
      color: #p1p1p1;
    }
    .login-lateral{
      width: 30%;
      background-image: url('/src/assets/custom-theme/images/lateral-login.jpg');
      background-size: cover;
      background-repeat: no-repeat;
      background-position: 0px 0px;
      height: 100vh;
      display: inline-block;
      vertical-align: top;
      position: relative;
    }

    .login-lateral h4 {
      margin-bottom: 0.5em;
    }

    .login-lateral h2 {
      margin-top: 0em;
      margin-bottom: 0.5em;
    }

    .login-lateral hr {
      display: block;
      width: 25%;
      height: 1px;
      border: 0;
      border-top: 2px solid #6ca22b;
      margin: 1em 0;
      padding: 0;
    }

    .login-lateral .layer {
      background-color: rgba(48,114,164,0.9);
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
    }

    .contenido-lateral {
      width: 100%;
      height: 170px;
      position: relative;
      top: 55%;
      left: 0px;
      color: #fff;
      padding: 0% 30% 0% 15%;
    }

    .redes-lateral{
      position: relative;
      width: 100%;
      height: 100%;
      color: #fff;
      padding: 5% 30% 0% 15%;
      display: block;
      top: 55%;
    }

    .in-circle{
      color: #3f7eac;
      top: 4px;
      position: relative;
    }

    .in-circle-linkedin{
      color: #3f7eac;
      top: -10px;
      position: relative;
    }

    .circle{
      width: 40px;
      height: 40px;
      background-color: #ffffff;
      border-radius: 30px;
      padding: 15px 10px 0px 10px;
    }

    .redes-lateral a:not(:first-child){
      margin-left: 10px;
    }

    .login-content {
      display: inline-block;
      width: 69%;
      height: 100%;
      vertical-align: top;
      background-color: #ffffff!important;
      color: #1b1b1b!important;

      .header {
        padding: 35px 48px;
      }

      label.label-input{
        font-size: 14px;
      }
    }
  }

$bg:#ffffff;
$dark_gray:#ffffff;
$light_gray:#1b1b1b;

.login-container {
  min-height: 100%;
  width: 100%;
  background-color: $bg;
  overflow: hidden;
  .login-form {
    position: relative;
    width: 520px;
    max-width: 100%;
    padding: 50px 35px 0;
    margin: 0 auto;
    overflow: hidden;
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
    display: none;
  }
  .title-container {
    position: relative;
    .title {
      font-size: 28px;
      color: $light_gray;
      margin: 0px 0px 10px 0px;
      font-weight: bold;
    }
    .subtitle {
      font-size: 16px;
      color: #7c7c7c;
      margin: 0px 0px 30px 0px;
      font-weight: normal;
    }
    .set-language {
      color: #p1p1p1;
      position: absolute;
      top: 5px;
      right: 0px;
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
  .thirdparty-button {
    display: inline-block;
    right: 0;
    bottom: 6px;
  }
}

.forgot{
  color: #7c7c7c;
  text-align: center;
  margin-bottom: 1rem;
  display: inline-block;
  position: absolute;
  right: 35px;
  font-size: 12px;
}

.alternative-login{
  color: #1b1b1b;
  text-align: center;
  margin-bottom: 1rem;
}

.registration{
  color: #1b1b1b;
  text-align: center;
  margin-bottom: 1rem;
  margin-top: 1rem;
}

</style>
