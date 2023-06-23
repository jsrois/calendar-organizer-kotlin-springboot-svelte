<script>
    export let day;
</script>

{#if day}
    <div class="day">{day.monthDay + 1}</div>
{:else }
    <div class="day empty"></div>
{/if}

<style>
    .day {
        width: 100px;
        height: 100px;
        border: 1px solid black;
    }

    .day.empty {
        background-color: lightgray;
    }
</style>
