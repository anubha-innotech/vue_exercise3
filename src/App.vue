<template>

  <body v-bind:style='{ "background-color": (isActive ? "dodgerblue" : "green") }'>
    <div id="container">
      <button class="actionBtn" id="go" v-if="show" @click="go()">Go</button>
      <button id="stop" class="actionBtn" v-if="!show" @click="stop()">Stop</button>
      <div id="score">
        <span id="details">{{details}}</span>
        <br>
        <br>
        <span class="span-results">
          <b>Your High Score</b>
          <p id="highscore">{{highscore}}</p>
        </span>
      </div>
    </div>
  </body>
</template>
<script>
export default {
  data() {
    return {
      show: true,
      isActive: true,
      timeStart:0,
      timeStop:0,
      diff:0,
      score: 0,
      highscore:"No highscore yet.",
      details: "Click Go to test your reaction time!",
      firstRun:1,
      timeout:0,
    }
  },
  methods: {
    go() {
      this.details = "Pay attention. Click stop when the color changes."
      this.show = !this.show;
      let interval = Math.floor(Math.random() * (5000 - 2000 + 1) + 2000);
       this.timeout = setTimeout(() => {
        this.isActive = false;
        this.timeStart = new Date().getTime();
      }, interval);
      this.timeStart = 0;
    },
    stop() {
      this.isActive = true;
      this.show = !this.show;
      if(this.timeStart == 0 ){
        this.details = "Too quick... Try again!";
        clearTimeout(this.timeout);
      }
      else{
        this.timeStop = new Date().getTime();
        this.diff = this.timeStop - this.timeStart;
        this.score = (this.diff/1000).toFixed(2);
        if(this.firstRun === 1){
          this.highscore = this.score;
          this.firstRun++
          this.details = `You've set a new high score: ${this.highscore} seconds!`
        }
        else if(this.score < this.highscore){
          this.highscore = this.score
          this.details = `You've set a new high score: ${this.highscore} seconds!`
        }
        else{
          this.details = `Your time was: ${this.score} seconds. Try again!`
        }
        console.log(this.score);
      }
    }
  },
}

</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}

#container {
  display: flex;
  height: 100vh;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.actionBtn,
#score {
  height: 150px;
  width: 60vw;
  border: 1px solid transparent;
  border-radius: 15px;
  margin: 20px;
}

.actionBtn {
  color: white;
  font-size: 3em;
  cursor: pointer;
}

#go {
  background-color: mediumseagreen;
}

#stop {
  background-color: tomato;
}

#score {
  background-color: #d9edf7;
  padding: 10px 25px 10px 25px;
  font-size: 1.5em;
}
</style>
