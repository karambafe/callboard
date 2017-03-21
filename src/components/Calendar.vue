<template>
  <div class="calendar">
    <div class="calendar__month">
      <i v-on:click="switchPreviousMonth" class="button ion-chevron-left"></i>
      <div v-for="item in months" v-if="item.id == month" class="month">{{ item.name }}</div>
      <div v-if="year != 2017" class="year">{{ year }}</div>
      <i v-on:click="switchNextMonth" class="button ion-chevron-right"></i>
    </div>

    {{ firstDayInMonth }}
    {{ lastDayInMonth }}
  </div>

</template>

<script>
  Date.prototype.daysInMonth = function() {
    return 33 - new Date(this.getFullYear(), this.getMonth(), 33).getDate();
  };

  Date.prototype.firstDayInMonth = function() {
    return new Date(this.getFullYear(), this.getMonth(), 1).getDay();
  };

  Date.prototype.lastDayInMonth = function() {
    return new Date(this.getFullYear(), this.getMonth(), this.daysInMonth()).getDay();
  };

  var date = new Date();

  export default {
    name: 'calendar',
    data () {
      return {
        year: date.getFullYear(),
        month: date.getMonth(),
        daysInMonth: date.daysInMonth(),
        firstDayInMonth: date.firstDayInMonth(),
        lastDayInMonth: date.lastDayInMonth(),
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
    }
  };
</script>
