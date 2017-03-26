<template>
  <div id="app">
    <md-toolbar>
      <h1 class="md-title" style="flex: 1">My Title</h1>
      <md-button class="md-icon-button">
        <md-icon>more_vert</md-icon>
      </md-button>
    </md-toolbar>

    <md-button class="md-primary">Primary</md-button>
    <md-avatar class="md-avatar-icon md-primary">
      <md-icon>folder</md-icon>
    </md-avatar>
    <div class="callboard">
      <div class="callboard__container">
        <div class="squad">
          <squad v-bind:name="squads[0].name" v-bind:id="0" v-bind:state="squads[0].isActive" v-on:switchSquad="onSwitchSquad"></squad>
          <squad v-bind:name="squads[1].name" v-bind:id="1" v-bind:state="squads[1].isActive" v-on:switchSquad="onSwitchSquad"></squad>
          <squad v-bind:name="squads[2].name" v-bind:id="2" v-bind:state="squads[2].isActive" v-on:switchSquad="onSwitchSquad"></squad>
          <squad v-bind:name="squads[3].name" v-bind:id="3" v-bind:state="squads[3].isActive" v-on:switchSquad="onSwitchSquad"></squad>
        </div>
        <calendar :squadInformation="squads[squadActive]"></calendar>
      </div>
    </div>
</div>
</template>

<script>
  import { setCookie, getCookie } from './assets/js/cookie';

  import Squad from './components/Squad';
  import Calendar from './components/Calendar';

  const options = {
    expires: 10000000,
  };

  const squadsInformation = [
    { name: 'Голубева', day: 27, month: 1, year: 2017, isActive: false },
    { name: 'Cухарев', day: 28, month: 1, year: 2017, isActive: false },
    { name: 'Ворожцов', day: 25, month: 1, year: 2017, isActive: false },
    { name: 'Зубов', day: 26, month: 1, year: 2017, isActive: false },
  ];

  let squadCurrent = getCookie('squad');

  if (!squadCurrent) {
    squadCurrent = 0;
  }

  squadsInformation[squadCurrent].isActive = true;

  export default {
    name: 'app',
    components: {
      Squad,
      Calendar,
    },
    data() {
      return {
        squads: squadsInformation,
        squadActive: squadCurrent,
      };
    },
    methods: {
      onSwitchSquad(id) {
        let i;
        for (i = 0; i < this.squads.length; i += 1) {
          this.squads[i].isActive = false;
        }
        this.squads[id].isActive = true;
        this.squadActive = id;
        setCookie('squad', id, options);
      },
    },
  };
</script>

<style lang="scss">
  @import '../node_modules/vue-material/dist/vue-material.css';
  @import "assets/scss/main.scss";
</style>
