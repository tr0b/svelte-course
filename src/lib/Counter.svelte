<script>
    export let maxCount = 10;
    export let initialCount;
    let count = initialCount;
    $: counterText = `Count is now ${count}`;

    const increment = () => {
        if (count === maxCount) return;
        
        count += 1;
    };
</script>

<h2>{counterText}</h2>

<button on:click={increment}>
    Count is now: {count}
</button>
