<template>
  <div class="footer">
    <div class="container-fluid">
      <div class="row">
        <div class="col-sm-6 col-md-4 offset-md-1 text-center">
          <ul class="no-decoration">
            <li class="e-centered">
              Sitio OasisCom
            </li>
            <li class="e-centered">
              Cómo empezar en OasisCom <i class="zmdi zmdi-youtube-play zmdi-hc-2x icon-overgrren margin-top-a"/>
            </li>
            <li class="e-centered">
              Tutorial OasisU
            </li>
            <li class="e-centered">
              Capacitación OasisU <i class="zmdi zmdi-youtube-play zmdi-hc-2x icon-overgrren margin-top-a"/>
            </li>
          </ul>
        </div>
        <div class="col-sm-5 col-md-3  text-center">
          <ul class="no-decoration">
            <li class="e-centered">
              Política de privacidad
            </li>
            <li class="e-centered">
              Términos y condiciones
            </li>
            <li class="e-centered">
              Casos de éxito OasisCom <i class="zmdi zmdi-youtube-play zmdi-hc-2x icon-overgrren margin-top-a"/>
            </li>
          </ul>
        </div>
        <div class="col-sm-12 col-md-3 text-sm-right text-md-right auto-height">
          <div>
            <img src="/src/assets/custom-theme/images/logo-oasis.png" alt="OasisCom" width="220">
          </div>
          <div>V4.5</div>
          <div class="redes-lateral">
            <a class="circle-fb circle-gray"><i class="zmdi zmdi-facebook zmdi-hc-2x in-circle text-white"/></a>
            <a><i class="zmdi zmdi-twitter zmdi-hc-2x"/></a>
            <a><i class="zmdi zmdi-instagram zmdi-hc-2x"/></a>
            <a><i class="zmdi zmdi-youtube-play zmdi-hc-2x"/></a>
            <a class="circle-in circle-gray"><i class="zmdi zmdi-linkedin zmdi-hc-lg in-circle-linkedin text-white"/></a>
          </div>
        </div>
      </div>
    </div>
    <div class="line-green">
      OasisCom Cloud Solutions Versión 4.5 | Todos los derechos reservados © 2019
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
.footer{
    background-color: #f7f5f5;
    height: auto;
    color: #8a8a8a;
    padding-top: 3rem;

    @media (min-width: 768px){
      height: 255px;
    }
}
.no-decoration{
  list-style-type: none;
  text-align: left;
}
.margin-top-a{
  margin-left: 3px;
}
.e-centered{
  white-space: nowrap;
  padding-top: 0px;
  display: flex;
  justify-content: left;
  align-items: center;
  align-content: center;
  text-align: left;
}
.redes-lateral{
  color: #888888;
  width: 310px;
  right: 2px;
  width: 310px;
  right: 0;
  margin: 0;
  padding: 0;
  position: absolute;
  top: 40px;
  left: auto;
  right: -38px;
}
.circle-gray{
  background-color: #888888;
  color: white;
}
.auto-height{
  height: 148px;

  @media (min-width: 768px){
    height: auto;
  }
}
.line-green{
  background-color: #31db41;
  width: 100%;
  height: 80px;
  text-align: center;
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
}
</style>

