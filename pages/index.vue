<template>
  <div class="container">
    <div class="row">
      <div class="col-12 mt-4 mb-5">
        <VotersGuide />
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
