<script>
    export let title;
    let exercise = {
        activity: "",
        sets: 4,
        reps: 10
    };
    let exercises = [];

    function handleSubmit() {
        exercises = [...exercises, { ...exercise }];
        console.log({ exercises });
    }
</script>

<style></style>

<div>
    <h2>{title}</h2>
    <form on:submit|preventDefault={handleSubmit}>
        <div>
            <label for="activity">Activity</label>
            <input type="text" id="activity" bind:value={exercise.activity} />
        </div>
        <div>
            <label for="sets">Sets</label>
            <input type="number" id="sets" bind:value={exercise.sets} />
        </div>
        <div>
            <label for="reps">Reps</label>
            <input type="number" id="reps" bind:value={exercise.reps} />
        </div>
        <button type="submit">Add exercise</button>
        <div>
            <ul>
                {#each exercises as ex}
                    <li>{ex.activity} : {ex.sets} sets of {ex.reps}</li>
                {/each}
            </ul>
        </div>
    </form>
</div>