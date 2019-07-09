    <template id="html-clock">
      <div class="html-clock">
        <div class="hours">{{ hours | clockMode }}</div>
        <div class="sep">:</div>
        <div class="minutes">{{ minutes | clockMode }}</div>
        <div class="sep2">:</div>
        <div class="seconds">{{ seconds | clockMode }}</div>
        <div class="mode">{{ mode }}</div>
      </div>
    </template>

<script>
export default {
  name: "HtmlClock",
  template: "#html-clock",
  data() {
    return {
      hours: "--",
      minutes: "--",
      seconds: "--",
      mode: "asd"
    };
  },
  filters: {
    clockMode: d => d.toString().padStart(2, "0")
  },
  methods: {
    updateDate() {
      const date = new Date();

      this.hours = date.getHours();
      this.minutes = date.getMinutes();
      this.seconds = date.getSeconds();

      if (this.hours >= 12) {
        this.mode = "PM";
      } else this.mode = "AM";
    },
    startClock() {
      setInterval(this.updateDate, 1000);
    }
  },
  mounted() {
    this.startClock();
  }

}
</script>

<style>
.html-clock {
  font-family: "Orbitron", sans-serif;
  font-size: 150px;
  text-shadow: 5px 5px 10px darkred;
  color: red;
  background: #000;
  width: 1100px;
  padding: 75px;
  border: 30px outset gray;
  box-shadow: 15px 15px 20px black;
  display: grid;
  grid-template-columns: 1fr 0.2fr 1fr 0.2fr 1fr 1fr;
  grid-template-rows: 1fr;
  grid-template-areas: "hours sep minutes sep2 seconds mode";
}

.hours {
  grid-area: hours;
}

.minutes {
  grid-area: minutes;
}

.sep {
  grid-area: sep;
}
.sep2 {
  grid-area: sep2;
}

.seconds {
  grid-area: seconds;
}

.mode {
  grid-area: mode;
  margin-top: 40px;
  text-align: center;
}

/* .html-clock .hours,
.html-clock .minutes,
.html-clock .seconds {
  display: inline-block;
  min-width: 150px;
} */
.html-clock > .sep {
  text-shadow: 2px 2px 5px darkred;
}
.html-clock .mode {
  font-size: 50px;
  padding-left: 50px;
}


</style>
