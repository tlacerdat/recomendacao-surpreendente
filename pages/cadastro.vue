/* eslint-disable no-console */
<template>
  <div>
    <blueTrack position="upper" />
    <section id="banner">
      <picture>
        <source
          media="(max-width: 767px)"
          :srcset="require('@/assets/img/banner-cadastro_mobile.png')"
        />
        <source :srcset="require('@/assets/img/banner-cadastro.png')" />
        <img
          :src="require('@/assets/img/banner-cadastro.png')"
          alt="Banner"
          class="img-fluid"
        />
      </picture>

      <div class="wrap-container">
        <div class="container">
          <div class="inner">
            <h2>Participe do programa</h2>
            <titulo />
            <h2>
              e ganhe <strong>3 meses</strong> de
              <strong>garantia adicional.</strong>
            </h2>
          </div>
        </div>
      </div>
    </section>

    <section id="main">
      <div class="container">
        <h2>
          Você que possui um produto <strong class="blue">Midea</strong> pode
          fazer o cadastro abaixo e <strong>ajudar outra pessoa</strong> a tirar
          dúvidas sobre o seu produto Midea
          <strong>através das suas recomendações e experiência</strong> de uso.
        </h2>

        <h2>
          Você sai ganhando, as outras pessoas também. <br />
          <strong>É só se cadastrar:</strong>
        </h2>

        <div class="line">
          <div class="item imageCol">
            <picture>
              <source
                media="(max-width: 767px)"
                :srcset="require('@/assets/img/produtos_mobile.png')"
              />
              <source :srcset="require('@/assets/img/produtos.png')" />
              <img
                :src="require('@/assets/img/produtos.png')"
                alt="Banner"
                class="img-fluid"
              />
            </picture>
          </div>

          <div class="item formCol">
            <b-form @submit.prevent="onSubmit">
              <b-form-group
                label="Qual o seu Produto Midea:"
                label-for="nomeProduto"
              >
                <b-form-input
                  id="nomeProduto"
                  v-model="form.nomeProduto"
                  required
                  placeholder="Nome do Produto"
                ></b-form-input>
              </b-form-group>

              <b-form-group label="Onde comprou:" label-for="ondeComprou">
                <b-form-input
                  id="ondeComprou"
                  v-model="form.ondeComprou"
                  required
                ></b-form-input>
              </b-form-group>

              <b-form-group label="Número da Nota Fiscal:" label-for="numeroNf">
                <b-form-input
                  id="numeroNf"
                  v-model="form.numeroNf"
                  type="tel"
                  required
                ></b-form-input>
              </b-form-group>

              <b-form-group label="Nome:" label-for="nome">
                <b-form-input
                  id="nome"
                  v-model="form.nome"
                  required
                ></b-form-input>
              </b-form-group>

              <b-form-group
                label="Telefone Celular:"
                label-for="telefoneCelular"
              >
                <b-form-input
                  id="telefoneCelular"
                  v-model="form.telefoneCelular"
                  v-mask="['(##) #####-####']"
                  type="tel"
                  required
                ></b-form-input>
              </b-form-group>

              <b-form-group label="E-mail:" label-for="emailInput">
                <b-form-input
                  id="emailInput"
                  v-model="form.email"
                  type="email"
                  required
                ></b-form-input>
              </b-form-group>

              <b-form-group label="CEP:" label-for="cep">
                <b-form-input
                  id="cep"
                  v-model="form.cep"
                  v-mask="['#####-###']"
                  type="tel"
                  required
                ></b-form-input>
              </b-form-group>

              <b-form-group>
                <b-form-checkbox-group v-model="form.checked">
                  <b-form-checkbox value="Aceito ser avisado"
                    >Quero ser avisado para <br />
                    ganhar 3 meses de garantia</b-form-checkbox
                  >
                </b-form-checkbox-group>
              </b-form-group>

              <div class="button">
                <b-button type="submit" variant="azul"
                  >Quero ser Recomendador Midea</b-button
                >
              </div>
            </b-form>
          </div>
        </div>

        <div class="bottom">
          <h2>
            Em breve, você receberá um chamado para
            <strong>atender as dúvidas</strong> de alguém que também quer um
            produto Midea. Nessas horas, <strong>toda ajuda é válida</strong> e
            você vai ter a chance de oferecer uma
            <strong>experiência surpreendente</strong>. Até logo!
          </h2>
        </div>
      </div>

      <div class="underbg"></div>
    </section>
    <blueTrack position="bottom" />
  </div>
