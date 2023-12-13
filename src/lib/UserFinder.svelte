<script>
  let username = "";
  let user = null;
  async function submit() {
    const response = await fetch(`https://api.github.com/users/${username}`);
    const user = await response.json();
    console.log(user);
  }
</script>

<main class="flex items-center justify-center mt-16 ">
  <form on:submit|preventDefault={submit}>
    <p>Enter a username to find on GitHub</p>
    <div class="grid gap-2 mt-4">
     
      <input type="text" bind:value={username} placeholder="Type user name here" class="input input-bordered input-primary w-full max-w-xs" />

      <button class="btn btn-secondry mt-2 text-white fontbold">Search</button>
    </div>
  </form>

  {#if user}
  <div class="card card-side bg-base-100 shadow-xl">
    <figure><img src="{user.avatar}" alt="Movie"/></figure>
    <div class="card-body">
      <h2 class="card-title">{user.name}</h2>
      <p>{user.bio}</p>
      <div class="card-actions justify-end">
        <button class="btn btn-primary">Show More</button>
      </div>
    </div>
  </div>
  {/if}
</main>
