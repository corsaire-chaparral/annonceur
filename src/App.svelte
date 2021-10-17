<script>
  import participantsJson from './participants.json';
  import { onMount, beforeUpdate, tick } from 'svelte';

  // Vars
  let current = '';
  let tmp = {};
  let entered = [];
  let participants = [];
  let inputElem;

  $: {
    current;
    makeTmp();
  }

  onMount(() => {
    participants = participantsJson;
  });

  // beforeUpdate(async () => {
  //   await tick();
  // });

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

    inputElem ? inputElem.select() : '';
  }
</script>

<h1>Annonceur</h1>
<div class="total">
  Total: <br>
  {participants.length} participants
</div>

<form on:submit={submitForm}>
  <input
    bind:this={inputElem}
    type="number"
    bind:value={current}
    on:keyup={() => makeTmp()}
    autofocus
    placeholder="# dossard"
  >
</form>

{#if tmp.nom}
<div class="tmp">
  <span>{tmp.prenom}</span>
  <span>{tmp.nom}</span>
  <span>#{tmp.id}</span>
  <span class="equipe">{tmp.equipe}</span>
</div>
{:else}
{#if current > 0}
<div class="notfound">
  (#{current} introuvable)
</div>
{/if}
{/if}

<div id="list">
  <div class="header row">
    <span>#</span>
    <span>Prénom</span>
    <span>Nom</span>
    <span>Équipe</span>
  </div>
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
    margin: 2rem auto;
    width: 100%;
    max-width: 40rem;
  }

  input {
    background-color: var(--color-text);
    color: #000;
    text-align: center;

    font-size: 3rem;
    padding: 1rem .75rem;
    line-height: 1;
    width: 100%;
    display: block;
    margin: .5rem 0 .5rem;
  }

  #list {
    margin-top: 1.5rem;
    width: 100%;
  }

  .tmp {
    margin: 2rem 0;
    font-size: 7vw;
    text-transform: uppercase;
    text-align: center;
  }

  .notfound {
    margin: 2rem 0;
    line-height: 7vw;
    font-size: 6vw;
    opacity: .85;
  }

  .row {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    flex-direction: row;
    justify-content: space-between;
    border-bottom: 1px solid currentColor;
    padding: .75rem 0;
  }
  .row.header {
    border-top: 2px solid currentColor;
    border-bottom: 2px solid currentColor;
  }
  .row.header span {
    font-size: .9325rem;
  }
  @media (min-width: 60rem) {

    .row.header span {
      font-size: .875rem;
    }
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

