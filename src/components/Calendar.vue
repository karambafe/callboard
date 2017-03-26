<template>
  <div class="calendar">
    <div class="calendar__days">
      <div v-for="day in days" class="calendar__day">{{ day }}</div>
    </div>
    <div class="calendar__body">
      <div
        v-for="item in daysArr"
        class="calendar__day"
        v-bind:class="{ calendar__day_hidden : !item.isCurrentMonth, calendar__day_day : item.isDayShift, calendar__day_night : item.isNightShift }"
      >
        {{ item.day }}
      </div>
    </div>
    <div class="calendar__month">
      <div v-on:click="switchPreviousMonth">
        <md-button class="md-icon-button">
          <md-icon>navigate_before</md-icon>
        </md-button>
      </div>
      <div class="calendar__month-wrapper">
        <div v-for="item in months" v-if="item.id == month" class="calendar__month-title">{{ item.name }}</div>
        <transition name="fade">
          <div v-if="year != 2017" class="calendar__month-desc">{{ year }}</div>
        </transition>
      </div>
      <div v-on:click="switchNextMonth">
        <md-button class="md-icon-button">
          <md-icon>navigate_next</md-icon>
        </md-button>
      </div>
    </div>
  </div>
</template>

<script>
  const date = new Date();

  export default {
    name: 'calendar',
    props: {
      squadInformation: Object,
    },
    data() {
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
      };
    },
    methods: {
      switchPreviousMonth() {
        if (this.month === 0) {
          this.month = 11;
          this.year = this.year - 1;
        } else {
          this.month = this.month - 1;
        }
      },
      switchNextMonth() {
        if (this.month === 11) {
          this.month = 0;
          this.year = this.year + 1;
        } else {
          this.month = this.month + 1;
        }
      },
      calculateMonth(month) {
        let returnMonth;
        if (month === 12) {
          returnMonth = 0;
        } else if (month === -1) {
          returnMonth = 11;
        } else {
          returnMonth = month;
        }

        return returnMonth;
      },
      calculateYearForPreviousMonth(month, year) {
        let returnYear;
        if (month === 0) {
          returnYear = year - 1;
        } else {
          returnYear = year;
        }

        return returnYear;
      },
      calculateYearForNextMonth(month, year) {
        let returnYear;
        if (month === 11) {
          returnYear = year + 1;
        } else {
          returnYear = year;
        }

        return returnYear;
      },
      getDaysInMOnth(year, month) {
        return 33 - new Date(year, month, 33).getDate();
      },
    },
    computed: {
      daysInCurrentMonth() {
        return this.getDaysInMOnth(this.year, this.month);
      },
      firstDayInMonth() {
        return new Date(this.year, this.month, 1).getDay();
      },
      lastDayInMonth() {
        return new Date(this.year, this.month, this.daysInCurrentMonth).getDay();
      },
      daysArr() {
        this.arr.length = 0;
        let firstDayInMonth;
        if (this.firstDayInMonth === 0) {
          firstDayInMonth = 7;
        } else {
          firstDayInMonth = this.firstDayInMonth;
        }

        for (let i = 0; i < firstDayInMonth - 1; i += 1) {
          this.arr.push({ // eslint-disable-next-line no-mixed-operators
            day: this.getDaysInMOnth(this.year, this.month - 1) - firstDayInMonth + 2 + i,
            days: this.getDaysInMOnth(this.year, this.month - 1),
            month: this.calculateMonth(this.month - 1),
            isCurrentMonth: false,
            year: this.calculateYearForPreviousMonth(this.month, this.year),
            isDayShift: false,
            isNightShift: false,
          });
        }

        for (let i = 1; i <= this.daysInCurrentMonth; i += 1) {
          this.arr.push({
            day: i,
            days: this.getDaysInMOnth(this.year, this.month),
            month: this.month,
            year: this.year,
            isCurrentMonth: true,
            isDayShift: false,
            isNightShift: false,
          });
        }

        let lastDayInMonth;
        if (this.lastDayInMonth === 0) {
          lastDayInMonth = 7;
        } else {
          lastDayInMonth = this.lastDayInMonth;
        }
        for (let i = 1; i <= 7 - lastDayInMonth; i += 1) {
          this.arr.push({
            day: i,
            days: this.getDaysInMOnth(this.year, this.month + 1),
            month: this.calculateMonth(this.month + 1),
            year: this.calculateYearForNextMonth(this.month, this.year),
            isCurrentMonth: false,
            isDayShift: false,
            isNightShift: false,
          });
        }

        const timeYear = this.squadInformation.year;
        const timeMonth = this.squadInformation.month;
        const dayTimeDay = this.squadInformation.day;
        const nightTimeDay = this.squadInformation.day + 1;
        this.arr.map((item) => {
          const dayTimeOfTable = +new Date(timeYear, timeMonth, dayTimeDay) / (3600 * 24 * 1000);
          const dayCurrent = +new Date(item.year, item.month, item.day) / (3600 * 24 * 1000);
          const nightTimeOfTable = +new Date(timeYear, timeMonth, nightTimeDay) / (3600 * 24 * 1000);

          if (dayCurrent >= dayTimeOfTable) { // eslint-disable-next-line no-param-reassign
            item.isDayShift = (dayCurrent - dayTimeOfTable) % 4 === 0;
          } else { // eslint-disable-next-line no-param-reassign
            item.isDayShift = (dayTimeOfTable - dayCurrent) % 4 === 0;
          }

          if (dayCurrent >= nightTimeOfTable) { // eslint-disable-next-line no-param-reassign
            item.isNightShift = (dayCurrent - nightTimeOfTable) % 4 === 0;
          } else { // eslint-disable-next-line no-param-reassign
            item.isNightShift = (nightTimeOfTable - dayCurrent) % 4 === 0;
          }

          return this.arr;
        });

        return this.arr;
      },
    },
  };
</script>
