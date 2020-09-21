<template>
  <div class="container">
    <div class="row">
      <div class="col-12 mt-4 mb-5">
        <VotersGuide />
      </div>
    </div>
    <div class="row">
      <div class="col-12 col-lg-4">
        <h2 class="h5 pb-2">
          {{ $t('exceptional_cases.case1_title') }}
        </h2>
        <div v-html="$t('exceptional_cases.case1_text')"></div>
      </div>
      <div class="col-12 col-lg-4 py-4 py-lg-0">
        <h2 class="h5 pb-2">
          {{ $t('exceptional_cases.case2_title') }}
        </h2>
        <p>
          {{ $t('exceptional_cases.case2_text') }}
        </p>
      </div>
      <div class="col-12 col-lg-4">
        <h2 class="h5 pb-2">
          {{ $t('exceptional_cases.case3_title') }}
        </h2>
        <p>
          {{ $t('exceptional_cases.case3_text') }}
        </p>
      </div>
    </div>
    <div class="row">
      <div class="col-12 mt-4 mb-5">
        <h2 class="h4 text-center">
          {{ $t('pollingStationSearch.question') }}
        </h2>
        <p class="text-center">
          {{ $t('pollingStationSearch.callToAction') }}
        </p>
        <PollingStationSearch />
      </div>
    </div>
  </div>
</template>
