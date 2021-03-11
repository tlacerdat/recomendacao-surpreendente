<template>
  <div>
    <blueTrack position="upper" />
    <section id="bannerChamada" class="perdida">
      <picture>
        <source
          media="(max-width: 767px)"
          :srcset="require('@/assets/img/banner-chamada-perdida_mobile.png')"
        />
        <source :srcset="require('@/assets/img/banner-chamada-perdida.png')" />
        <img
          :src="require('@/assets/img/banner-chamada-perdida.png')"
          alt="Banner"
          class="img-fluid"
        />
      </picture>

      <div class="wrap-container">
        <div class="container">
          <div class="inner">
            <img
              :src="require('@/assets/img/icon-sad-face.png')"
              alt="Sad face"
            />
            <h1 class="d-none d-md-block">
              Ops, alguém já <br />
              atendeu essa chamada.
            </h1>
            <h1 class="d-md-none">
              Ops, <br />
              alguém já atendeu<br />
              essa chamada.
            </h1>
            <h4 class="d-none d-md-block">
              Mas não se preocupe, você vai poder atender<br />
              outras chamadas em breve. <strong>Fique ligado!</strong>
            </h4>

            <h4 class="d-md-none">
              Mas não se preocupe, você vai poder atender outras chamadas em
              breve. <strong>Fique ligado!</strong>
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

export default {
  components: {
    blueTrack,
  },
}
</script>

<style lang="scss">
#bannerChamada {
  position: relative;

  h1 {
    font-family: $fontb;
    line-height: 1.1;
    font-size: 4.375rem;
    margin-bottom: 1.25rem;
  }

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

    img {
      width: 13rem;
      min-width: unset;
      margin: 0 auto 0.5rem auto;
    }
  }
}

@media only screen and (max-width: 767px) {
  #bannerChamada {
    h4 {
      font-size: 1.25rem;
    }

    h1 {
      font-size: 1.875rem;
    }

    .inner {
      img {
        width: 6.125rem;
      }
    }
  }
}
</style>
