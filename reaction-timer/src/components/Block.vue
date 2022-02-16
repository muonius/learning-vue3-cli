
<template>
  <!-- type vue in vsc will populate a default .vue template -->
  <div class="block" v-if="showBlock" @click="stopTimer">Click me</div>
</template>

<script>
export default {
  props: ["delay"],

  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0,
    };
  },

  //mounted() is a lifecyle hook, it will only fire when it's mounted to the DOM
  mounted() {
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay);
  },

  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
      }, 10);
    },
    stopTimer() {
      clearInterval(this.timer);
      //   console.log(this.reactionTime);
      this.$emit("end", this.reactionTime);
      // the first parameter in $emit is just a name you can call it whatever you like
      // the second parameter is the data to be sent along to the main element
    },
  },

  //   updated() {
  //     //updated() is a lifecycle hook. It gets fired when data is updated
  //     console.log("data is updated");
  //   },
  //   unmounted() {
  //     //this fires when component is unmounted
  //   },
};
</script>

<style>
.block {
  width: 400px;
  border-radius: 20px;
  background: #0faf87;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>