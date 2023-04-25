<script>
    import * as d3 from "d3";
    export let data;
    export let index;
    export let label = "no";

    const categoryScale = d3.scaleOrdinal()
                    .domain(["weekend", "daily"])
                    .range(["#f08080", "#3bb371"]);

    const calculatePath = (d) =>{
        const firstArcSection = /(^.+?)L/;
        let hiddenArc = firstArcSection.exec(d)[1];
        return  hiddenArc.replace(/,/g, " ");
    }

</script>


<!-- svelte-ignore a11y-mouse-events-have-key-events -->
<path        
    class="hiddenArcs"
    id={label === "yes" ? `hiddenArc-${data.data.category}-${index}` : `hiddenArc-${data.data.score}-${index}`}
    d={calculatePath(data.path)}
    fill="none"   
/>

<text
    class="donutText"
    class:chart-labels={label === "yes"}
    dy="20"
    fill={label === "yes" ? categoryScale(data.data.type) : "black"}
    >
    <textPath
        startOffset="50%"
        text-anchor="middle"
        xlink:href={label === "yes" ? `#hiddenArc-${data.data.category}-${index}` : `#hiddenArc-${data.data.score}-${index}`}
    >
        {label === "yes" ? data.data.label : data.data.value}
    </textPath>
</text>

<style>
    path {
        pointer-events: none;
    }

    .donutText {
        font-size: 13px;
        pointer-events: none;
    }

    .chart-labels {
        font-size: 14px;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: 500;
        pointer-events: none;
    }
</style>