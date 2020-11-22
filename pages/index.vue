<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-12 mt-4 mb-5">
          <VotersGuide />
        </div>
      </div>
    </div>
    <div class="bg-light">
      <div class="container mt-4 mb-5 py-4">
        <div class="row">
          <div class="col-lg-4">
            <h4>{{ $t('exceptional_cases.case1_title') }}</h4>
            <div v-html="$t('exceptional_cases.case1_text')"></div>
          </div>
          <div class="col-lg-4">
            <h4>{{ $t('exceptional_cases.case2_title') }}</h4>
            <div v-html="$t('exceptional_cases.case2_text')"></div>
          </div>
          <div class="col-lg-4">
            <h4>{{ $t('exceptional_cases.case3_title') }}</h4>
            <div v-html="$t('exceptional_cases.case3_text')"></div>
          </div>
        </div>
      </div>
    </div>
    <div class="container mt-4 mb-5">
      <div class="row">
        <div class="col-12 mt-4 mb-5">
          <h2 class="h4 text-center">
            {{ $t('pollingStationSearch.question') }}
          </h2>
          <p class="text-center">
            {{ $t('pollingStationSearch.callToAction') }}
          </p>
          <PollingStationSearchGMaps />
        </div>
      </div>
    </div>
  </div>
</template>
