<template>
  <div class="container">
    <div class="row">
      <div class="col-12 mt-4 mb-5">
        <VotersGuide />
      </div>
    </div>
    <div class="row mt-4 mb-5">
      <div class="col-lg-4">
        <h4>{{ $t('exceptionalCases.title1') }}</h4>
        <div v-html="$t('exceptionalCases.content1')"></div>
      </div>
      <div class="col-lg-4">
        <h4>{{ $t('exceptionalCases.title2') }}</h4>
        <div v-html="$t('exceptionalCases.content2')"></div>
      </div>
      <div class="col-lg-4">
        <h4>{{ $t('exceptionalCases.title3') }}</h4>
        <div v-html="$t('exceptionalCases.content3')"></div>
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
        <PollingStationSearchGMaps />
      </div>
    </div>
  </div>
</template>
