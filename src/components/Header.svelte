<!-- <script>
    import { isLoggedIn, logOut } from '../utils/auth.js';
    import { goto } from '$app/navigation';

    function handleLogout() {
        logOut();
       // goto('/login'); // Optional: Redirect to login after logout
    }
</script>

<nav class="navbar bg-base-100">
    <div class="flex-1">
        <a href='/' class="btn btn-ghost normal-case text-xl">NEXT Jobs DB</a>
    </div>
    <div class="flex-none">
        <a href='/jobs/createJob'>Post a Job</a>
    </div>
    
    {#if isLoggedIn == false}
        <a href="/login" class="menu menu-horizontal px-1">Log In</a>
        <button on:click={handleLogout}>Logout</button>
    {:else}
        <button on:click={handleLogout}>Logout</button>
        <a href="/login" class="menu menu-horizontal px-1">Log In</a>
    {/if}
</nav> -->




<!-- <script>
    import { isLoggedIn, logOut } from '../utils/auth.js';
    import { goto } from '$app/navigation';

    function handleLogout() {
        logOut();
        
    }

    function handlePostJobClick() {
        if (isLoggedIn) {
            goto('/jobs/createJob');
        } else {
            goto('/users/new');
        }
    }
</script>

<nav class="navbar bg-base-100">
    <div class="flex-1">
        <a href='/' class="btn btn-ghost normal-case text-xl">NEXT Jobs DB</a>
    </div>
    <div class="flex-none">
        <!-- Use button instead of <a> for handling click event -->
        <button on:click={handlePostJobClick}>Post a Job</button>
    </div>
    
    {#if isLoggedIn == false}
        <a href="/login" class="menu menu-horizontal px-1">Log In</a>
    {:else}
        <button on:click={handleLogout}>Logout</button>
    {/if}
</nav>
 -->
