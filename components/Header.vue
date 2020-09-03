<template>
  <header class="container px-0">
    <nav
      class="navbar navbar-expand-sm justify-content-center justify-content-sm-end"
    >
      <nuxt-link :to="localePath('index')" class="text-dark"
        ><img
          class="navbar-brand"
          src="../static/logo_horizontal.svg"
          width="200"
          height="70"
          alt="Vot Romania" />
        by
        <img
          class="navbar-brand"
          src="../static/code4Romania.svg"
          width="100"
          alt="Vot Romania"
      /></nuxt-link>
      <div class="d-flex align-items-center mx-auto mr-sm-0 mt-5 mt-sm-0">
        <nuxt-link
          :to="localePath('despre')"
          class="font-weight-bold mr-2 mr-sm-4 text-body"
        >
          {{ $t('nav_about') }}
        </nuxt-link>
        <select
          v-model="selectedValue"
          class="custom-select"
          @change="onChange(selectedValue)"
        >
          <option
            v-for="(locale, index) in $i18n.locales"
            :key="index"
            :value="locale.code"
            :selected="locale.code === selectedValue"
          >
            {{ locale.name }}
          </option>
        </select>
        <a
          href="https://code4.ro/ro/doneaza"
          class="btn btn-success text-white font-weight-bold ml-2 ml-sm-4"
        >
          {{ $t('donate') }}
        </a>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  data() {
    return {
      selectedValue: this.$i18n.locale,
    }
  },
  computed: {
    availableLocales() {
      return this.$i18n.locales.filter((i) => i.code !== this.$i18n.locale)
    },
  },
  methods: {
    onChange(event) {
      this.$router.replace(this.switchLocalePath(event))
    },
  },
}
</script>

<style lang="scss" scoped>
.dropdown-menu {
  &.small {
    min-width: 0;
  }
}
</style>
