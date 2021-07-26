<script context="module">
   export async function load({page}){
      const roomCode = page.params.room 
      return {props: {roomCode}}; 
   }
</script>
<script>
   import JoinRoom from '../../components/JoinRoom.svelte'
   import { supabase } from "$lib/db";
   export let roomCode;

   async function getRoom(event) {
      let {data: rooms, error } = await supabase.from('rooms').select("*").eq('joinCode',roomCode)
      console.log(rooms);
      console.log(error);
      console.log(event);
   }

   
</script>

<h1 use:getRoom>Welcome to Room {roomCode}</h1>