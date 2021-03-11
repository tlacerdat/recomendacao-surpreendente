<template>
  <div class="blueTrack" :class="position">
    <template v-if="position === 'upper'">
      <img
        :src="require('@/assets/img/midea-logo-topo.png')"
        alt="Logo Midea"
      />
    </template>
    <template v-else>
      <img
        :src="require('@/assets/img/midea-logo-footer.png')"
        alt="Logo Midea"
      />
    </template>
  </div>
</template>
<script>
export default {
  props: {
    position: {
      type: String,
      default: '',
    },
  },
}
</script>
<style lang="scss" scoped>
.blueTrack {
  background-color: $blue;
  text-align: center;

  &.upper {
    padding: 1.2rem 0;
    img {
      width: 7rem;
    }
  }

  &.bottom {
    padding: 1.75rem 0;
    img {
      width: 12.625rem;
    }
  }
}

@media only screen and (max-width: 767px) {
  .blueTrack {
    &.upper {
      padding: 0.75rem 0;
      img {
        width: 3.5rem;
      }
    }

    &.bottom {
      padding: 1.1rem 0;
      img {
        width: 6.313rem;
      }
    }
  }
}
</style>
