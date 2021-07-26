<script>
    import {supabase} from '../lib/db'
    import {createEventDispatcher} from 'svelte'
    let showRoom = false;
    let joinCode = '';
    let connected = false;
    function displayJoinRoom(){
        showRoom = true;
    }
    async function joinRoom(){
        let {data, error} = await supabase
        .from('rooms')
        .update({'connected': true})
        .eq('joinCode', joinCode)

        connected = true;
    }

    async function startTimer() {
        let {data, error} = await supabase
        .from('rooms')
        .update({'time': 1})
        .eq('joinCode', joinCode)

        dispatchEvent('timerStarted', {joinCode})
    }

</script>

{#if connected}
    <h1>Connected to {joinCode}</h1>
    <button on:click|preventDefault={startTimer} 
        label="Join Room"
        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
    >1 Min Time</button>
{:else}
    <form on:submit|preventDefault={displayJoinRoom}>
        {#if showRoom}
            <form on:submit|preventDefault={joinRoom}>
                <label for="username">Join Code</label>
                <input
                id="joinCode"
                type="text"
                bind:value={joinCode}
                class="shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                />
                <button 
                    label="Join Room"
                    class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                >Submit</button>
            </form>
        {:else}
            <button 
                label="Join Room"
                class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
            >Join room</button>
        {/if}

    </form>
{/if}