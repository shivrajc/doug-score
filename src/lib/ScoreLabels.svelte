<script>
    export let index;
    export let rowHeight;
    export let type;
</script>

{#if type === "left"}
    <circle
        class="score-dot"
        cx={index * rowHeight - 422}
        cy="22"
        r="12"
    >
    </circle>
    <text 
        class="score-label"
        x={index * rowHeight - 422}
        y="26"
        >
        {10 - index}
    </text>    
{:else}
    <circle 
        class="score-dot"
        cx={index * rowHeight + 134}
        cy="22"
        r="12"
    >
    </circle>
    <text 
        class="score-label"
        x={index * rowHeight + 134}
        y="26"
        >
    {index + 1}
    </text>
{/if}

<style>
    .score-label {
        font-size: 12px;
        font-weight: 500;
        /* fill: black; */
        text-anchor: middle;
    }

    .score-dot {
        fill: #e4e6e4;
        /* stroke: lightgray; */
    }
</style>