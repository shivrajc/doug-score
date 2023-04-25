<script>
    import { createEventDispatcher } from "svelte";
    // import * as d3 from "d3";
    import { inputData } from "../../data/data";
    export let data;

    let carSearchTerm= '',
        year= 'All',
        country= 'All',
        dougscore= 1,
        styling= 1,
        acceleration= 1,
        handling= 1,
        fun_factor= 1,
        cool_factor= 1,
        features= 1,
        comfort= 1,
        quality= 1,
        practicality= 1,
        value= 1;
    
    $: years = ["All", ...new Set($inputData.map(d => d.year).sort((a, b) => a-b))]
    $: countries = ["All", ...new Set($inputData.map(d => d.vehicle_country).sort())]

    // $: console.log(filters)

    $: filters = {
        carSearchTerm,
        year,
        country,
        dougscore,
        styling,
        acceleration,
        handling,
        fun_factor,
        cool_factor,
        features,
        comfort,
        quality,
        practicality,
        value        
    }

    const rangeFilters = ["styling",	"acceleration",	"handling",	"fun_factor",	"cool_factor",	"features",	"comfort",	"quality",	"practicality",	"value"]; 
    const rangeFiltersLabels = ["styling",	"acceleration",	"handling",	"fun factor",	"cool factor",	"features",	"comfort",	"quality",	"practicality",	"value"]; 

    // console.log(filters);

    const dispatch = createEventDispatcher();

    function forwardFilter()  {
        dispatch('filter', {filters});
    }

    function handleReset() {
        filters.carSearchTerm= '';
        filters.year= 'All';
        filters.country= 'All';
        filters.dougscore= 1;
        filters.styling= 1;
        filters.acceleration= 1;
        filters.handling= 1;
        filters.fun_factor= 1;
        filters.cool_factor= 1;
        filters.features= 1;
        filters.comfort= 1;
        filters.quality= 1;
        filters.practicality= 1;
        filters.value= 1;

        dispatch('reset', {reset: "reset"})
    }

</script>

<div class="filters">

    <div class="name-filters">
        <div class="car-search">
            <input type="text" 
                id="search-field" 
                placeholder="Search Car Make/Model" 
                autocomplete="off"
                bind:value={carSearchTerm}
                on:input={forwardFilter}
                class:selected={carSearchTerm != ""} 
            />
        </div>
        <div class="name-filters-sub">
            <div class="year-select select">
                <label for="year">Year</label>
                <select name="year" id="year" bind:value={filters.year} on:change={forwardFilter} class:selected={filters.year != "All"} >
                    {#each years as y}
                        <option value={y}>{y}</option>
                    {/each}
                </select>
            </div>
            <div class="country-select select">
                <label for="country">Conutry</label>
                <select name="country" id="country" bind:value={filters.country} on:change={forwardFilter} class:selected={filters.country != "All"}>
                    {#each countries as c}
                        <option value={c}>{c}</option>
                    {/each}
                </select>
            </div>
        </div>
    </div>

    <div class="score-filters-main-container">
        <div class="clear-btn">
            <span>&#9432; &nbsp;Click on the column names to sort the table</span>
            <button on:click={handleReset}>
                CLEAR ALL FILTERS
            </button>
        </div>        
        <div class="score-filters-container">
            <div class="total-score-filter">
                <div class="dougscore-range">
                    <label for="dougscore">&#8807;</label>
                    <input 
                        type="number" 
                        id="dougscore"
                        name="dougscore"
                        min="1"
                        max="100" 
                        bind:value={dougscore}
                        on:change={forwardFilter} 
                        class:selected={dougscore > 1}
                    />
                </div>
            </div>
            
            <div class="score-filters">
                {#each rangeFilters as rng, i}
                    <div class="{rng}-range score-range">
                        <label for="{rangeFiltersLabels[i]}">&#8807;</label>
                        <input 
                            type="number" 
                            id={rng}
                            name={rng}
                            min="1"
                            max="10" 
                            bind:value={filters[rangeFilters[i]]}
                            on:change={forwardFilter} 
                            class:selected={filters[rangeFilters[i]] > 1}
                        />
                    </div>        
                {/each}
            </div>
        </div>

    </div>

</div>


<style>
    .filters {
        width: 1600px;
        display: flex;
        justify-content: flex-start;
        align-items: flex-end;
        height: 70px;
        padding: 0 30px;
        text-transform: uppercase;
        font-size: 10px;
        letter-spacing: 0.4px;
    }

    .name-filters {
        width: 320px;
        display: flex;
        justify-content: flex-start;
        align-items: center;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
        gap: 8px;
    }

    .name-filters-sub {
        display: flex;
        justify-content: flex-start;
        align-items: center;
        gap: 28px;        
    }

    .name-filters-sub.select {
        display: flex;
        justify-content: flex-start;
        align-items: center;     
    }

    .name-filters input[type="text"] {
        padding: 4px 8px;
        width: 316px;
        /* border: 1px solid lightgray; */
        /* border-radius: 4px; */
    }

    .name-filters select {
        padding: 4px 2px;
        background-color: white;
        border-radius: 2px;
        /* border: 1px solid gray; */
        padding: 3px 4px;
    }

    .name-filters label {
        font-size: 11px;
    }

    select {
        cursor: pointer;
    }

    .year-select select {
        width: 80px;
    }

    .country-select {
        width: 180px;
    }

    .country-select select {
        width: 120px;
    }

    .score-filters-main-container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-end;
        gap: 12px;
    }

    .score-filters-main-container button{
        display: flex;
        justify-content: center;
        align-items: center;
        margin-right: 16px;
        padding: 4px 8px;
        color: orangered;
        background-color: transparent;
        border: 1px solid orangered;
        border-radius: 4px;
        font-size: 11px;
        cursor: pointer;
        /* visibility: hidden; */
    }

    .clear-btn {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        gap: 770px;
        font-size: 12px;
        text-transform: none;
        letter-spacing: normal;
        color: gray;
        /* letter-spacing: 1px; */
    }

    .score-filters-main-container button:hover {
        background-color: rgb(246, 120, 74);
        color: white;
    }

    .score-filters-container {
        display: flex;

    }

    .total-score-filter {
        width: 160px;
        display: flex;
        justify-content: center;
        align-items: center;      
    }

    .total-score-filter input {
        padding: 2px;
        width: 80px;
    }

    .score-filters {
        display: flex;
        justify-content: space-between;
        align-items: center;
        /* gap: 12px; */
        /* text-align: left; */
    }

    .score-range {
        flex-grow: 1;
        padding: 0 12px;
        width: 104px;
        display: flex;
        /* flex-direction: column; */
        justify-content: center;
        align-items: center;
        gap: 4px;

    }

    .score-range label, .dougscore-range label {
        font-size: 14px;
        font-weight: bold;
    }

    .score-range input{        
        padding: 2px;
        width: 60px;
    }

    .selected {
        border: 1px solid darkorange;
        /* color: orangered; */
    }

    .selected:focus {
        outline: none;
    }
</style>