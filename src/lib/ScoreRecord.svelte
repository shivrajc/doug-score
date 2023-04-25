<script>
    import * as d3 from "d3";
    import { fade, fly } from 'svelte/transition';

    export let rowData;

    const scoreCategories = ["styling",	"acceleration",	"handling",	"fun_factor",	"cool_factor",	"features",	"comfort",	"quality",	"practicality",	"value"]; 
    const weekendCategories = ["styling",	"acceleration",	"handling",	"fun_factor",	"cool_factor"]; 
    const dailyCategories = ["features",	"comfort",	"quality",	"practicality",	"value"]; 
</script>

<div class="score-row">
<!-- <div class="score-row" in:fly="{{ y: 60, duration: 100 }}" out:fade> -->
    <div class="row-header">
        <div class="row-header-name">
            <span class="row-header-make">{rowData.make}</span>
            <span class="row-header-model">{rowData.model}</span>
        </div>
        <div class="row-header-subtext">
            <span class="row-header-subtext-label">
                YEAR: <span class="row-header-subtext-value">{rowData.year}</span> 
            </span>
            <span class="row-header-subtext-label">
                COUNTRY: <span class="row-header-subtext-value">{rowData.vehicle_country}</span> 
            </span>
            <span class="row-header-subtext-label">
                <span class="row-header-subtext-value"><a href="{rowData.video_link}" target="_blank">review</a></span> 
                <!-- <span class="row-header-subtext-value"><a href="{rowData.video_link}">&#128279</a></span>  -->
            </span>
        </div>
    </div>
    
    <div class="total-score">
        <p class="total-score-text">{rowData.dougscore}</p>
        <p class="total-score-subtext">
            <span class="total-score-subtext-weekend">{rowData.weekend_total}</span>
            <span class="total-score-subtext-daily">{rowData.daily_total}</span>
        </p>
    </div>
    
    <div class="score-columns">
        {#each weekendCategories as dc, index}        
            <div class="column">
                {#each d3.range(1, 11) as score}
                    <div class="score-bar weekend-bar" class:weekend-filled={score <= rowData[weekendCategories[index]]}></div>
                {/each}
            </div>
            {/each}
        {#each dailyCategories as dc, index}        
            <div class="column daily-column ">
                {#each d3.range(1, 11) as score}
                    <div class="score-bar daily-bar" class:daily-filled={score <= rowData[dailyCategories[index]]}></div>
                {/each}
            </div>
            {/each}
    </div>
</div>

<style>
    .score-row {
        display: flex;
        justify-content: space-between;
        height: 80px;
        margin-bottom: 8px;
        /* box-shadow: rgba(0, 0, 0, 0.12) 0px 1px 3px, rgba(0, 0, 0, 0.24) 0px 1px 2px; */
        background-color: white;
        border: 1px solid hsl(140, 4%, 88%);
        border-radius: 8px;
        padding: 20px;
    }

    .score-columns {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-grow: 1;
    }

    .row-header {
        width: 320px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: left;
        text-align: left;
        gap: 8px;
        /* padding: 20px 8px 20px 20px; */
    }

    .row-header-name {
        font-size: 18px;
    }

    .row-header-make {
        font-weight: bold;
    }

    .row-header-model {
        font-weight: 400;
        /* color: rgb(175, 158, 3); */
    }

    .row-header-subtext {
        font-size: 12px;
        display: flex;
        justify-content: left;
        align-items: center;
        gap: 20px        
    }

    .row-header-subtext-label {
        font-weight: 400;
        color: gray;
    }

    .row-header-subtext-value {
        font-weight: 500;
        color: black;
    }

    .row-header-subtext-value a {
        font-weight: 500;
        /* text-decoration: none; */
        color: cornflowerblue;        
    }

    .row-header-subtext-value a:visited {
        color: cornflowerblue;        
    }

    .total-score {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
        width: 160px;
    }

    .total-score-text {
        font-size: 28px;
        font-weight: bold;

    }

    .total-score-subtext {
        font-size: 16px;
        font-weight: 500;
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 8px;
    }

    .total-score-subtext-weekend {
        color: lightcoral;
    }

    .total-score-subtext-daily {
        color: mediumseagreen;
    }





    .score-bar {
        flex-grow: 1;
        width: 4px;
        height: 16px;
        transform: skewX(-20deg);
        background-color: rgb(222, 220, 220);        
    }

    .column {
        /* flex-grow: 1; */
        width: 104px;
        display: flex;
        justify-content: center;
        align-items: center; 
        gap: 1px;       
        padding: 20px;
    }

    .weekend-bar {
        /* border: 1px solid lightcoral ; */
    }
    
    .daily-bar {
        /* border: 1px solid mediumseagreen ; */
    }
    
    .weekend-filled {
        /* border: 1px solid lightcoral ; */
        background-color: lightcoral;
    }
    
    .daily-filled {
        /* border: 1px solid mediumseagreen ; */
        background-color: mediumseagreen;
    }
</style>