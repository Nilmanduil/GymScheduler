<script>
    import TrainingDayDetails from './TrainingDayDetails.svelte';
    import TrainingWeekSummary from "./TrainingWeekSummary.svelte";

    const nbOfDays = [
        {id: 1, text: "One day", value: [1]},
        {id: 2, text: "Two days", value: [1, 2]},
        {id: 3, text: "Three days", value: [1, 2, 3]},
        {id: 4, text: "Four days", value: [1, 2, 3, 4]},
        {id: 5, text: "Five days", value: [1, 2, 3, 4, 5]},
        {id: 6, text: "Six days", value: [1, 2, 3, 4, 5, 6]},
        {id: 7, text: "Seven days", value: [1, 2, 3, 4, 5, 6, 7]}
    ];

    let summary = [];
    let isSummaryReady = false;
    let nbDaysTrainingPerWeek;

    function handleNewExercise(event) {
        console.log("on:add-exercise", event);
        summary = [...summary, event.detail];
        isSummaryReady = false;
    }

    function generateSummary() {
        isSummaryReady = true;
    }
</script>

<style>
    .all-days {
        border: solid 2px purple;
        margin: 5px;
    }

    .training-day-details {
        border: solid 2px green;
        margin: 5px;
    }
</style>

<div>
    <form>
        <select bind:value={nbDaysTrainingPerWeek}>
            {#each nbOfDays as day (day.id)}
                <option value={day}>{day.text} per week</option>
            {/each}
        </select>
    </form>
    {JSON.stringify(nbDaysTrainingPerWeek)}
</div>
{#if nbDaysTrainingPerWeek}
    <div class="all-days">
        {#each nbDaysTrainingPerWeek.value as dayNumber, i}
            <div class="training-day-details">
                <TrainingDayDetails title={`Day ${++i}`} on:add-exercise={handleNewExercise} />
            </div>
        {/each}
    </div>
    {#if isSummaryReady}
        <TrainingWeekSummary {summary} days={nbDaysTrainingPerWeek.value.length} />
    {/if}
    <button on:click={generateSummary}>Generate summary</button>
{/if}