</template>
<script>
import blueTrack from '@/components/_blueTrack'
import titulo from '@/components/_titulo'
import { mask } from 'vue-the-mask'
import axios from 'axios'

export default {
  directives: {
    mask,
  },
  components: {
    blueTrack,
    titulo,
  },
  data() {
    return {
      form: {
        nomeProduto: '',
        ondeComprou: '',
        numeroNf: '',
        nome: '',
        telefoneCelular: '',
        email: '',
        cep: '',
        checked: [],
        utm_campaign: '',
        utm_source: '',
        utm_medium: '',
        utm_content: '',
      },
    }
  },
  mounted() {
    function getCookie(cname) {
      const name = cname + '='
      const decodedCookie = decodeURIComponent(document.cookie)
      const ca = decodedCookie.split(';')
      for (let i = 0; i < ca.length; i++) {
        let c = ca[i]
        while (c.charAt(0) === ' ') {
          c = c.substring(1)
        }
        if (c.indexOf(name) === 0) {
          return c.substring(name.length, c.length)
        }
      }
      return ''
    }

    function setCookie(cname, cvalue, exdays) {
      const d = new Date()
      d.setTime(d.getTime() + exdays * 24 * 60 * 60 * 1000)
      const expires = 'expires=' + d.toUTCString()
      document.cookie = cname + '=' + cvalue + ';' + expires + ';path=/'
    }

    function getUrlParameter(name) {
      name = name.replace(/[[]/, '\\[').replace(/[\]]/, '\\]')
      const regex = new RegExp('[\\?&]' + name + '=([^&#]*)')
      const results = regex.exec(location.search)
      return results === null
        ? ''
        : decodeURIComponent(results[1].replace(/\+/g, ' '))
    }

    if (getUrlParameter('utm_campaign').length > 0)
      setCookie('utm_campaign', getUrlParameter('utm_campaign'), 30)
    if (getUrlParameter('utm_source').length > 0)
      setCookie('utm_source', getUrlParameter('utm_source'), 30)
    if (getUrlParameter('utm_medium').length > 0)
      setCookie('utm_medium', getUrlParameter('utm_medium'), 30)
    if (getUrlParameter('utm_content').length > 0)
      setCookie('utm_content', getUrlParameter('utm_content'), 30)

    this.form.utm_campaign = getCookie('utm_campaign')
    this.form.utm_source = getCookie('utm_source')
    this.form.utm_medium = getCookie('utm_medium')
    this.form.utm_content = getCookie('utm_content')
  },
  methods: {
    async onSubmit(event) {
      event.preventDefault()
      const btn = event.target.querySelector('button[type=submit]')
      btn.disabled = true
      btn.innerHTML = '<div class="loader"></div>'

      const myForm = new FormData()
      for (const key in this.form) {
        myForm.append(key, this.form[key])
      }

      try {
        const sendData = await axios.post(
          'https://apps.l0gik.com.br/midea/integracao/recomendacao-surpreendente.php',
          myForm,
          {
            headers: { 'Content-Type': 'multipart/form-data' },
          }
        )

        if (sendData.status !== 200)
          throw new Error('HTTP error ' + sendData.status)

        btn.innerHTML = 'CADASTRO ENVIADO!'
      } catch (error) {
        // eslint-disable-next-line no-console
        console.error(error)
        btn.classList.add('btn-danger')
        btn.innerHTML = 'Erro'
      }
    },
  },
}
</script>
<style lang="scss">
#banner {
  position: relative;
  color: #fff;
  img {
    display: block;
    min-width: 100%;
  }

  h2 {
    margin-bottom: 0;
    font-size: 2.188rem;
    padding-left: 0.3rem;

    strong {
      font-family: $fontb;
    }
  }

  .inner {
    padding-top: 8rem;
    padding-left: 1rem;
  }
}

