<script>
    // Need to listen to change to the time value, and start a timer.
    import {supabase} from '../lib/db';
    export let joinCode = '';
    export let remote;

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

</script>

<h1 use:createRoom>Your code is:  {joinCode}</h1>
<h1> {remote} </h1>
