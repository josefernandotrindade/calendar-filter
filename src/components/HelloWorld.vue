<template>
  <div class="calendar">
    <cal-month v-for="m in months" :month="m" :year="year" :key="m"/> 
  </div>
</template>

<script>
import CalMonth from "./CalMonth.vue";

export default {
  name: "HelloWorld",
  components: {
    CalMonth
  },
  data: function() {
    return {
      year: {
        type: Number,
        default: 0
      },
      months: {
        type: Array,
        default: []
      }
    };
  },
  created: function() {
    var today = new Date();
    this.months = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11];
    this.year = today.getFullYear();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calendar {
  display: flex;
  justify-content: center;
  align-items: stretch;
  flex-wrap: wrap;
  font-size: 12px;
  margin: 0 auto;
  width: 100%;
  clear: both;
}

.month {
  align-content: space-between;
  flex-grow: 0;
}

@media screen and (min-width: 300px) {
  .calendar {
    width: 300px;
  }
}

@media screen and (min-width: 600px) {
  .calendar {
    width: 600px;
  }
}

@media screen and (min-width: 900px) {
  .calendar {
    width: 900px;
  }
}

@media screen and (min-width: 1200px) {
  .calendar {
    width: 1200px;
  }
}
</style>
