<script>
    export let data;
    export let index;
    export let label = "no";

    const calculatePath = (d) =>{
        const firstArcSection = /(^.+?)L/;
        let hiddenArc = firstArcSection.exec(d)[1];
        return  hiddenArc.replace(/,/g, " ");
    }
</script>

<!-- {#each data as d,i} -->
    <path
        class="hiddenArcs"
        id={`hiddenArc-${data.data.category}-${index}`}
        d={calculatePath(data.path)}
        fill="none"
    />

    <text
        class="donutText"
        dy="20"
        >
        <textPath
            startOffset="50%"
            text-anchor="middle"
            xlink:href ={`#hiddenArc-${data.data.category}-${index}`}
        >
            {data.data.category}
        </textPath>
    </text>
<!-- {/each} -->

<style>
    .donutText {
        font-size: 12px;
    }
</style>