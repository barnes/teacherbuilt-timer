<script>
    export let user;
</script>

<nav class="flex justify-center w-full">
    <a class="mx-4 text-lg" href="/">Home</a>
    <a class="mx-4 text-lg" href="/about">About</a>
    {#if $user}
    <a class="mx-4 text-lg" href="/profile">Profile</a>
    {:else}
    <a class="mx-4 text-lg" href="/auth">Sign Up</a>
    {/if}
</nav>