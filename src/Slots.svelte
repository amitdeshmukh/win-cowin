<script>
  import { onMount } from 'svelte'
  import Slot from './Slot.svelte'
  // define the data holding variable
  let slots;
  let counter = 0
  let today, day, month, year, dateStr, filteredCenters

  function doFetch() {
    slots = []
    today = new Date()
    day = today.getDate()
    month = today.getMonth() < 10 ? '0' + (today.getMonth() + 1) : (today.getMonth() + 1)
    year = today.getFullYear()
    dateStr = day + '-' + month + '-' + year

    fetch(`https://cdn-api.co-vin.in/api/v2/appointment/sessions/calendarByDistrict?district_id=395&date=${dateStr}`)
    .catch((err) => console.log(err))
    .then(r => r.json())
    .then(d => {
      let a = []
      d.centers.forEach(center => {
        center.sessions.forEach(session => {
          if ((session.min_age_limit === 18) && (session.available_capacity_dose1 > 0) && (session.vaccine === "COVAXIN")) {
            a.push(center)
          }
        })
      })
      slots = a
      counter++
      console.log(counter)
    })
  }

  onMount(() => {
    setInterval(doFetch, 5000)
  })
</script>  

{#if slots}
  {#each slots as slot }
    <ul>
      <li>    
        <Slot {slot} />
      </li>
    </ul>
  {/each}
{:else}
  <p class="loading">loading...</p>
{/if}

<style>
  .loading {
    opacity: 0;
    animation: 0.4s 0.8s forwards fade-in;
  }
  @keyframes fade-in {
    from { opacity: 0; }
    to { opacity: 1; }
  }
  li {
    list-style-type: georgian;
  }
</style>