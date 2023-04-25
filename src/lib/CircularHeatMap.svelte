<script>
    import * as d3 from "d3";
    import DonutChart from "./DonutChart.svelte";
    import ScoreLabels from "./ScoreLabels.svelte";
    import Tooltip from "./Tooltip.svelte";

    export let inputData;
    let width = 1000;
    let height = 600; 
    let hoveredData;

    const scoreCategories = ["styling",	"acceleration",	"handling",	"fun_factor",	"cool_factor",	"features",	"comfort",	"quality",	"practicality",	"value"]; 
    const categoryLabels = ["styling",	"acceleration",	"handling",	"fun factor",	"cool factor",	"features",	"comfort",	"quality",	"practicality",	"value"]; 
    const scores = d3.range(1, 11);

    const rowHeight = 32,
          initialRadius = 120;

    let summaryData = [];    

    d3.range(1, 11).forEach((d, i) => {
        scoreCategories.forEach((cat, j) => {
            summaryData.push(
            {
                category: cat,
                label: categoryLabels[j],
                type: j < 5 ? "weekend": "daily",
                score: d,
                value: 0
            })
        })
    });

    $inputData.forEach((d, i) => {
        scoreCategories.forEach(category => {
            summaryData.forEach(sd => {
                    if(sd.category === category && sd.score === d[category]) {
                        sd.value++;
                    }
                })
            })
    });
    
    // const categories = [...new Set(summaryData.map(d => d.category))];

    // const textColorScale = d3.scaleLinear()
    //     .domain(d3.extent(summaryData, d => d.value))
    //     .range(["green", "white"]);



    const colorScale = d3.scaleLinear()
        .domain(d3.extent(summaryData, d => d.value))
        .range(["white", "#3bb371"]);
    const weekendColorScale = d3.scaleLinear()
        .domain(d3.extent(summaryData, d => d.value))
        .range(["white", "#f08080"]);          

    // const color = d3.scaleOrdinal(d3.schemeCategory10);

    console.log(summaryData);

    // const dataset = summaryData.filter(d => d.score === 1)    

    function handleMouseOver(event) {
          hoveredData = event.detail.data;
    }
        
    function handleMouseLeave(event) {
          hoveredData = null;
    }
    


    // const angleGen = d3.pie()
        // .startAngle(Math.PI * -1/2)
        // .endAngle(Math.PI * 1/2)
        // .padAngle(0)
        // .value(1);
    
    // const chartData = angleGen(dataset);

    // const arcGen = d3.arc()
    //     .innerRadius(initialRadius + rowHeight)
    //     .outerRadius(initialRadius + rowHeight * 2);      


</script>

<div class="circular-heatmap">
    <svg {width} {height}>
        <g style="transform: translate({width/2}px, {height/1.1}px)">
            <!-- {#each pieData as d, i}                
                <DonutArc data={d} {colorScale} {weekendColorScale}/>
            {/each} -->
            {#each scores as score, index}
                <DonutChart 
                    dataset={summaryData.filter(sd => sd.score === score)} 
                    innerRadius={initialRadius + rowHeight * index} 
                    outerRadius={(initialRadius + rowHeight * index) + rowHeight - 4} 
                    {colorScale} 
                    {weekendColorScale} 
                    on:hover={handleMouseOver}  
                    on:leave={handleMouseLeave}  
                    
                />  
                    
                <ScoreLabels {index} {rowHeight} type="left" />
                <ScoreLabels {index} {rowHeight} type="right" />

            {/each}
            <DonutChart 
                dataset={summaryData.filter(sd => sd.score === 1)} 
                innerRadius={initialRadius + rowHeight * (scores.length)} 
                outerRadius={(initialRadius + rowHeight * (scores.length)) + rowHeight} 
                {colorScale} 
                {weekendColorScale} 
                label="yes"/>    
        </g>
        <g>
            <text
                class="total-ban"
                x={width/2}
                y={height-92}
            >
                {$inputData.length}
            </text>
            <text
                class="total-ban-subtext"
                x={width/2}
                y={height-56}
            >
                TOTAL CARS
            </text>
            <text
                class="score-axis-label"
                x={width/5}
                y={height-4}
            >
                score
            </text>
        
            <text
                class="score-axis-label"
                x={width/1.3}
                y={height-4}
                >
                score
            </text>

    </g>
    </svg>
    <p class="chart-title"># of Cars by Score and by different Categories (<span class="weekend-legend-text">weekend</span> vs <span class="daily-legend-text">daily</span>) </p>

    {#if hoveredData}
        <Tooltip data={hoveredData} {width} {height}/>
    {/if}  
</div>

<style>
    .circular-heatmap {
        position: relative;
    }


    svg {
        /* border: solid 1px; */
    }

    .total-ban {
        text-anchor: middle;
        font-size: 48px;
        font-weight: bold;
    }
    .total-ban-subtext {
        text-anchor: middle;
        font-size: 20px;
        font-weight: 400;
        fill: gray;
    }
    .score-axis-label {
        font-size: 12px;
        text-transform: uppercase;
        letter-spacing: 1px;
    }

    .chart-title {
        padding-top: 8px;
        text-anchor: middle;
        /* text-transform: uppercase; */
        font-size: 16px;
        margin: 0 auto;
        text-align: center;
        color: gray;
    }

    .weekend-legend-text {
        color: lightcoral;
        font-weight: bold;
    }
    .daily-legend-text {
        color: mediumseagreen;
        font-weight: bold;
    }
</style>