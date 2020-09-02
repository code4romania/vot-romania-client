<template>
  <div class="container">
    <div class="row">
      <div class="col-12 col-lg-4">
        <h3>
          {{ $t('exceptional_cases.case1_title') }}
        </h3>
        <div v-html="$t('exceptional_cases.case1_text')"></div>
      </div>
      <div class="col-12 col-lg-4 py-4 py-lg-0">
        <h3>
          {{ $t('exceptional_cases.case2_title') }}
        </h3>
        <p>
          {{ $t('exceptional_cases.case2_text') }}
        </p>
      </div>
      <div class="col-12 col-lg-4">
        <h3>
          {{ $t('exceptional_cases.case3_title') }}
        </h3>
        <p>
          {{ $t('exceptional_cases.case3_text') }}
        </p>
      </div>
    </div>
    <div class="coming-soon text-center p-2 my-5">
      <p class="font-weight-bold m-0">
        {{ $t('map_hero_p1') }}
        <a
          href="https://code4.ro/ro/doneaza/"
          target="_blank"
          rel="noopener noreferrer"
        >
          {{ $t('map_hero_p2') }}
        </a>
        {{ $t('map_hero_p3') }}
      </p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.coming-soon {
  background: #fc0;
  color: #352245;
}
</style>
