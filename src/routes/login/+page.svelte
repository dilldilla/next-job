<script>
    // AKU RASA KAN AKU KENA REVIEW BALIK LAH CODE DIA AAAAAAAAAA
    import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
    import { goto } from '$app/navigation';
    import { authenticateUser} from  './../../utils/auth.js'
    let formErrors = {};

    async function loginUser(evt) {
      evt.preventDefault();

    const userData = {
      username: evt.target['username'].value,
      password: evt.target['password'].value,
      };

    // STATUS OF THE USERS
        const res = await authenticateUser(userData.username, userData.password)
        console.log(res)

      if (res.success) {
        goto('/');
      } else {
        formErrors = res.res.message
      }
    
  }
</script>


<h1 class="text-center text-xl">Login To Account</h1>

<div class="flex justify-center items-center mt-8">
    <form on:submit={loginUser} class="w-1/3">
        <div class="form-control w-full">
            <label class="label" for="username">
                <span class="label-text">Username</span>
            </label>
            <input
                type="text"
                name="username"
                placeholder="johndoe"
                class="input input-bordered w-full"
            />
            <!-- {#if 'username' in formErrors}
                <label class="label" for="username">
                    <span class="label-text-alt text-red-500">{formErrors.username.message}</span>
                </label>
            {/if} -->
        {#if formErrors}
            <div class="text-red-500 text-center mt-2">{formErrors}</div>
        {/if}
        </div>



        <div class="form-control w-full">
            <label class="label" for="password">
                <span class="label-text">Password</span>
            </label>
            <input
                type="password"
                name="password"
                placeholder=""
                class="input input-bordered w-full"
                required
            />
            {#if 'password' in formErrors}
                <label class="label" for="password">
                    <span class="label-text-alt text-red-500">{formErrors['password'].message}</span>
                </label>
            {/if}
        </div>

        

        <div class="form-control w-full mt-4">
            <button class="btn btn-md">Login</button>
        </div>
    </form>
</div>

<!-- <h1 class="text-center text-2xl mt-5 font-bold sm:text-3xl">Login</h1>
<div class="flex justify-center items-center mt-8 ">
    <form on:submit={loginUser} class="w-1/3">
    <div class="form-control w-full">
        <label class="label" for="username">
            <span class="label-text text-xl ">Username</span>
        </label>
        <input type="text" name="username" placeholder="Type here" class="input input-bordered w-full" required />
        {#if 'username' in formErrors}
            <label class="label" for="username">
                <span class="label-text-alt text-red-500">{formErrors['username'].message}</span>
            </label>
        {/if}
    </div>
    <div class="form-control w-full">
        <label class="label" for="password">
            <span class="label-text text-xl ">Password</span>
        </label>
        <input type="password" name="password" placeholder="Type here" class="input input-bordered w-full" required />
        {#if 'password' in formErrors}
            <label class="label" for="password">
                <span class="label-text-alt text-red-500">{formErrors['password'].message}</span>
            </label>
        {/if}
    </div>
    <div class="form-control w-full mt-4">
        <button>Login</button>
    </div>
    <div class="text-center">
        <a class="link-hover italic text-xs" href="/users/new">Don't have an account yet? Click here to sign-up instead!.</a>
    </div>
</form>
</div> -->