<template>
  <div class="content">
    <!-- agoDayHide='1517483961' -->
    <!-- futureDayHide="1526054400" -->
    <div class="top">
      <input type="text" @change="changeDateInput" v-model="year">
      <input type="text" @change="changeDateInput" v-model="month">
    </div>
    <Calendar
      ref="Calendar"
      :signDay="arr"
      v-on:isToday="clickToday"
      agoDayHide="1530115221"
      v-on:choseDay="clickDay"
      @breakSign="supplementSignIn"
      v-on:changeMonth="changeDate"
    ></Calendar>
  </div>
</template>

<script>
import Calendar from '../vue-calendar-component/index';
// import Calendar from "vue-calendar-component";
export default {
  data() {
    return {
      arr: [],
      break: ['2019/4/15', '2019/4/17', '2019/4/28'],
      gift: ['2019/4/3', '2019/4/6', '2019/4/29'],
      year: '',
      month: ''
    };
  },
  components: {
    Calendar
  },
  methods: {
    init() {
      const days = 30
      let arrs = []
      for (let i = 1; i <= days; i++) {
        arrs.push({
          date: this.format(new Date(), i),
          signDay: true,
          breakSign: this.break.includes(this.format(new Date(), i)),
          gift: this.gift.includes(this.format(new Date(), i))
        });
      }
      this.arr = arrs
    },
    format(date, index) {
      date = new Date(date);
      return `${date.getFullYear()}/${date.getMonth() + 1}/${index}`;
    },
    supplementSignIn(item) {
      this.$toast('补签成功');
      this.break = this.break.filter(i => i !== item.date)
      this.init()
    },
    changeDateInput() {
      this.$refs.Calendar.ChoseMonth(`${this.year}/${this.month}`)
    },
    clickDay(data) {
      console.log("选中了", data); //选中某天
      this.$toast("选中了" + data);
    },
    clickToday(data) {
      console.log("跳到了本月今天", data); //跳到了本月
    },
    changeDate(data) {
      this.$toast("切换到的月份为" + data);
      console.log("左右点击切换月份", data); //左右点击切换月份
    }
  },
  created() {
    this.init()
    this.year = new Date().getFullYear()
    this.month = new Date().getMonth() + 1
  },
  mounted() {
    this.changeDateInput()
  }
};
</script>

<!-- Add "scoped " attribute to limit CSS to this component only -->
<style scoped>
h3 {
  text-align: center;
  width: 90%;
  margin: auto;
}

.div {
  margin: auto;
  width: 220px;
  height: 44px;
  line-height: 44px;
  background: #0fc37c;
  color: #fff;
  font-size: 17px;
  text-align: center;
  margin-top: 20px;
}

.wh_container >>> .mark1 {
  /* background-color: orange; */
}

.wh_container >>> .mark2 {
  /* background-color: blue; */
}
.wh_content_item > .wh_isMark {
  /* background: orange; */
}
.wh_container >>> .wh_content_all {
  /* background-color: red; */
}
</style>