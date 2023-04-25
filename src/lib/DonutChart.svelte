<script>
    import DonutArc from "./DonutArc.svelte";
    import Tooltip from "./Tooltip.svelte";
    import * as d3 from "d3";
    import HiddenArc from "./HiddenArc.svelte";

    export let dataset;
    export let innerRadius;
    export let outerRadius;
    export let colorScale;
    export let weekendColorScale;
    export let label = "no"; 

    let hoveredData;

    const createPieData = (data) => {
        // const pie = d3.pie().value(1);
        const pie = d3.pie()        
                        .startAngle(Math.PI * -1/2)
                        .endAngle(Math.PI * 1/2)
                        .padAngle(0.02)
                        .value(1);
        const arcGenerator = d3
            .arc()
            .innerRadius(innerRadius)
            .outerRadius(outerRadius);

        return pie(data).map((d, i) => {
            return {
                data: d.data,
                index: i,
                path: arcGenerator(d),
                fill: colorScale(d.data.category),
                centroid: arcGenerator.centroid(d),
            };
        });
    }        

    const pieData = createPieData(dataset);

    // function handleHover(d, event) {
    //     hoveredData = d;
    // }
</script>

<g>
    {#each pieData as d, i}                
        <DonutArc 
            data={d} 
            {colorScale} 
            {weekendColorScale} 
            {label}
            on:hover    
            on:leave    
        />

        <HiddenArc 
            data={d} 
            index={i} 
            {label}           
        />

        <!-- {#if label="yes"}
        <ChartLabel data={d} index={i}/>         
        {/if} -->
    {/each}

</g>