#main {
  position: relative;
  text-align: center;
  padding: 4.5rem 0 8rem 0;

  .underbg {
    background-color: #ebebeb;
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 24%;
    z-index: -1;
  }

  .line {
    display: flex;
    padding: 4rem 0 7rem 0;
  }

  .item {
    width: 50%;
  }

  .form-group {
    margin-bottom: 2.5rem;
  }

  .imageCol {
    position: relative;
    height: inherit;

    img {
      position: absolute;
      height: 104%;
      max-width: unset;
      left: -69%;
      top: 1%;
    }
  }

  form {
    width: 100%;
    margin-left: auto;
  }

  label {
    cursor: pointer;
    font-size: 2.188rem;
    font-family: $fontmd;
    margin-bottom: 1.25rem;
  }

  input {
    height: 4.5rem;
    background-color: #ebebeb;
    border-radius: 3.125rem;
    border: none;
    text-align: center;
    font-size: 1.8rem;
    padding-left: 1.5rem;
    padding-right: 1.5rem;
  }

  h2 {
    font-size: 2.5rem;
    margin-bottom: 2.5rem;

    strong {
      font-family: $fontb;

      &.blue {
        color: $blue;
      }
    }
  }

  .bottom {
    h2 {
      margin-bottom: 0;
    }
  }

  .custom-control-label::before {
    border-radius: 50% !important;
    background-color: #ebebeb;
    border: #ebebeb solid 1px;
  }

  input:checked ~ label:after {
    border-radius: 50% !important;
    background-color: $blue;
    border: $blue solid 1px;
  }

  .custom-control-label::before,
  .custom-control-label::after {
    width: 1.25rem;
    height: 1.25rem;
    left: -2.5rem;
    top: unset;
  }

  .custom-checkbox {
    label {
      display: flex;
      align-items: center;
      text-align: left;
      line-height: 1.15;
      font-size: 1.8rem;
      margin-bottom: 0;
    }

    input {
      height: unset;
    }
  }

  .button {
    padding-top: 3.5rem;
  }
}

@media only screen and (max-width: 1699px) {
  #main .imageCol img {
    left: -55%;
  }
}

@media only screen and (max-width: 1599px) {
  #main .imageCol img {
    left: -49%;
  }
}

@media only screen and (max-width: 1499px) {
  #main .imageCol img {
    left: -37%;
  }
}

@media only screen and (max-width: 1399px) {
  #main .imageCol img {
    left: -34.5%;
  }
}

@media only screen and (max-width: 1199px) {
  #main .imageCol img {
    left: -44%;
  }
}

@media only screen and (max-width: 1099px) {
  #main .imageCol img {
    left: -34%;
  }
}

@media only screen and (max-width: 767px) {
  #banner {
    h2 {
      font-size: 0.875rem;
      padding-left: 0.1rem;
      margin-bottom: 0.15rem;
    }

    .inner {
      padding-top: 2.5rem;
    }
  }

  #main {
    padding: 2.5rem 0 5rem 0;
    .line {
      flex-wrap: wrap;
      padding: 0.75rem 0 1rem 0;
    }

    .item {
      width: 100%;
    }

    .formCol {
      order: 1;
    }

    .imageCol {
      order: 2;
      img {
        position: static;
        max-width: 100%;
        height: auto;
      }
    }

    .form-group {
      margin-bottom: 1.75rem;
    }

    label {
      font-size: 1.063rem;
      margin-bottom: 0.75rem;
    }

    .custom-checkbox {
      label {
        font-size: 0.945rem;
      }
    }

    .custom-control-inline {
      margin-right: 0;
    }

    input {
      font-size: 0.945rem;
      height: 2.6rem;
    }

    h2 {
      font-size: 1.063rem;
      margin-bottom: 1.5rem;

      br {
        display: none;
      }
    }

    .custom-control-label::before,
    .custom-control-label::after {
      width: 0.85rem;
      height: 0.85rem;
      left: -1.5rem;
    }

    .button {
      padding-top: 1rem;
      padding-bottom: 2rem;
    }

    .underbg {
      height: 19.5%;
    }
  }
}
</style>
