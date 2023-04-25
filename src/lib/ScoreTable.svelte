<script>
    import { createEventDispatcher } from "svelte";
    import Search from "./Filters/Search.svelte";
    import ScoreRecord from "./ScoreRecord.svelte";
    export let data;

    export let sortColumn;
    export let sortOrder;

    const dispatch = createEventDispatcher();

    $: sortOrderReversed = sortOrder === 'desc' ? 'asc' : 'desc';

    // let searchTerm;

    function handleSort(sort, event) {
        dispatch('sort', sort)
    }


</script>



<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="table-header">
    <div class="row-header">Car Make/Model</div>
    <div class="total-score-header">
        <p class="total-score-name" on:click={() => handleSort({sortColumn:'dougscore', sortOrder: sortOrderReversed})}>
            dougscore 
            <span class="sort-asc-icon sort-icon" style="display: {sortColumn === 'dougscore' && sortOrder === 'asc' ? 'unset' : 'none'}">&#8593;</span>
            <span class="sort-desc-icon sort-icon" style="display: {sortColumn === 'dougscore' && sortOrder === 'desc' ? 'unset' : 'none'}">&#8595;</span>
        </p>
        <p>
            <span class="weekend-header" on:click={() => handleSort({sortColumn:'weekend_total', sortOrder: sortOrderReversed})}>
                weekend
                <span class="sort-desc-icon sort-icon" style="display: {sortColumn === 'weekend_total' && sortOrder === 'desc' ? 'unset' : 'none'}">&#8595;</span>
                <span class="sort-asc-icon sort-icon" style="display: {sortColumn === 'weekend_total' && sortOrder === 'asc' ? 'unset' : 'none'}">&#8593;</span>
            </span>
            <span>|</span>
            <span class="daily-header"  on:click={() => handleSort({sortColumn:'daily_total', sortOrder: sortOrderReversed})}>
                daily
                <span class="sort-desc-icon sort-icon" style="display: {sortColumn === 'daily_total' && sortOrder === 'desc' ? 'unset' : 'none'}">&#8595;</span>
                <span class="sort-asc-icon sort-icon" style="display: {sortColumn === 'daily_total' && sortOrder === 'asc' ? 'unset' : 'none'}">&#8593;</span>
            </span>
        </p>
    </div>
    <div class="score-columns">
        <div class="table-header-column weekend-column-header" on:click={() => handleSort({sortColumn:'styling', sortOrder: sortOrderReversed})}>
            styling
            <span class="sort-asc-icon sort-icon" style="display: {sortColumn === 'styling' && sortOrder === 'asc' ? 'unset' : 'none'}">&nbsp;&#8593;</span>
            <span class="sort-desc-icon sort-icon" style="display: {sortColumn === 'styling' && sortOrder === 'desc' ? 'unset' : 'none'}">&nbsp;&#8595;</span>        
        </div>
        <div class="table-header-column weekend-column-header" on:click={() => handleSort({sortColumn:'acceleration', sortOrder: sortOrderReversed})}>
            acceleration
            <span class="sort-asc-icon sort-icon" style="display: {sortColumn === 'acceleration' && sortOrder === 'asc' ? 'unset' : 'none'}">&nbsp;&#8593;</span>
            <span class="sort-desc-icon sort-icon" style="display: {sortColumn === 'acceleration' && sortOrder === 'desc' ? 'unset' : 'none'}">&nbsp;&#8595;</span>                
        </div>
        <div class="table-header-column weekend-column-header" on:click={() => handleSort({sortColumn:'handling', sortOrder: sortOrderReversed})}>
            handling
            <span class="sort-asc-icon sort-icon" style="display: {sortColumn === 'handling' && sortOrder === 'asc' ? 'unset' : 'none'}">&nbsp;&#8593;</span>
            <span class="sort-desc-icon sort-icon" style="display: {sortColumn === 'handling' && sortOrder === 'desc' ? 'unset' : 'none'}">&nbsp;&#8595;</span>        
        </div>
        <div class="table-header-column weekend-column-header" on:click={() => handleSort({sortColumn:'fun_factor', sortOrder: sortOrderReversed})}>
            fun factor
            <span class="sort-asc-icon sort-icon" style="display: {sortColumn === 'fun_factor' && sortOrder === 'asc' ? 'unset' : 'none'}">&nbsp;&#8593;</span>
            <span class="sort-desc-icon sort-icon" style="display: {sortColumn === 'fun_factor' && sortOrder === 'desc' ? 'unset' : 'none'}">&nbsp;&#8595;</span>        
        </div>
        <div class="table-header-column weekend-column-header" on:click={() => handleSort({sortColumn:'cool_factor', sortOrder: sortOrderReversed})}>
            cool factor
            <span class="sort-asc-icon sort-icon" style="display: {sortColumn === 'cool_factor' && sortOrder === 'asc' ? 'unset' : 'none'}">&nbsp;&#8593;</span>
            <span class="sort-desc-icon sort-icon" style="display: {sortColumn === 'cool_factor' && sortOrder === 'desc' ? 'unset' : 'none'}">&nbsp;&#8595;</span>        
        </div>

        <div class="table-header-column daily-column-header" on:click={() => handleSort({sortColumn:'features', sortOrder: sortOrderReversed})}>
            features
            <span class="sort-asc-icon sort-icon" style="display: {sortColumn === 'features' && sortOrder === 'asc' ? 'unset' : 'none'}">&nbsp;&#8593;</span>
            <span class="sort-desc-icon sort-icon" style="display: {sortColumn === 'features' && sortOrder === 'desc' ? 'unset' : 'none'}">&nbsp;&#8595;</span>        
        </div>
        <div class="table-header-column daily-column-header" on:click={() => handleSort({sortColumn:'comfort', sortOrder: sortOrderReversed})}>
            comfort
            <span class="sort-asc-icon sort-icon" style="display: {sortColumn === 'comfort' && sortOrder === 'asc' ? 'unset' : 'none'}">&nbsp;&#8593;</span>
            <span class="sort-desc-icon sort-icon" style="display: {sortColumn === 'comfort' && sortOrder === 'desc' ? 'unset' : 'none'}">&nbsp;&#8595;</span>        
        </div>
        <div class="table-header-column daily-column-header" on:click={() => handleSort({sortColumn:'quality', sortOrder: sortOrderReversed})}>
            quality
            <span class="sort-asc-icon sort-icon" style="display: {sortColumn === 'quality' && sortOrder === 'asc' ? 'unset' : 'none'}">&nbsp;&#8593;</span>
            <span class="sort-desc-icon sort-icon" style="display: {sortColumn === 'quality' && sortOrder === 'desc' ? 'unset' : 'none'}">&nbsp;&#8595;</span>        
        </div>
        <div class="table-header-column daily-column-header" on:click={() => handleSort({sortColumn:'practicality', sortOrder: sortOrderReversed})}>
            practicality
            <span class="sort-asc-icon sort-icon" style="display: {sortColumn === 'practicality' && sortOrder === 'asc' ? 'unset' : 'none'}">&nbsp;&#8593;</span>
            <span class="sort-desc-icon sort-icon" style="display: {sortColumn === 'practicality' && sortOrder === 'desc' ? 'unset' : 'none'}">&nbsp;&#8595;</span>        
        </div>
        <div class="table-header-column daily-column-header" on:click={() => handleSort({sortColumn:'value', sortOrder: sortOrderReversed})}>
            value
            <span class="sort-asc-icon sort-icon" style="display: {sortColumn === 'value' && sortOrder === 'asc' ? 'unset' : 'none'}">&nbsp;&#8593;</span>
            <span class="sort-desc-icon sort-icon" style="display: {sortColumn === 'value' && sortOrder === 'desc' ? 'unset' : 'none'}">&nbsp;&#8595;</span>        
        </div>
    </div>
