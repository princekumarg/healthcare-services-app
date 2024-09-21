<!-- <script>
  export let services;
  export let onUpdate;
  export let onDelete;

  function handleUpdate(service) {
    onUpdate(service);
  }

  function handleDelete(service) {
    onDelete(service);
  }
</script>

<ul>
  {#each services as service, index}
    <li>
      <strong>{service.name}</strong> - {service.description} ( ₹{service.price})
      <button on:click={() => handleUpdate(service)}>Update</button>
      <button on:click={() => handleDelete(index)}>Delete</button>
    </li>
  {/each}
</ul> -->
<script>
  export let services;
  export let onUpdate;
  export let onDelete;

  let editIndex = null;
  let updatedService = { name: "", description: "", price: "" };

  function editService(service, index) {
    // Set the service in edit mode
    editIndex = index;
    updatedService = { ...service }; // Clone the service data
  }

  function saveService() {
    onUpdate(editIndex, updatedService); // Trigger the update in parent
    editIndex = null; // Exit edit mode
  }

  function handleDelete(index) {
    onDelete(index);
  }
</script>

<ul>
  {#each services as service, index}
    <li>
      {#if editIndex === index}
        <input
          type="text"
          bind:value={updatedService.name}
          placeholder="Service Name"
        />
        <input
          type="text"
          bind:value={updatedService.description}
          placeholder="Description"
        />
        <input
          type="number"
          bind:value={updatedService.price}
          placeholder="Price"
        />
        <button on:click={saveService}>Save</button>
        <button on:click={() => (editIndex = null)}>Cancel</button>
      {:else}
        <strong>{service.name}</strong> - {service.description} ($ {service.price})
        <button on:click={() => editService(service, index)}>Update</button>
        <button on:click={() => handleDelete(index)}>Delete</button>
      {/if}
    </li>
  {/each}
</ul>
