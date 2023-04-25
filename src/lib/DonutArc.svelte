<script>
    import { createEventDispatcher } from 'svelte';
    import Tooltip from "./Tooltip.svelte";
    export let data;
    export let colorScale;
    export let weekendColorScale;
    export let label;

    const dispatch = createEventDispatcher();
    let hoveredData;

	function forwardHover(event) {
		dispatch('hover', {data});
	}

	function forwardLeave(event) {
		dispatch('leave', {data});
	}


    // function handleHover(chain) {
    //     hoveredData = chain;
    // }
    
    // console.log(hoveredData)
</script>

<!-- svelte-ignore a11y-mouse-events-have-key-events -->
<path
    d={data.path}
    fill={label === "yes" ? "none" : data.index <= 4 ? weekendColorScale(data.data.value) : colorScale(data.data.value)}
    stroke={data.index <= 4 ? "#C38080" : "#7DAC92"}
    stroke-width={label === "yes" ? "0" : "0.2"}
    on:mouseover={forwardHover}
    on:mouseleave={forwardLeave}   
/>

