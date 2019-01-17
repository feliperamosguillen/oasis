<template>
  <div class="solutions">
    <h2>NUESTRAS SOLUCIONES CLOUD</h2>
    <h3>Todas incluídas en OasisCom</h3>

    <div class="container-fluid">
      <div class="row">
        <div class="col-md-2 offset-md-1 mt-2">
          <img src="/src/assets/images/finanzas.png" alt="">
        </div>
        <div class="col-md-2 mt-2">
          <img src="/src/assets/images/logistica.png" alt="">
        </div>
        <div class="col-md-2 mt-2">
          <img src="/src/assets/images/factura-electronica.png" alt="">
        </div>
        <div class="col-md-2 mt-2">
          <img src="/src/assets/images/clientes.png" alt="">
        </div>
        <div class="col-md-2 mt-2">
          <img src="/src/assets/images/recursos-humanos.png" alt="">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
  },
  methods: {
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
  .solutions{
    width: 100%;
    text-align: center;
    margin-top: 3rem;
    margin-bottom: 6rem;

    & > h2{
      font-size: 20px;
      color: #1b1b1b;
      margin: 30px 0px 10px 0px;
      font-weight: bold;
    }

    & > h3{
      font-size: 20px;
      color: #6ca22b;
      margin: 0px 0px 30px 0px;
    }

    &__list {
      width: 100%;
    }
  }
</style>
