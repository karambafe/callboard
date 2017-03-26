<template>
  <div id="app">
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
  import Squad from './components/Squad'
  import Calendar from './components/Calendar'

  function getCookie(name) {
    var matches = document.cookie.match(new RegExp(
      "(?:^|; )" + name.replace(/([\.$?*|{}\(\)\[\]\\\/\+^])/g, '\\$1') + "=([^;]*)"
    ));
    return matches ? decodeURIComponent(matches[1]) : undefined;
  }

  function setCookie(name, value, options) {
    options = options || {};

    var expires = options.expires;

    if (typeof expires == "number" && expires) {
      var d = new Date();
      d.setTime(d.getTime() + expires * 1000);
      expires = options.expires = d;
    }
    if (expires && expires.toUTCString) {
      options.expires = expires.toUTCString();
    }

    value = encodeURIComponent(value);

    var updatedCookie = name + "=" + value;

    for (var propName in options) {
      updatedCookie += "; " + propName;
      var propValue = options[propName];
      if (propValue !== true) {
        updatedCookie += "=" + propValue;
      }
    }

    document.cookie = updatedCookie;
  }

  const options = {
    expires: 10000000,
  };

  let squadsInformation = [
    { name: 'Голубева', day: 27, month: 1, year: 2017, isActive: false },
    { name: 'Cухарев', day: 28, month: 1, year: 2017, isActive: false },
    { name: 'Ворожцов', day: 25, month: 1, year: 2017, isActive: false },
    { name: 'Зубов', day: 26, month: 1, year: 2017, isActive: false },
  ];

  let squadCurrent = getCookie('squad');

  if (squadCurrent == undefined) {
    squadCurrent = 0;
  }

  squadsInformation[squadCurrent].isActive = true;



  export default {
    name: 'app',
    components: {
      Squad,
      Calendar,
    },
    data () {
      return {
        squads: squadsInformation,
        squadActive: squadCurrent,
      }
    },
    methods: {
      onSwitchSquad: function (id) {
        let i;
        for (i = 0; i < this.squads.length; ++i) {
          this.squads[i].isActive = false;
        }
        this.squads[id].isActive = true;
        this.squadActive = id;
        setCookie('squad', id, options);
      },
    }
  }
</script>

<style lang="scss">
  @import "assets/scss/main.scss";
</style>
