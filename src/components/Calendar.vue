<template>
  <div class="calendar">
    <div class="calendar__month">
      <i v-on:click="switchPreviousMonth" class="button ion-chevron-left"></i>
      <div v-for="item in months" v-if="item.id == month" class="month">{{ item.name }}</div>
      <div v-if="year != 2017" class="year">{{ year }}</div>
      <i v-on:click="switchNextMonth" class="button ion-chevron-right"></i>
    </div>
    <div class="row">
      <div v-for="day in days" class="cell cell_days">{{ day }}</div>
    </div>
    <div class="wrapper">
      <div
        v-for="item in daysArr"
        class="cell"
        v-bind:class="{ cell_hidden : !item.currentMonth }"
      >
        {{ item.day }}
      </div>
    </div>
  </div>



</template>

<script>
  var date = new Date();

  export default {
    name: 'calendar',
    data () {
      return {
        year: date.getFullYear(),
        month: date.getMonth(),
        days: ['пн', 'вт', 'ср', 'чт', 'пт', 'сб', 'вс'],
        months: [
          { id: 0, name: 'Январь' },
          { id: 1, name: 'Февраль' },
          { id: 2, name: 'Март' },
          { id: 3, name: 'Апрель' },
          { id: 4, name: 'Май' },
          { id: 5, name: 'Июнь' },
          { id: 6, name: 'Июль' },
          { id: 7, name: 'Август' },
          { id: 8, name: 'Сентябрь' },
          { id: 9, name: 'Октябрь' },
          { id: 10, name: 'Ноябрь' },
          { id: 11, name: 'Декабрь' },
        ],
        arr: [],
      }
    },
    methods: {
      switchPreviousMonth: function() {
        if (this.month == 0) {
          this.month = 11;
          this.year = this.year - 1;
        } else {
          this.month = this.month - 1;
        }
      },

      switchNextMonth: function() {
        if (this.month == 11) {
          this.month = 0;
          this.year = this.year + 1;
        } else {
          this.month = this.month + 1;
        }
      },
      calculateMonth: function (month) {
        let returnMonth;
        if (month  == 12) {
          returnMonth = 0;
        } else if (month == -1) {
          returnMonth = 11;
        } else {
          returnMonth = month
        }

        return returnMonth;
      },
      calculateYearForPreviousMonth: function (month, year) {
        let returnYear;
        if (month  == 0) {
          returnYear = year - 1;
        } else {
          returnYear = year
        }

        return returnYear;
      },
      calculateYearForNextMonth: function (month, year) {
        let returnYear;
        if (month  == 11) {
          returnYear = year +1 ;
        } else {
          returnYear = year
        }

        return returnYear;
      },
      getDaysInMOnth: function (year, month) {
        return 33 - new Date(year, month, 33).getDate();
      }
    },
    computed: {
      daysInCurrentMonth () {
        return this.getDaysInMOnth(this.year, this.month);
      },
      firstDayInMonth () {
        return new Date(this.year, this.month, 1).getDay();
      },
      lastDayInMonth () {
        return new Date(this.year, this.month, this.daysInCurrentMonth).getDay();
      },
      daysArr () {
        this.arr.length = 0;
        let firstDayInMonth;
        if (this.firstDayInMonth == 0) {
          firstDayInMonth = 7;
        } else {
          firstDayInMonth = this.firstDayInMonth;
        }

        for (let i = 0; i < firstDayInMonth - 1; i++) {
          this.arr.push({
            day: this.getDaysInMOnth(this.year, this.month -1) - firstDayInMonth + 2 + i,
            month: this.calculateMonth(this.month - 1),
            currentMonth: false,
            year: this.calculateYearForPreviousMonth(this.month, this.year),
          });
        }

        for (let i = 1; i <= this.daysInCurrentMonth; i++) {
          this.arr.push({
            day: i,
            month: this.month,
            year: this.year,
            currentMonth: true,
          });
        }

        let lastDayInMonth;
        if (this.lastDayInMonth == 0) {
          lastDayInMonth = 7;
        } else {
          lastDayInMonth = this.lastDayInMonth;
        }
        for (let i = 1; i <= 7 - lastDayInMonth; i++) {
          this.arr.push({
            day: i,
            month: this.calculateMonth(this.month + 1),
            year: this.calculateYearForNextMonth(this.month, this.year),
            currentMonth: false,
          });
        }
        return this.arr;
      },
    }
  };
</script>
