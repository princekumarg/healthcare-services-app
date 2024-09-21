<script>
  import ServiceList from "./components/ServiceList.svelte";
  import AddService from "./components/AddService.svelte";

  let services = [
    { name: "General Checkup", description: "Routine health check", price: 50 },
    {
      name: "Blood Test",
      description: "Comprehensive blood analysis",
      price: 30,
    },
  ];

  function addService(service) {
    services = [...services, service];
  }

  function updateService(updatedService) {
    services = services.map((service) =>
      service.name === updatedService.name ? updatedService : service
    );
  }

  function deleteService(index) {
    services = services.filter((_, i) => i !== index);
  }
</script>

<main>
  <h1>Healthcare Services</h1>
  <AddService onAdd={addService} />
  <ServiceList {services} onUpdate={updateService} onDelete={deleteService} />
</main>

<style>
  button {
    margin: 5px;
  }
</style>
