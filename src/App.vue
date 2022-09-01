<template>
<body :class="[gameVar.isActive ? 'blue' : 'green']">
    <div id="container">
        <ActionBtn :gameVar="gameVar">
        </ActionBtn>
        <Score :gameVar="gameVar">
        </Score>
    </div>
</body>
</template>

<script>
import ActionBtn from './components/ActionBtn.vue'
import Score from './components/Score.vue'
export default {
    components: {
        ActionBtn,
        Score
    },
    data() {
        return {
            gameVar: {
                show: true,
                isActive: true,
                timeStart: 0,
                timeStop: 0,
                diff: 0,
                score: 0,
                highscore: "No highscore yet.",
                details: "Click Go to test your reaction time!",
                firstRun: 1,
                timeout: 0,
            }
        };

    },

};
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

.blue {
    background-color: dodgerblue;
}

.green {
    background-color: green;
}

#details {
    margin-bottom: 40px;
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
