<script>

  import { createEventDispatcher} from 'svelte';
  let dispatch = createEventDispatcher();

  let name;
  let position;
  let age;
  //let dribbling = false;
  //let passing = false;
  //let strength = false;
  let skills = [];

  const submit = () => {
    const person = {
      name,
      position,
      age,
      skills,
      id: Math.random()
    };


    dispatch('add_person_event', person);

  };
</script>


<main>
  <form on:submit|preventDefault={submit}>
    <input type='text' placeholder='name' bind:value={name}>
    <input type='number' placeholder='age' bind:value={age}>

    <label>Skills:</label>
    <input type='checkbox' bind:group={skills} value='dribbling'> dribbling<br>
    <input type='checkbox' bind:group={skills} value='passing'> passing<br>
    <input type='checkbox' bind:group={skills} value='strength'> strength<br>

    <label>Position:</label>
    <select bind:value={position}>
      <option value='midfield'>Midfield</option>
      <option value='defense'>Defender</option>
      <option value='attack'>Attacker</option>
    </select>

    <!--<input type='checkbox' bind:checked={dribbling}> dribbling<br>
    <input type='checkbox' bind:checked={passing}> passing<br>
    <input type='checkbox' bind:checked={strength}> strength<br> -->
    <button>Add Person</button>
  </form>
</main>



<style>

</style>
