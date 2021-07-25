<script>
    import Nav from '../components/Nav.svelte'
    import {user} from '../stores/sessionStore'
    import {supabase} from '../lib/db'

    user.set(supabase.auth.user())

    supabase.auth.onAuthStateChange((_,session) => {
        user.set(session.user)
    })



</script>
<div class="p-8 max-w-6xl mx-auto">
<Nav user={user}/>
<slot></slot>
</div>

<style>
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
</style>