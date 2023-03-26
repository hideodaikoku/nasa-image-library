<script>
    import { createEventDispatcher } from 'svelte';
    export let search = '';    
    const dispatch = createEventDispatcher();

    function submitSearch(){
        dispatch('message', {
			text: search
		});
    }
</script>

<div class='search-container'>
    <input type='text' placeholder="Type your search terms here..." bind:value={search} name="search" id='searchbar'/>
    <button on:click={submitSearch} type="submit" id="searchbutton">Search</button>
</div>

<style>
    .search-container{
        display: flex;
        flex-direction: column;
        justify-content: left;
        align-items: left;
    }
    #searchbar{
        min-width: 30vw;
        max-width: 1000px;
        outline: 1px solid black;
        border-radius: 2px;
        box-shadow: none;
        height: 1.5rem;
        padding: 2px 6px;
    }
    #searchbutton{
        height: 1.5rem;
        background-color: #0035F2;
        color: white;
        text-align: center;
        border: 1px solid black;
        border-radius: 2px;
        padding: 2px 6px;
        margin: 16px 0;
        cursor: pointer;
    }


    @media only screen and (min-width: 768px){
        .search-container{
            flex-direction: row;
            justify-content: space-between;
            align-items: center;
        }
        #searchbar{
            width: 60vw;
        }
    }
</style>