<script>
    import { onMount } from 'svelte';

    export let summary;
    export let days;
    let isDataFormatted = false;
    let formattedData;

    function prepareSummary() {
        formattedData = summary.reduce((acc, curr) => {
            if (Object.keys(acc).includes(curr.title)) {
                acc[curr.title] = [...acc[curr.title], curr];
            } else {
                acc[curr.title] = [curr];
            }
            return acc;
        }, {});
        isDataFormatted = true;
        console.log(formattedData);
    }

    onMount(() => {
        console.log("onMount");
        prepareSummary();
    });
</script>

<style></style>

<h2>Summary</h2>
{#if isDataFormatted}
    {formattedData}
{/if}