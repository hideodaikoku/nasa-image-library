<script>
	import Search from './Search.svelte';
	import Results from './Results.svelte';
    import Image from './Image.svelte'

    let page = 1;
	let data = [];
	let newBatch = [];
	let query = '';
	let imgSize = '200';
    let state = false;
    let metadata = {};

    function handleClick(data, imgUrl) {
        console.log(data);

        metadata = {
            title : data.title,
            image : imgUrl,
            photographer: data.photographer,
            description : data.description,
            location: data.location,
            keywords: data.keywords,
            nasaid : data.nasa_id,
            date : data.date_created,
            center : data.center
        }
        state = true;
    }

	async function fetchData() {
		fetch(`https://images-api.nasa.gov/search?q=${query}&page=${page}`)
			.then((response) => {
				if (!response.ok) {
					throw new Error(`HTTP error! Status: ${response.status}`);
				}
				return response.json();
			})
			.then((data) => {
				newBatch = data.collection.items;
			})
			.catch((error) => {
				console.error('Error fetching data:', error);
			});
	}

	function clicked(event) {
		query = event.detail.text;
		fetchData();
	}

	$: data = [...data, ...newBatch];
</script>

<h1>NASA Image & Video Library</h1>
<Search bind:search={query} on:message={clicked} />

{#if data.length>0}
<div class='size-container'>
    <div class='size-row'>
        <label for="size">Image Size</label>
        <p id="sizeIndicator">{imgSize} px</p>
    </div>
    <input
		name="size"
		type="range"
		bind:value={imgSize}
		min="50"
		max="600"
		style="--image-size: {imgSize}px"
	/>
</div>
{/if}

{#if state}
    <Image metadata={metadata} bind:state/>
{/if}

<div class="grid-container">
	<div class="grid">
		{#each data as item}
			{#if item.links}
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<img
					class="image-result"
					src={item.links[0].href}
					alt={item.data[0].title}
					style="--image-size: {imgSize}px"
                    on:click={()=>handleClick(item.data[0], item.links[0].href)}
				/>
			{/if}
		{/each}

		<Results
			hasMore={false}
			threshold={100}
			on:loadMore={() => {
				page++;
				fetchData();
			}}
		/>
	</div>
</div>

<style>
	h1 {
		margin-top: 3rem;
		font-weight: bold;
		font-size: 2rem;
		color: black;
		text-align: left;
	}

	.grid-container {
		display: flex;
		flex-direction: column;
		margin: 2rem auto;
	}

	.grid {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: center;
		align-content: top;
		grid-gap: 7px;
	}

	img {
		width: var(--image-size);
		object-fit: cover;
		border-radius: 2px;
	}

    .size-container{
        display: flex;
        flex-direction: column;
        max-width: 200px;
    }

    .size-row{
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
    }

    #sizeIndicator{
        background-color: #0035F2;
        color: white;
        padding: 2px;
        width: 60px;
        text-align: center;
    }
</style>