</div>
<div class="score-table">


    {#each data as d}
        <ScoreRecord rowData={d} />
    {/each}

</div>

<style>
    .filters {
        height: 80px;
        max-width: 1600px;
    }

    .sort-icon {
        font-size: 14px;
        font-weight: bold;

    }

    .sort-visibility {
        visibility: visible;
    }



    .score-table {
        max-width: 1600px;
        max-height: 800px;
        overflow-y: scroll;
        padding: 4px 12px 12px 12px;
    }

    .table-header {
        height: 60px;
        display: flex;
        justify-content: space-between;
        padding: 0 32px;
        font-weight: bold;
        font-size: 11px;
        text-transform: uppercase;
        letter-spacing: 0.4px;
    }

    .table-header-column {
        text-align: center;
        width: 104px;
        display: flex;
        justify-content: center;
        align-items: center;   
        padding: 12px;
    }

    .row-header {
        width: 320px;
        text-align: left;
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }

    .total-score-header {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        gap: 4px;
        width: 160px;
        text-align: center;
        cursor: pointer;
    }


    .weekend-header {
        font-size: 10px;
        color: lightcoral;
    }

    .daily-header {
        font-size: 10px;
        color: mediumseagreen;
    }

    .score-columns {
        display: flex;
        justify-content: flex-start;
        align-items: center;
        flex-grow: 1;
        cursor: pointer;
    }



</style>