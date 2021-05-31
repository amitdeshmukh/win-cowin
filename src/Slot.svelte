<script>
  export let slot
  var audio = new Audio('bell.mp3');
  audio.play();
</script>

{#each slot.sessions as session}
  <article>
    <h2>
      Pin code: <b>{slot.pincode}</b>
    </h2>
    <h3>
      Vaccine: <b>{session.vaccine}</b>   
    </h3>
    <small>
      Area: <b>{slot.address}</b>   
    </small><br/>
    <small>
      Fee Type: <b>{slot.fee_type}</b>
    </small><br/>
    <small>
      Dose 1 Capacity: <b>{session.available_capacity_dose1}</b>
    </small><br/>
  </article>
{/each}

<style>
  article {
    margin: 0 0 3em 0;
  }
  h1 {
    font-size: 1.4em;
    margin: 0;
    display: block;
  }
</style>