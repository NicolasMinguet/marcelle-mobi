<template>
  <div>
    <div class="filterGo">
      <div class="containerButtonsMap mr-2 mb-3">
        <b-button variant="light" pill @click="refreshMap" style="width: 40px;height: 40px;">
          <i :class="['fas fa-sync-alt', {'fa-spin': isLoading}]"></i>
        </b-button>
        <div
          @click="$store.commit('map/TOGGLE_FILTER')"
          class="buttonGo"
        >{{$store.state.map.filterVisible ? 'X' : 'Go'}}</div>
      </div>
      <b-collapse :visible="$store.state.map.filterVisible">
        <div v-if="$store.state.map.filterVisible" id="filter" class="container">
          <div class="row justify-content-between mx-0 clickable">
            <div class="col-3 borderBottom" @click="this.$router.push({ path: '/bowling' })">
              <h2 class="lettreTransport text-primary">B</h2>
              <p class="textFilter">Bowling</p>
            </div>

            <div
              class="col-3 borderCentral borderBottom"
              @click="$router.push({ path: '/cinema' })"
            >
              <h2 class="lettreTransport text-primary">C</h2>
              <p class="textFilter">Cinéma</p>
            </div>

            <div
              class="col-3 borderCentral borderBottom"
              @click="$router.push({ path: '/football' })"
            >
              <h2 class="lettreTransport text-primary">F</h2>
              <p class="textFilter">Football</p>
            </div>

            <div
              class="col-3 borderCentral borderBottom"
              @click="$router.push({ path: '/nautique' })"
            >
              <h2 class="lettreTransport text-primary">S</h2>
              <p class="textFilter">Sports Nautiques</p>
            </div>

            <div
              class="col-3 borderCentral borderBottom"
              @click="$router.push({ path: '/randonnee' })"
            >
              <h2 class="lettreTransport text-primary">R</h2>
              <p class="textFilter">Randonnées</p>
            </div>

            <div @click="$router.push({ path: '/arcade' })" class="col-3">
              <h2 class="lettreTransport text-primary">A</h2>
              <p class="textFilter">Arcade</p>
            </div>

            <div @click="$router.push({ path: '/plage' })" class="col-3 borderCentral">
              <h2 class="lettreTransport text-primary">P</h2>
              <p class="textFilter">Plage</p>
            </div>

            <div @click="$router.push({ path: '/basket' })" class="col-3 borderCentral">
              <h2 class="lettreTransport text-primary">B</h2>
              <p class="textFilter">Basket</p>
            </div>

            <div @click="$router.push({ path: '/running' })" class="col-3 borderCentral">
              <h2 class="lettreTransport text-primary">R</h2>
              <p class="textFilter">Running</p>
            </div>
          </div>
        </div>
      </b-collapse>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isLoading: false
    }
  },

  methods: {
    async refreshMap() {
      this.isLoading = true
      await this.$store.dispatch('map/fetchAllVehicles', this.location)
      this.isLoading = false
    }
  }
}
</script>

<style lang="scss">
.filterGo {
  width: 100%;
  z-index: 450;
  position: fixed;
  left: 0;
  bottom: 0;

  .active {
    background-color: rgba(187, 231, 255, 0.38);
  }

  #filter {
    z-index: 999;
    text-align: center;
    background-color: aliceblue;
    border-radius: 0.5rem;
    width: 96%;
    box-shadow: 5px 5px 5px gray;
    margin-bottom: 5px;
    padding: 0;
  }

  .borderCentral {
    border-right: 1px solid rgba(182, 181, 181, 0.5);

    border-left: 1px solid rgba(182, 181, 181, 0.5);
  }

  .borderBottom {
    border-bottom: 1px solid rgba(182, 181, 181, 0.5);
  }

  .buttonGo {
    width: 40px;
    height: 40px;
    background: #0e5da4;
    box-shadow: 2px 2px 8px #aaa;
    font: bold 1rem Arial;
    border-radius: 50%;
    border: 2px solid White;
    color: white;
    right: 2vw;
    text-align: center;
    padding: 10px 0px;
    margin-top: 20px;
  }

  .containerButtonsMap {
    position: absolute;
    right: 0;
    bottom: 100%;
    display: flex;
    flex-direction: column;
  }

  .lettreTransport {
    width: 40px;
    height: 40px;
    display: inline-block;
    border: 2px solid #0e5da4;
    border-radius: 75%;
    padding: 0.3rem;
    margin-top: 0.5rem;
    font-size: 1.3rem;
  }
}
</style>
