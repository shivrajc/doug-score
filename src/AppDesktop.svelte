<script>
    import { inputData } from "./data/data";
    import CircularHeatMap from "./lib/CircularHeatMap.svelte";
    import ScrollDown from "./lib/ScrollDown.svelte";
    import Title from "./lib/Title.svelte";
    import ScoreTable from "./lib/ScoreTable.svelte";
    import Search from "./lib/Filters/Search.svelte";
    import Filters from "./lib/Filters/Filters.svelte";

    let currentData = $inputData;
    let sortColumn = 'dougscore';
    let sortOrder = 'desc'

    function handleSort(event) {
        let arr;
        sortColumn = event.detail.sortColumn;
        sortOrder = event.detail.sortOrder;
        arr = currentData.sort((a, b) => sortOrder === 'desc' ? (b[sortColumn]-a[sortColumn]) : (a[sortColumn]-b[sortColumn]));
        currentData = [...arr];
    }


    function filterData(event) {
        let filteredData;

        console.log(event.detail.filters);

        filteredData = 
            $inputData
                .filter(d => {
                    if(event.detail.filters.carSearchTerm === "" || event.detail.filters.carSearchTerm === null) return true;
                    return d.key.toLowerCase().includes(event.detail.filters.carSearchTerm.toLowerCase())
                })
                .filter(d => {
                    if(event.detail.filters.year === 'All') return true;
                    return d.year === event.detail.filters.year
                })
                .filter(d => {
                    if(event.detail.filters.country === 'All') return true;
                    return d.vehicle_country === event.detail.filters.country;
                }) 
                .filter(d => {
                    return d.dougscore >= event.detail.filters.dougscore
                })                                
                .filter(d => {
                    return d.styling >= event.detail.filters.styling
                })                                
                .filter(d => {
                    return d.acceleration >= event.detail.filters.acceleration
                })                                
                .filter(d => {
                    return d.handling >= event.detail.filters.handling
                })                                
                .filter(d => {
                    return d.fun_factor >= event.detail.filters.fun_factor
                })                                
                .filter(d => {
                    return d.cool_factor >= event.detail.filters.cool_factor
                })                                
                .filter(d => {
                    return d.features >= event.detail.filters.features
                })                                
                .filter(d => {
                    return d.comfort >= event.detail.filters.comfort
                })                                
                .filter(d => {
                    return d.quality >= event.detail.filters.quality
                })                                
                .filter(d => {
                    return d.practicality >= event.detail.filters.practicality
                })                                
                .filter(d => {
                    return d.value >= event.detail.filters.value
                })                                
        currentData = [...filteredData];
    }

</script>

<main>
    <div class="circular-chart">
        <CircularHeatMap {inputData} />
        <div class="title-section">
            <Title />
        </div>
        <div class="scroll-down">
            <ScrollDown />
        </div>
    </div>

    <div class="table-section">
        <div class="table-title">
            <h1>DougScore of all cars</h1>
        </div>
        <div class="filters">
            <Filters data={currentData} on:filter={filterData} on:reset={() => currentData = $inputData}/>
        </div>

        <div class="score-table">
            <!-- <img src="src\assets\car_bkg.jpg" alt=""> -->
            <ScoreTable 
                data={currentData} 
                {sortColumn}
                {sortOrder}
                on:search={filterData}  
                on:sort={handleSort}  
            />
        </div>
    </div>
</main>

<style>
    main {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
        margin: 0 auto;   
        width: 100%;
        /* height: 100%; */
        scroll-snap-type: y mandatory;
        /* overflow-y: scroll; */
    }
    
    .circular-chart {
        height: 100vh; 
        scroll-snap-align: start;
        scroll-snap-stop: always;
    }
    
    .scroll-down {
        height: 60px;
    }

    .table-title {
        height: 80px;
        display: flex;
        justify-content: center;
        align-items: center;
        /* border-bottom: 2px solid; */
    }

    .table-section {
        height: 100vh;
        scroll-snap-align: start;
        scroll-snap-stop: always;
        display: flex;
        flex-direction: column;
    }

    .score-table {
        width: 100%;
        /* height: 100%; */
    }

</style>