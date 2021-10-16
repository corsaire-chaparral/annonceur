<script>
  import participantsJson from './participants.json';
  import { onMount, beforeUpdate, tick } from 'svelte';

  // Vars
  let current = '';
  let tmp = {};
  let entered = [];
  let participants = [];

  $: {
    current;
    makeTmp();
  }

  onMount(() => {
    participants = participantsJson;
  });

  beforeUpdate(async () => {
    await tick();
  });

  // Functions
  function makeTmp() {
    for (let i = 0; i < participants.length; i++) {
      if (participants[i].id === current) {
        tmp = participants[i];
        return;
      }
    }
    tmp = {};
  }

  function findParticipant() {
    for (let i = 0; i < participants.length; i++) {
      if (participants[i].id === current) {
        entered.unshift(participants[i])
        entered = entered;
        return;
      }
    }
  }

  function submitForm(ev) {
    ev.preventDefault();

    findParticipant();
  }
</script>

<h1>Annonceur</h1>
<div class="total">
  Total: <br>
  {participants.length} participants
</div>

<form on:submit={submitForm}>
  <input type="number" bind:value={current} on:keyup={() => makeTmp()} >
</form>

<div class="tmp">
  {#if tmp.nom}
  <span>{tmp.prenom}</span>
  <span>{tmp.nom}</span>
  <span>#{tmp.id}</span>
  <span class="equipe">{tmp.equipe}</span>
  {/if}
</div>

<div id="list">
  {#each entered as enter}
  <div class="row">
    <span>{enter.id}</span>
    <span>{enter.prenom}</span>
    <span>{enter.nom}</span>
    <span>{enter.equipe}</span>
  </div>
  {/each}

</div>

<style>

	h1 {
		color: var(--color-text);
		text-transform: uppercase;
		font-size: 2.5rem;
		font-weight: 100;
    margin: 0;
	}

  .total {
    position: absolute;
    top: 0;
    right: 0;
    padding: .5rem;
    font-size: .675rem;
    text-transform: uppercase;
    letter-spacing: .02em;
  }

  form {

  }

  input {
    background-color: var(--color-text);
    color: #000;
    text-align: center;

    font-size: 3rem;
    line-height: 1.35;
    width: 6em;
    display: block;
    margin: .5rem 0 .5rem;
  }

  #list {
    margin-top: 1.5rem;
    border-top: 2px solid currentColor;
    width: 100%;

  }

  .tmp {
    margin: 2rem 0;
    font-size: 7vw;
    text-transform: uppercase;
    text-align: center;
  }

  .row {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    flex-direction: row;
    justify-content: space-between;
    border-bottom: 1px solid currentColor;
    padding: .75rem 0;
  }

  .row span {
    letter-spacing: .015em;
    text-transform: uppercase;
    font-size: .935rem;
  }
  @media (min-width: 60rem) {
    .row span {
      font-size: 2rem;
    }
  }

  .equipe {
    font-size: 2rem;
    padding: .75rem .25rem;
    background: var(--color-text);
    color: var(--color-primary);
    display: block;
    border-radius: .35rem;
  }
</style>

