<template>
    <button class="actionBtn" id="go" v-if="gameVar.show" @click="go()">Go</button>
    <button id="stop" class="actionBtn" v-if="!gameVar.show" @click="stop()">Stop</button>
</template>
<script>
    export default{
        data() {
            return{
            }
        },
        props:{
            gameVar: Object
        },
        methods: {
    go() {
      this.gameVar.details = "Pay attention. Click stop when the color changes.";
      this.gameVar.show = !this.gameVar.show;
      let interval = Math.floor(Math.random() * (5000 - 2000 + 1) + 2000);
      this.gameVar.timeout = setTimeout(() => {
        this.gameVar.isActive = false;
        this.gameVar.timeStart = new Date().getTime();
      }, interval);
      this.gameVar.timeStart = 0;
    },
    stop() {
      this.gameVar.isActive = true;
      this.gameVar.show = !this.gameVar.show;
      if (this.gameVar.timeStart == 0) {
        this.gameVar.details = "Too quick... Try again!";
        clearTimeout(this.gameVar.timeout);
      } else {
        this.gameVar.timeStop = new Date().getTime();
        this.gameVar.diff = this.gameVar.timeStop - this.gameVar.timeStart;
        this.gameVar.score = (this.gameVar.diff / 1000).toFixed(2);
        if (this.gameVar.firstRun === 1) {
          this.gameVar.highscore = this.gameVar.score;
          this.gameVar.firstRun++;
          this.gameVar.details = `You've set a new high score: ${this.gameVar.highscore} seconds!`;
        } else if (this.gameVar.score < this.gameVar.highscore) {
          this.gameVar.highscore = this.gameVar.score;
          this.gameVar.details = `You've set a new high score: ${this.gameVar.highscore} seconds!`;
        } else {
          this.gameVar.details = `Your time was: ${this.gameVar.score} seconds. Try again!`;
        }
        console.log(this.gameVar.score);
      }
    },
  },
    }
    
</script>