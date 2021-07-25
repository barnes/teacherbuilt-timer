<script>
    // Need to listen to change to the time value, and start a timer.
    import {supabase} from '../lib/db';
    let showCreate = false;
    export let joinCode = '';
    function displayCreateRoom(){
        showCreate = true;
    }
    async function createRoom(){
        let alphabet = "ABCDERFGHIJKLMNOPQRSTUVWXYZ"
        joinCode = '';

        for (let i = 0; i<4; i++){
            joinCode += (alphabet.charAt(Math.floor(Math.random() *alphabet.length)))
        }
        showCreate = true;

        try {
            const { data, error } = await supabase
            .from('rooms')
            .insert([
                { joinCode: joinCode},
            ])
  
            if (error) throw error
        } catch (error) {
            console.log(error.message)
        } finally {
        }
    }

    const rooms = supabase
        .from('rooms:joinCode=eq.joinCode')
        .on('UPDATE', payload => {
            console.log('Change received!', payload)
        })
        .subscribe()
</script>

<form on:submit|preventDefault={createRoom}>
    <button 
        label="Create Room"
        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
    >Create</button>
    {#if joinCode != ''}
        <h1>Your code is:  {joinCode}</h1>
    {:else}
    {/if}
</form>