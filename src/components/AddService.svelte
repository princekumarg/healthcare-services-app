<script>
  export let onAdd;

  let name = "";
  let description = "";
  let price = "";

  function addService() {
    if (name && description && price) {
      onAdd({ name, description, price });
      name = description = price = ""; // Clear form
    } else {
      alert("All fields are required!");
    }
  }
</script>

<form on:submit|preventDefault={addService}>
  <input type="text" placeholder="Service Name" bind:value={name} />
  <input type="text" placeholder="Description" bind:value={description} />
  <input type="number" placeholder="Price" bind:value={price} />
  <button type="submit">Add Service</button>
</form>
