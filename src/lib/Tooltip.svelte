<script>
    export let data;
    export let width;
    export let height

    console.log("Hovered")
</script>

<div class="tooltip" style="position:absolute; top:{data.centroid[1] + (height / 1.2)}px; left:{data.centroid[0] + (width / 2) + 120}px">
<!-- <div class="tooltip" style="position:absolute; top:{100}px; left:{100}px"> -->
    <p><span class="tooltip-header">Category:</span> {data.data.label}</p>
    <p><span class="tooltip-header">Score:</span> {data.data.score}</p>
    <p><span class="tooltip-header"># of Cars:</span> {data.data.value}</p>
</div>

<style>
    .tooltip {
        background-color: white;
        opacity: 0.96;
        padding: 12px;
        /* border: 1px solid lightgray; */
        border-radius: 8px;
        pointer-events: none;
        transition: top 300ms, left 300ms;
        text-align: left;
        box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px, rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
    }

    span {
        font-weight: 400;
        color: gray;
        text-transform: none;
    }

    p {
        font-weight: bold;
        text-transform: capitalize;
    }
</style>