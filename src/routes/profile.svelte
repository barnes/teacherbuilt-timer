<script>
    import  { supabase }  from '../lib/db'
    import { user } from '../stores/sessionStore'
  
    let loading = true
    let username = null
    let website = null
    let times = null
    let avatar_url = null
  
    async function getProfile() {
      try {
        loading = true
        const user = supabase.auth.user()
  
        let { data, error, status } = await supabase
          .from('profiles')
          .select(`username, website, avatar_url, times`)
          .eq('id', user.id)
          .single()
  
        if (error && status !== 406) throw error
  
        if (data) {
          username = data.username
          website = data.website
          avatar_url = data.avatar_url
        }
      } catch (error) {
        alert(error.message)
      } finally {
        loading = false
      }
    }
  
    async function updateProfile() {
      try {
        loading = true
        const user = supabase.auth.user()
  
        const updates = {
          id: user.id,
          username,
          website,
          avatar_url,
          updated_at: new Date(),
        }
  
        let { error } = await supabase.from('profiles').upsert(updates, {
          returning: 'minimal', // Don't return the value after inserting
        })
  
        if (error) throw error
      } catch (error) {
        console.log(error.message)
      } finally {
        loading = false
      }
    }
  
    async function signOut() {
      try {
        loading = true
        let { error } = await supabase.auth.signOut()
        if (error) throw error
      } catch (error) {
        alert(error.message)
      } finally {
        loading = false
      }
      
    }
  </script>
  
  <form use:getProfile class="form-widget" on:submit|preventDefault={updateProfile}>
    <div class="p-4">
      <label for="email">Email</label>
      <input 
        id="email" 
        type="text" 
        value={$user.email} 
        disabled />
    </div>
    <div class="p-4">
      <label for="username">Name</label>
      <input
        id="username"
        type="text"
        bind:value={username}
        class="shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
      />
    </div>
    <div class="p-4">
      <label for="website">Website</label>
      <input
        id="website"
        type="website"
        bind:value={website}
        class="shadow appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
      />
    </div>
  
    <div class="p-4">
      <input 
        type="submit"  
        value={loading ? 'Loading ...' : 'Update'} 
        disabled={loading}
        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
      />
    </div>
  
    <div class="p-4">
      <button
        on:click={signOut} 
        disabled={loading}
        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
      >
        Sign Out
      </button>
    </div>
  </form>