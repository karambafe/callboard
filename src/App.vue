<template>
  <div id="app">
    <div class="callboard">
      <div v-show="false">{{ msg }}</div>
      <div class="callboard__container">
        <div class="squad">
          <squad name="Голубева" v-bind:id="0" v-bind:state="activeSquad[0]" v-on:removestyles="falseState"></squad>
          <squad name="Зубов" v-bind:id="1" v-bind:state="activeSquad[1]" v-on:removestyles="falseState"></squad>
          <squad name="Свешникова" v-bind:id="2" v-bind:state="activeSquad[2]" v-on:removestyles="falseState"></squad>
          <squad name="Ворожцов" v-bind:id="3" v-bind:state="activeSquad[3]" v-on:removestyles="falseState"></squad>
        </div>
      </div>
    </div>
    <!--<div class="row row_buttons">-->
      <!--<button class="group-button" v-on:click="changeGroup('golubeva')" v-bind:class="{ active : buttonActiveGolubeva }">Голубева</button>-->
      <!--<button class="group-button" v-on:click="changeGroup('sveshnikova')" v-bind:class="{ active : buttonActiveSveshnikova }">Свешникова</button>-->
      <!--<button class="group-button" v-on:click="changeGroup('belov')" v-bind:class="{ active : buttonActiveBelov }">Белов</button>-->
      <!--<button class="group-button" v-on:click="changeGroup('zubov')" v-bind:class="{ active : buttonActiveZubov }">Зубов</button>-->
    <!--</div>-->
    <!--<div class="row row_month">-->
      <!--<i v-on:click="switchPreviousMonth" class="button ion-chevron-left"></i>-->
      <!--<div v-for="month in months" v-if="month.id == currentMonth" class="month">{{ month.name }}</div>-->
      <!--<div v-if="year != 2017" class="year">{{ year }}</div>-->
      <!--<i v-on:click="switchNextMonth" class="button ion-chevron-right"></i>-->
    <!--</div>-->
    <!--<div class="container">-->
      <!--<div class="row">-->
        <!--<div v-for="day in days" class="cell cell_days">{{ day }}</div>-->
      <!--</div>-->
      <!--<div class="wrapper">-->
        <!--<div-->
            <!--v-for="element in computedArr"-->
            <!--class="cell"-->
            <!--v-bind:class="{ cell_hidden : !element.monthType, cell_daytime : element.workDay, cell_nighttime : element.workNigth }"-->
        <!--&gt;-->
          <!--{{ element.day }}-->
        <!--</div>-->
      <!--</div>-->
    <!--</div>-->
</div>
</template>

<script>
  import Squad from './components/Squad'

  export default {
    name: 'app',
    data () {
      return {
        msg: 'Test vue js',
        activeSquad: [false, false, false, false]
      }
    },
    components: {
      Squad,
    },
    methods: {
      falseState: function (id) {
        var i;
        for (i = 0; i < this.activeSquad.length; ++i) {
          this.activeSquad[i] = false;
        }
        this.activeSquad[id] = true;
        this.msg = id;
      }
    }
  }
</script>


