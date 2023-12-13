<script>
  let username = "";
  let user = null;
  async function submit() {
    try {
      const response = await fetch(`https://api.github.com/users/${username}`);
      if (!response.ok) {
        throw new Error("User not found");
      }
      user = await response.json();
      console.log(user);
    } catch (error) {
      console.error(error);
      user = null;
    }
  }
</script>

<main class="flex items-center justify-center mt-16 bg-gray-800 text-gray-50">
  <form on:submit|preventDefault={submit}>
    <p>Enter a username to find on GitHub</p>
    <div class="grid gap-2">
      <label
        for="username"
        class="block text-sm text-gray-500 dark:text-gray-300">Username</label
      >

      <input type="text" placeholder="Type here" class="input input-bordered input-primary w-full max-w-xs" />

      <button
        class="px-6 py-2 font-medium tracking-wide text-white capitalize transition-colors duration-300 transform bg-blue-600 rounded-lg hover:bg-blue-500 focus:outline-none focus:ring focus:ring-blue-300 focus:ring-opacity-80"
      >
        Primary
      </button>
    </div>
  </form>

  {#if user}
    <div>
      <h2>{user.name}</h2>
      <p>{user.bio}</p>
      <img src={user.avatar_url} alt="{user.name}'s avatar" />
    </div>
  {/if}
</main>
