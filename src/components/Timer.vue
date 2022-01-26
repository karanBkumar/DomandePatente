<template>
  <div v-if="this.countdown > 0"><h1>{{ formatedCountdown }}</h1></div>
  <div v-else>
    <p>Tempo esaurito</p>
  </div>
</template>

<script>
import * as moment from "moment";
import "moment-duration-format";

export default {
  data(){
    return {
      countdown: 60 * 20, // 1 min * 20
    };
  },
  mounted(){
      const stopCountdown = setInterval(() => {
        this.countdown -= 1;
        if (!this.countdown)
        {
          clearInterval(stopCountdown)
          this.$emit("inputChange");
        }
      }, 1000);
    },
  computed: {
    formatedCountdown() {
      return moment.duration(this.countdown, "seconds").format("m:ss");
    },
  },
};
</script>