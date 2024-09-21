<script>
	export let names = []; // Default to an empty array
	export let onEdit; // Function to handle editing
  </script>
  
  <div class="mt-10 pt-10 w-full max-w-xl p-12 mx-auto rounded-lg shadow-xl dark:bg-white/10 bg-white/30 ring-1 ring-gray-900/5 backdrop-blur-lg">
	<div class="flex items-center justify-between mb-4">
	  <div class="space-y-1">
		<h2 class="text-xl font-semibold">List of Users</h2>
		<p class="text-sm text-gray-500">
		  Fetched {names.length} user{names.length !== 1 ? 's' : ''}
		</p>
	  </div>
	</div>
	
	<div class="divide-y divide-gray-900/5">
	  {#if names.length > 0}
		{#each names as user (user.id)}
		  <div class="flex items-center justify-between py-3">
			<div class="flex items-center space-x-4">
			  <div class="flex">
				<p class="font-medium pt-1 leading-none">{user.name}</p>
				<p class="font-medium pl-5 text-gray-500 pt-0">{user.email}</p>
			  </div>
			</div>
  
			<!-- Delete button -->
			<form method="POST" action="/profiles?/delete">
			  <input type="hidden" name="id" value={user.id}>
			  <button type="submit">
				<img class="w-4 float-right" src="./trash-can.svg" alt="delete"/>
			  </button>
			</form>
  
			<!-- Update button: Calls onEdit with the current user -->
			<button
			  class="ml-4 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
			  on:click={() => onEdit(user)}
			>
			  Update
			</button>
		  </div>
		{/each}
	  {:else}
		<p class="text-gray-500">No users found.</p>
	  {/if}
	</div>
  </div>
  