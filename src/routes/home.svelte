<script>
    import Display from '../components/Display.svelte'
    import Remote from '../components/Remote.svelte'

    let displayStatus = false;
    let remoteStatus = false;
    
    let remoteCode = '';

    function setDisplay() {
        displayStatus = true;
        remoteStatus = false;
    }

    function setRemote() {
        remoteStatus = true;
        displayStatus = false;
    }

    function handleBubble(event){
        console.log('Bubble Event')
        console.log(event.detail.roomCode);
        remoteCode = event.detail.roomCode;
        
    }
</script>

{#if !remoteStatus && !displayStatus}
    <button 
        on:click={setDisplay} 
        label="Create A Display"
        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
    > Create a Display </button>


    <button 
        on:click={setRemote} 
        label="Connect to Display"
        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
    >Connect to Display</button>
{:else if remoteStatus && !displayStatus}
    <Remote on:message={handleBubble} />
{:else if !remoteStatus && displayStatus}
    <Display on:message={handleBubble} />
{/if}
