<template>
  <div class="forgot">
    <div class="forgot__container">
      <span class="forgot__title">
        Forgot your password?
      </span>
      <span class="forgot__subtitle">
        Enter your email address below and we'll get you back on track.
      </span>

      <form class="main-panel__form" action="/d/password/requestReset" method="post" novalidate="" __bizdiag="-1473824698" __biza="WJ__">
        <input type="hidden" name="submitted" value="true">
        <input type="hidden" name="redir" value="">
        <input type="hidden" name="formToken" value="HpSkyfAqxR6VIBIePZVV0Gwgv3MiuqriLQBPEtxkkDo">

        <div class="form__group">
          <label class="form__label" for="email">Email Address</label>
          <input type="text" required="" class="form__input cleanup validate-empty">

          <div class="alert alert-error alert-email" style="display: none;">Oops! Email is required.</div>
        </div>

        <footer class="text--center">
          <button type="submit" class="form__button">Request Reset Link</button>
          <div>
            <div>Back to sign in</div>
          </div>
        </footer>
      </form>

    </div>
  </div>
</template>
<script>
import LangSelect from '@/components/LangSelect'

export default {
  name: 'Forgot',
  components: { LangSelect },
  data() {
  },
  created() {
    // window.addEventListener('hashchange', this.afterQRScan)
  },
  destroyed() {
    // window.removeEventListener('hashchange', this.afterQRScan)
  },
  methods: {
  }
}
</script>

<style rel="stylesheet/scss" lang="scss">
.forgot{
  width: 100%;
  height: 95vh;
  display: flex;
  justify-content: center;
  align-content: center;
  align-items: center;

  &__container{
    width: 400px;
  }

  &__title{
    font-size: 28px;
    font-weight: 400;
    color: #434C5F;
    margin-bottom: 50px;
  }

  &__subtitle{
    display: block;
    margin-top: 10px;
    font-size: 16px;
    color: #596377;
  }
}

.form {
  position: relative;

  &__label {
    display: block;
    font-weight: 700;
    font-size: 11px;
    color: #434C5E;
    margin-bottom: 8px;
  }

  &__input {
    border: 1px solid #D4D9E2;
    border-radius: 3px;
    padding: 15px;
    font-size: 14px;
    color: #596377;
    outline: 0;
    -webkit-transition: border-color .2s ease;
    -o-transition: border-color .2s ease;
    transition: border-color .2s ease;
    height: 50px;
    display: block;
    width: 100%;
  }
}
</style>
