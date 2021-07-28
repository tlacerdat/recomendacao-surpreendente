<template>
  <h1 id="title">
    Recomendaçã <br />Surpreendente
    <img :src="require('@/assets/img/likes-amei.png')" alt="Likes e amei" />
  </h1>
</template>
<style lang="scss" scoped>
h1#title {
  display: inline-block;
  font-size: 3.7rem;
  font-family: $fontb;
  color: #fff;
  position: relative;
  line-height: 0.9;
  margin-bottom: 0.75rem;
  text-align: left;

  img {
    position: absolute;
    top: -5.95rem;
    right: -5rem;
    width: 6.25rem;
    min-width: unset !important;
  }
}

@media only screen and (max-width: 767px) {
  h1#title {
    font-size: 2rem;
    line-height: 0.95;
    margin-bottom: 0.5rem;

    img {
      width: 3.125rem;
      top: -2.825rem;
      right: -2.5rem;
    }
  }
}
</style>
