<script>
  import { onMount } from "svelte";
  import Slots from "./Slots.svelte";
  let slots;
  let slot;
</script>

<h1>😀 The UnOFFiciaL CoW!n App 🙃</h1>
<main>
	<Slots {slots} />
</main>
<svelte:head>
	<title>CoW!n Slot App</title>
</svelte:head>

<style>
  main {
    background-color: rgb(185, 175, 178);
    font-size: 15px;
  }
  h1 {
    font-size: 25px;
  }
  
</style>