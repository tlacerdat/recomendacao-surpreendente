<template>
  <div>
    <blueTrack position="upper" />
    <section id="bannerTelaEspera">
      <picture>
        <source
          media="(max-width: 767px)"
          :srcset="require('@/assets/img/banner-tela-de-espera_mobile.png')"
        />
        <source :srcset="require('@/assets/img/banner-tela-de-espera.png')" />
        <img
          :src="require('@/assets/img/banner-tela-de-espera.png')"
          alt="Banner"
          class="img-fluid"
        />
      </picture>

      <div class="wrap-container">
        <div class="container">
          <div class="inner">
            <titulo />

            <countdown :duration="20" />

            <h4 class="d-none d-md-block">
              Aguarde para <strong>esclarecer dúvidas</strong> de alguém que
              quer<br />
              comprar o mesmo <strong>produto Midea</strong> que você comprou.
            </h4>

            <h4 class="d-md-none">
              Aguarde para <strong>esclarecer dúvidas</strong> de alguém que
              quer comprar o mesmo <strong>produto Midea</strong> que você
              comprou.
            </h4>
          </div>
        </div>
      </div>
    </section>
    <blueTrack position="bottom" />
  </div>
</template>
<script>
import blueTrack from '@/components/_blueTrack'
import titulo from '@/components/_titulo'
import countdown from '@/components/_countdown'

export default {
  components: {
    blueTrack,
    titulo,
    countdown,
  },
}
</script>

<style lang="scss">
#bannerTelaEspera {
  position: relative;

  h4 {
    font-size: 2.5rem;
    margin-bottom: 0;

    strong {
      font-family: $fontb;
    }
  }

  img {
    display: block;
    min-width: 100%;
  }

  .container {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .inner {
    text-align: center;
    color: #fff;
  }
}

@media only screen and (max-width: 767px) {
  #bannerTelaEspera {
    h4 {
      font-size: 1.15rem;
    }
  }
}
</style>
