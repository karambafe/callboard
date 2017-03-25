<template>
  <div id="app">
    <div class="callboard">
      <div v-show="false">{{ msg }}</div>
      <div class="callboard__container">
        <div class="squad">
          <squad v-bind:name="squads[0].name" v-bind:id="0" v-bind:state="squads[0].isActive" v-on:switchSquad="onSwitchSquad"></squad>
          <squad v-bind:name="squads[1].name" v-bind:id="1" v-bind:state="squads[1].isActive" v-on:switchSquad="onSwitchSquad"></squad>
          <squad v-bind:name="squads[2].name" v-bind:id="2" v-bind:state="squads[2].isActive" v-on:switchSquad="onSwitchSquad"></squad>
          <squad v-bind:name="squads[3].name" v-bind:id="3" v-bind:state="squads[3].isActive" v-on:switchSquad="onSwitchSquad"></squad>
        </div>
        <calendar :squadInformation="squadInformation"></calendar>
      </div>
    </div>
</div>
</template>

<script>
  import Squad from './components/Squad'
  import Calendar from './components/Calendar'

  export default {
    name: 'app',
    components: {
      Squad,
      Calendar,
    },
    data () {
      return {
        msg: '',
        squads: [
          { name: 'Голубева', day: 27, month: 1, year: 2017, isActive: true },
          { name: 'Cухарев', day: 28, month: 1, year: 2017, isActive: false },
          { name: 'Ворожцов', day: 25, month: 1, year: 2017, isActive: false },
          { name: 'Зубов', day: 26, month: 1, year: 2017, isActive: false },
        ],
        squadInformation: {
          name: 'Голубева', day: 27, month: 1, year: 2017, isActive: true,
        }
      }
    },
    methods: {
      onSwitchSquad: function (id) {
        let i;
        for (i = 0; i < this.squads.length; ++i) {
          this.squads[i].isActive = false;
        }
        this.squads[id].isActive = true;
        this.msg = id;
        this.squadInformation = this.squads[id];
      }
    }
  }
</script>

<style lang="scss">
  @import "assets/scss/main.scss";
</style>
