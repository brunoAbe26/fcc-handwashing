<script>
    import ProgressBar from "./ProgressBar.svelte";
    import { createEventDispatcher } from "svelte";

    const totalSeconds = 20;
    let secondLeft = totalSeconds;
    let isRunning = false;
    $: progress = ((totalSeconds - secondLeft) / totalSeconds) * 100;
    const dispatch = createEventDispatcher();
    function startTimer() {
        isRunning = true;
        const timer = setInterval(() => {
            secondLeft -= 1;
            if (secondLeft === 0) {
                clearInterval(timer);
                isRunning = false;
                secondLeft = totalSeconds;
                dispatch("end");
            }
        }, 1000);
    }
</script>

<div bp="grid">
    <h2 bp="offset-5@md 4@md 12@sm">Second left {secondLeft}:</h2>
</div>

<ProgressBar {progress} />

<div bp="grid">
    <button
        disabled={isRunning}
        on:click={startTimer}
        bp="offset-5@md 4@md 12@sm"
        class="start">Start</button
    >
</div>

<style>
    h2 {
        margin: 0;
    }
    .start {
        background-color: rgb(154, 73, 73);
        width: 100%;
        margin: 10px 0;
    }
    .start[disabled] {
        background-color: rgb(194, 194, 194);
        cursor: not-allowed;
    }
</style>
