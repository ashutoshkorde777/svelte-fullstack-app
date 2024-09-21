<script lang="ts">
  import Table from "$lib/Table.svelte";

  /** @type {import('./$types').PageData} */
  export let data;
  
  /** @type {import('./$types').ActionData} */
  export let form;

  // State variables to hold the form data
  let name = "";
  let email = "";
  let id = null;  // Used to track if it's an update operation
  
  // Function to populate form fields for editing
  function editApplicant(applicant) {
    name = applicant.name;
    email = applicant.email;
    id = applicant.id;  // Set the ID to know it's an update operation
  }
</script>

<!-- Table to display list of users with edit and delete functionality -->
<Table names={data.names} onEdit={editApplicant} />

<!-- Form to create or update applicant -->
<div class="mt-10 pt-10 w-full max-w-xl p-12 mx-auto rounded-lg shadow-xl dark:bg-white/10 bg-white/30 ring-1 ring-gray-900/5 backdrop-blur-lg">
  <form method="POST" action="?/update">
    <input type="hidden" name="id" value={id}> <!-- Hidden input for ID -->
    <div class="flex flex-wrap -mx-3 mb-2">
      <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
        <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-name">
          Name
        </label>
        <input
          class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
          id="name"
          type="text"
          placeholder="Enter name"
          name="name"
          bind:value={name}
          required
        />
      </div>
      <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
        <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-email">
          Email
        </label>
        <input
          class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
          id="email"
          type="email"
          placeholder="Enter email"
          name="email"
          bind:value={email}
          required
        />
      </div>
      <button type="submit" class="bg-yellow-500 hover:bg-blue-700 text-white font-bold mt-5 ml-2 px-2 rounded">
        {id ? 'Update Applicant' : 'Create Applicant'}
      </button>
    </div>
  </form>

  {#if form?.success}
    <p class="pt-2">{id ? 'Applicant updated!' : 'Added new Applicant!'}</p>
  {/if}
</div>
