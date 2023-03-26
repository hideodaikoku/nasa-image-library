<script>
    export let metadata = {}
    export let state;
    function changeState() {
        state = false;
    }
</script>


<div class='background'>
    <div class='container'>
        <a on:click={changeState} href='/' alt='Back to Top'>← Back To Top </a>
        <h1>{metadata.title}</h1>
        <img src={metadata.image} alt={metadata.title}/>
        <small>by <span>{metadata.photographer}</span></small>
        <p>{metadata.description}</p>

        <div class='details'>

            <div class='detail-line'>
                <strong class='label'>Keywords</strong><br/>
                {#each metadata.keywords as keyword,index}
                <span>{keyword}{index < metadata.keywords.length - 1 ? ', ' : ''}</span>
                {/each}
            </div>

            <div class='detail-line'>
                <strong class='label'>Location</strong><br/>
                <span>{metadata.location}</span>
            </div>

            <div class='detail-line'>
                <strong class='label'>Date Created</strong><br/>
                <span>{metadata.date}</span>
            </div>

            <div class='detail-line'>
                <strong class='label'>Center</strong><br/>
                <span>{metadata.center}</span>
            </div>

            <div class='detail-line'>
                <strong class='label'>NASA ID</strong><br/>
                <span id='nasaid'>{metadata.nasaid}</span>
            </div>

            
        </div>
    </div>
</div>

<style>
    .background{
        position:fixed;
        padding:0;
        margin:0;

        top:0;
        left:0;

        width: 100%;
        height: 100%;
        background-color: white;

        overflow: scroll;
        z-index: 1;
    }

    .container{
        max-width: 500px;
        margin: 3rem auto;
    }
    h1{
        color: black;
        text-align: left;
    }
    img{
        width: 500px;
    }
    .detail-line{
        margin: 1.5rem 0;
    }
    #nasaid{
        font-family: 'Open Sans' monospace;
        background-color: rgb(194, 194, 194);
        padding: 0 5px;
    }
</style>