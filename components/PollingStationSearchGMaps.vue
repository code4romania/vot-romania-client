<template>
  <div>
    <Autocomplete
      :placeholder="$t('pollingStationSearch.searchPlaceholder')"
      :select-first-on-enter="true"
      class="w-75 mx-auto mb-4 d-block"
      @place_changed="setPlace"
    >
    </Autocomplete>
    <div v-show="showErrorMessage" class="bg-danger p-2 text-center text-white">
      Ne pare rau, a aparut o eroare.
    </div>
    <div v-if="pollingStationsWithAddress.length">
      <p class="font-weight-bold my-4">
        {{ $t('pollingStationSearch.hasPermanentResidence') }}
      </p>
      <div
        class="row row-cols-1"
        :class="pollingStationsWithAddress.length > 1 ? 'row-cols-md-2' : ''"
      >
        <div
          v-for="pollingStation of pollingStationsWithAddress"
          :key="pollingStation.id"
          class="col mb-4"
        >
          <PollingStationCard
            :polling-station-number="pollingStation.pollingStationNumber"
            :county="pollingStation.county"
            :address="pollingStation.address"
            :distance="pollingStation.distance"
            :assigned-addresses="pollingStation.assignedAddresses"
          />
        </div>
      </div>
    </div>
    <div
      v-if="pollingStationsWithAddress.length === 0 && pollingStations.length"
    >
      <p class="font-weight-bold my-4">
        {{ $t('pollingStationSearch.addressNotFound') }}
      </p>
      <div
        class="row row-cols-1"
        :class="pollingStations.length > 1 ? 'row-cols-md-2' : ''"
      >
        <div
          v-for="pollingStation of pollingStations"
          :key="pollingStation.id"
          class="col mb-4"
        >
          <PollingStationCard
            :polling-station-number="pollingStation.pollingStationNumber"
            :county="pollingStation.county"
            :address="pollingStation.address"
            :distance="pollingStation.distance"
            :assigned-addresses="pollingStation.assignedAddresses"
          />
        </div>
      </div>
    </div>
    <GmapMap
      :center="center"
      :zoom="zoom"
      map-type-id="terrain"
      style="width: 100%; height: 500px"
    >
      <gmap-info-window
        :options="infoOptions"
        :position="infoWindowPos"
        :opened="infoWinOpen"
        @closeclick="infoWinOpen = false"
      >
      </gmap-info-window>

      <GmapMarker
        v-for="(m, index) in markers"
        :key="index"
        :position="m.position"
        :clickable="true"
        :icon="m.iconPath"
        @click="toggleInfoWindow(m, index)"
      />
    </GmapMap>
  </div>
</template>

<script>
import GmapMap from 'gmap-vue/dist/components/map'
import Autocomplete from 'gmap-vue/dist/components/autocomplete'
import GmapMarker from 'gmap-vue/dist/components/marker'
import GmapInfoWindow from 'gmap-vue/dist/components/info-window'
import { PollingStationMatcherService } from '../service/polling-station-matcher.service'
import houseMarker from '../assets/house_marker.svg'
import pollingStationMarker from '../assets/polling_station_marker.svg'

export default {
  components: {
    Autocomplete,
    GmapMap,
    GmapMarker,
    GmapInfoWindow,
  },

  data() {
    return {
      zoom: 7,
      center: { lat: 45.658, lng: 25.6012 },
      markers: [],
      showErrorMessage: false,
      pollingStations: [],
      pollingStationsWithAddress: [],
      pollingStationService: new PollingStationMatcherService(),
      infoWindowPos: null,
      infoWinOpen: false,
      currentMidx: null,
      infoOptions: {
        content: '',
        pixelOffset: {
          width: 0,
          height: -35,
        },
      },
    }
  },
  methods: {
    async setPlace(place) {
      if (!place) return

      this.clearMarkers()
      const latitude = place.geometry.location.lat()
      const longitude = place.geometry.location.lng()
      this.addMarker(latitude, longitude, houseMarker, place.formatted_address)

      const selectedGeocodeAddress = {}
      place.address_components.forEach((address) => {
        if (address.types.includes('locality')) {
          selectedGeocodeAddress.city = address.long_name
        }
        if (address.types.includes('route')) {
          selectedGeocodeAddress.street = address.long_name
        }
        if (address.types.includes('street_number')) {
          selectedGeocodeAddress.houseNumber = address.long_name
        }
      })

      const poolingResults = await this.findPoolingStation(latitude, longitude)
      this.pollingStations = [].concat(
        ...poolingResults.map((g) =>
          g.pollingStations.map((ps) => {
            return { ...ps, distance: g.distance }
          })
        )
      )
      this.pollingStationsWithAddress = this.pollingStationService.findPollingStation(
        this.pollingStations,
        selectedGeocodeAddress
      )
      const stations = this.pollingStationsWithAddress.length
        ? this.pollingStationsWithAddress
        : this.pollingStations
      stations.forEach((c) => {
        this.addMarker(
          c.latitude,
          c.longitude,
          pollingStationMarker,
          `${this.$t('pollingStationCard.pollingStationNumber')} ${
            c.pollingStationNumber
          }, ${c.institution} ${c.address}`
        )
      })

      if (stations.length === 1) {
        this.center = {
          lat: stations[0].latitude,
          lng: stations[0].longitude,
        }
        this.zoom = 16
      } else {
        this.center = {
          lat: latitude,
          lng: longitude,
        }
        this.zoom = 15
      }
    },
    async findPoolingStation(latitude, longitude) {
      try {
        const result = await fetch(
          `${process.env.NUXT_ENV_API_URL}/polling-station/near-me?latitude=${latitude}&longitude=${longitude}`
        )
        if (result.status !== 204 && result.status !== 200) {
          this.showErrorMessage = true
        }
        return await result.json()
      } catch (error) {
        this.showErrorMessage = true
      }
    },
    addMarker(lat, lng, iconPath, infoText) {
      this.markers.push({
        iconPath,
        position: {
          lat,
          lng,
        },
        infoText,
      })
    },
    clearMarkers() {
      this.markers = []
    },
    toggleInfoWindow(marker, idx) {
      this.infoWindowPos = marker.position
      this.infoOptions.content = marker.infoText

      if (this.currentMidx === idx) {
        this.infoWinOpen = !this.infoWinOpen
      } else {
        this.infoWinOpen = true
        this.currentMidx = idx
      }
    },
  },
}
</script>
