<template>
  <div class="card border-0">
    <h5 class="card-header bg-white">
      {{ $t('pollingStationCard.pollingStationNumber') }}
      {{ pollingStationNumber.join() }}, {{ county }}
    </h5>
    <div class="card-body">
      <div class="d-flex justify-content-between align-items-center">
        <p class="m-0">
          <span class="bg-warning px-1 mr-1">{{
            $t('pollingStationCard.address')
          }}</span>
          {{ address }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    pollingStationNumber: { type: Array, default: () => [] },
    county: { type: String, default: '' },
    address: { type: String, default: '' },
  },
}
</script>
