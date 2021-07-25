<script>
    import {supabase} from '../lib/db'
  
    let loading = false
  
    const handleLogin = async () => {
      try {
        loading = true
        const { error } = await supabase.auth.signIn({ provider: 'google' })
        if (error) throw error
      } catch (error) {
        alert(error.error_description || error.message)
      } finally {
        loading = false
      }
    }
</script>

<form class="bg-blue-500 shadow-md" on:submit|preventDefault={handleLogin}>
  <input type="submit" value={loading ? "Loading" : "Signup with Google"} disabled={loading} />
  <div class="list-none p-6 bg-gray-100">
    <h1 class="text-4xl text-center my-8 uppercase">Supabase + Svelte</h1>
    <p>Sign in Google below.</p>
    <div>
      <input 
        type="submit" 
        value={loading ? "Loading" : "Signup with Google"} 
        disabled={loading} 
        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
      />
    </div>
  </div>
</form>