<template>
  <div class="calendar">
    <cal-month v-for="m in months" :month="m" :year="year" :key="m"></cal-month> 
  </div>
</template>


<script>
import CalMonth from './CalMonth.vue';

export default {
  name: 'HelloWorld',
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
  props: {
    msg: String
  },
  created: function() {
    var today = new Date();
      this.months = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11];
    this.year = today.getFullYear();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calendar {
    display: flex;
    justify-content: space-between;
    align-items: stretch;
    flex-wrap: wrap;
    font-size: 12px;
    margin: 0 auto;
  }
</style>
