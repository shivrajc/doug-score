<script>
    import { createEventDispatcher } from "svelte";
    let searchTerm; 

    const dispatch = createEventDispatcher();

    function forwardInput(event) {
        dispatch('search', {searchTerm});
    }
</script>

<input type="text" 
    id="search-field" 
    placeholder="Search Car Make/Model" 
    autocomplete="off"
    bind:value={searchTerm}
    on:input={forwardInput} 
/>