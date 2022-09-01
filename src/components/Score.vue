<template>
<div id="score">
    <p id="details">{{ gameVar.details }}</p>
    <p class="span-results">
        <b>Your High Score</b>
        <p id="highscore">{{ gameVar.highscore }}</p>
    </p>
</div>
</template>

<script>
export default {
    data() {
        return {}
    },
    props: {
        gameVar: Object
    }
}
</script>