<!--<script>-->
  <!--Date.prototype.daysInMonth = function() {-->
    <!--return 33 - new Date(this.getFullYear(), this.getMonth(), 33).getDate();-->
  <!--};-->

  <!--Date.prototype.firstDayInCurrentMonth = function() {-->
    <!--return new Date(this.getFullYear(), this.getMonth(), 1).getDay();-->
  <!--};-->

  <!--Date.prototype.lastDayInCurrentMonth = function() {-->
    <!--return new Date(this.getFullYear(), this.getMonth(), this.daysInMonth()).getDay();-->
  <!--};-->

  <!--var date = new Date();-->

  <!--var app = new Vue({-->
    <!--el: '#app',-->
    <!--data: {-->
      <!--months: [-->
        <!--{ id: 0, name: 'Январь' },-->
        <!--{ id: 1, name: 'Февраль' },-->
        <!--{ id: 2, name: 'Март' },-->
        <!--{ id: 3, name: 'Апрель' },-->
        <!--{ id: 4, name: 'Май' },-->
        <!--{ id: 5, name: 'Июнь' },-->
        <!--{ id: 6, name: 'Июль' },-->
        <!--{ id: 7, name: 'Август' },-->
        <!--{ id: 8, name: 'Сентябрь' },-->
        <!--{ id: 9, name: 'Октябрь' },-->
        <!--{ id: 10, name: 'Ноябрь' },-->
        <!--{ id: 11, name: 'Декабрь' },-->
      <!--],-->
      <!--days: ['пн', 'вт', 'ср', 'чт', 'пт', 'сб', 'вс'],-->
      <!--year: date.getFullYear(),-->
      <!--currentMonth: date.getMonth(),-->
      <!--countDays: date.daysInMonth(),-->
      <!--firstDayInMonth: date.firstDayInCurrentMonth(),-->
      <!--lastDayInMonth: date.lastDayInCurrentMonth(),-->
      <!--arr: [],-->
      <!--dayTime: {-->
        <!--day: 6,-->
        <!--month: 0,-->
        <!--year: 2017,-->
      <!--},-->
      <!--nightTime: {-->
        <!--day: 7,-->
        <!--month: 0,-->
        <!--year: 2017,-->
      <!--},-->
      <!--hidden_class: 'cell_hidden',-->
      <!--daytime_class: 'cell_daytime',-->
      <!--nighttime_class: 'cell_nighttime',-->
      <!--active_class: 'active',-->
      <!--buttonActiveGolubeva: true,-->
      <!--buttonActiveSveshnikova: false,-->
      <!--buttonActiveBelov: false,-->
      <!--buttonActiveZubov: false,-->
    <!--},-->
    <!--computed: {-->
      <!--computedArr: function () {-->
        <!--this.arr.length = 0;-->
        <!--var firstDayInMonthRight;-->
        <!--if (this.firstDayInMonth == 0) {-->
          <!--firstDayInMonthRight = 7;-->
        <!--} else {-->
          <!--firstDayInMonthRight = this.firstDayInMonth;-->
        <!--}-->
        <!--for (var i = 0; i < firstDayInMonthRight - 1; i++) {-->
          <!--this.arr.push({-->
            <!--day: this.daysInMonthTrue(this.year, this.currentMonth -1) - firstDayInMonthRight + 2 + i,-->
            <!--month: this.calculateMonth(this.currentMonth - 1),-->
            <!--year: this.calculateYearForPreviousMonth(this.currentMonth, this.year),-->
            <!--monthType: false,-->
            <!--days: this.daysInMonthTrue(this.year, this.currentMonth -1),-->
            <!--workDay: false,-->
            <!--workNigth: false,-->
          <!--});-->
        <!--}-->
        <!--for (var i = 1; i <= this.countDays; i++) {-->
          <!--this.arr.push({-->
            <!--day: i,-->
            <!--month: this.currentMonth,-->
            <!--year: this.year,-->
            <!--monthType: true,-->
            <!--days: this.daysInMonthTrue(this.year, this.currentMonth),-->
            <!--workDay: false,-->
            <!--workNigth: false,-->
          <!--});-->
        <!--}-->
        <!--var lastDayInMonthRight;-->
        <!--if (this.lastDayInMonth == 0) {-->
          <!--lastDayInMonthRight = 7;-->
        <!--} else {-->
          <!--lastDayInMonthRight = this.lastDayInMonth;-->
        <!--}-->
        <!--for (var i = 1; i <= 7 - lastDayInMonthRight; i++) {-->
          <!--this.arr.push({-->
            <!--day: i,-->
            <!--month: this.calculateMonth(this.currentMonth + 1),-->
            <!--year: this.calculateYearForNextMonth(this.currentMonth, this.year),-->
            <!--monthType: false,-->
            <!--days: this.daysInMonthTrue(this.year, this.currentMonth + 1),-->
            <!--workDay: false,-->
            <!--workNigth: false,-->
          <!--});-->
        <!--}-->
        <!--console.log(this.arr);-->


        <!--var dayTimeYear = this.dayTime.year;-->
        <!--var dayTimeMonth = this.dayTime.month;-->
        <!--var dayTimeDay = this.dayTime.day;-->
        <!--var nightTimeYear = this.nightTime.year;-->
        <!--var nightTimeMonth = this.nightTime.month;-->
        <!--var nightTimeDay = this.nightTime.day;-->
        <!--this.arr.map(function (item) {-->
          <!--dayTimeOfTable = +new Date(dayTimeYear, dayTimeMonth, dayTimeDay);-->
          <!--dayCurrent = +new Date(item.year, item.month, item.day);-->
          <!--nightTimeOfTable = +new Date(nightTimeYear, nightTimeMonth, nightTimeDay);-->
          <!--dayTimeOfTable = dayTimeOfTable / (3600 * 24 * 1000);-->
          <!--nightTimeOfTable = nightTimeOfTable / (3600 * 24 * 1000);-->
          <!--dayCurrent = dayCurrent / (3600 * 24 * 1000);-->

          <!--if (dayCurrent >= dayTimeOfTable) {-->
            <!--item.workDay = (dayCurrent - dayTimeOfTable) % 4 == 0;-->
          <!--} else {-->
            <!--item.workDay = (dayTimeOfTable - dayCurrent) % 4 == 0;-->
          <!--}-->

          <!--if (dayCurrent >= nightTimeOfTable) {-->
            <!--item.workNigth = (dayCurrent - nightTimeOfTable) % 4 == 0;-->
          <!--} else {-->
            <!--item.workNigth = (nightTimeOfTable - dayCurrent) % 4 == 0;-->
          <!--}-->

          <!--return this.arr;-->
        <!--});-->

        <!--return this.arr;-->
      <!--}-->
    <!--},-->
    <!--methods: {-->
      <!--daysInMonthNew: function() {-->
        <!--this.countDays =  33 - new Date(this.year, this.currentMonth, 33).getDate();-->
      <!--},-->
      <!--daysInMonthTrue: function(year, month) {-->
        <!--if (month == -1) {-->
          <!--month = 11;-->
        <!--} else if ( month == 11) {-->
          <!--month = 0;-->
        <!--}-->
        <!--return 33 - new Date(year, month, 33).getDate();-->
      <!--},-->
      <!--getFirstDayInMonth: function() {-->
        <!--this.firstDayInMonth =  new Date(this.year, this.currentMonth, 1).getDay();-->
      <!--},-->
      <!--getLastDayInMonth: function() {-->
        <!--this.lastDayInMonth =  new Date(this.year, this.currentMonth, this.daysInMonthTrue(this.year, this.currentMonth)).getDay();-->
      <!--},-->
      <!--switchPreviousMonth: function() {-->
        <!--if (this.currentMonth == 0) {-->
          <!--this.currentMonth = 11;-->
          <!--this.year = this.year - 1;-->
          <!--this.daysInMonthNew();-->
          <!--this.getFirstDayInMonth();-->
          <!--this.getLastDayInMonth();-->
        <!--} else {-->
          <!--this.currentMonth = this.currentMonth - 1;-->
          <!--this.daysInMonthNew();-->
          <!--this.getFirstDayInMonth();-->
          <!--this.getLastDayInMonth();-->
        <!--}-->
      <!--},-->

      <!--switchNextMonth: function() {-->
        <!--if (this.currentMonth == 11) {-->
          <!--this.currentMonth = 0;-->
          <!--this.year = this.year + 1;-->
          <!--this.daysInMonthNew();-->
          <!--this.getFirstDayInMonth();-->
          <!--this.getLastDayInMonth();-->
        <!--} else {-->
          <!--this.currentMonth = this.currentMonth + 1;-->
          <!--this.daysInMonthNew();-->
          <!--this.getFirstDayInMonth();-->
          <!--this.getLastDayInMonth();-->
        <!--}-->
      <!--},-->

      <!--calculateMonth: function (month) {-->
        <!--var returnMonth;-->
        <!--if (month  == 12) {-->
          <!--returnMonth = 0;-->
        <!--} else if (month == -1) {-->
          <!--returnMonth = 11;-->
        <!--} else {-->
          <!--returnMonth = month-->
        <!--}-->

        <!--return returnMonth;-->
      <!--},-->

      <!--calculateYearForPreviousMonth: function (month, year) {-->
        <!--var returnYear;-->
        <!--if (month  == 0) {-->
          <!--returnYear = year - 1;-->
        <!--} else {-->
          <!--returnYear = year-->
        <!--}-->

        <!--return returnYear;-->
      <!--},-->

      <!--calculateYearForNextMonth: function (month, year) {-->
        <!--var returnYear;-->
        <!--if (month  == 11) {-->
          <!--returnYear = year +1 ;-->
        <!--} else {-->
          <!--returnYear = year-->
        <!--}-->

        <!--return returnYear;-->
      <!--},-->

      <!--changeGroup: function (group) {-->
        <!--switch (group) {-->
          <!--case 'golubeva':-->
            <!--this.dayTime = {-->
              <!--day: 6,-->
              <!--month: 0,-->
              <!--year: 2017,-->
            <!--};-->
            <!--this.nightTime = {-->
              <!--day: 7,-->
              <!--month: 0,-->
              <!--year: 2017,-->
            <!--};-->
            <!--this.buttonActiveGolubeva = true;-->
            <!--this.buttonActiveSveshnikova = false;-->
            <!--this.buttonActiveBelov = false;-->
            <!--this.buttonActiveZubov = false;-->
            <!--break;-->

          <!--case 'sveshnikova':-->
            <!--this.dayTime = {-->
              <!--day: 7,-->
              <!--month: 0,-->
              <!--year: 2017,-->
            <!--};-->
            <!--this.nightTime = {-->
              <!--day: 8,-->
              <!--month: 0,-->
              <!--year: 2017,-->
            <!--};-->
            <!--this.buttonActiveGolubeva = false;-->
            <!--this.buttonActiveSveshnikova = true;-->
            <!--this.buttonActiveBelov = false;-->
            <!--this.buttonActiveZubov = false;-->
            <!--break;-->

          <!--case 'belov':-->
            <!--this.dayTime = {-->
              <!--day: 8,-->
              <!--month: 0,-->
              <!--year: 2017,-->
            <!--};-->
            <!--this.nightTime = {-->
              <!--day: 9,-->
              <!--month: 0,-->
              <!--year: 2017,-->
            <!--};-->
            <!--this.buttonActiveGolubeva = false;-->
            <!--this.buttonActiveSveshnikova = false;-->
            <!--this.buttonActiveBelov = true;-->
            <!--this.buttonActiveZubov = false;-->
            <!--break;-->

          <!--case 'zubov':-->
            <!--this.dayTime = {-->
              <!--day: 9,-->
              <!--month: 0,-->
              <!--year: 2017,-->
            <!--};-->
            <!--this.nightTime = {-->
              <!--day: 10,-->
              <!--month: 0,-->
              <!--year: 2017,-->
            <!--};-->
            <!--this.buttonActiveGolubeva = false;-->
            <!--this.buttonActiveSveshnikova = false;-->
            <!--this.buttonActiveBelov = false;-->
            <!--this.buttonActiveZubov = true;-->
            <!--break;-->

          <!--default:-->
            <!--this.dayTime = {-->
              <!--day: 6,-->
              <!--month: 0,-->
              <!--year: 2017,-->
            <!--};-->
            <!--this.nightTime = {-->
              <!--day: 7,-->
              <!--month: 0,-->
              <!--year: 2017,-->
            <!--};-->
            <!--this.buttonActiveGolubeva = true;-->
            <!--this.buttonActiveSveshnikova = false;-->
            <!--this.buttonActiveBelov = false;-->
            <!--this.buttonActiveZubov = false;-->
            <!--break;-->
        <!--}-->
      <!--}-->
    <!--}-->
  <!--})-->
<!--</script>-->


<style lang="scss">
  @import "assets/scss/main.scss";
</style>
