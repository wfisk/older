<script>
  import {
    differenceInYears,
    getYear
  } from 'date-fns';
  import parseISO from 'date-fns/parseISO'
  import {
    onMount
  } from 'svelte';
  import Welcome from './screens/Welcome.svelte';
  import Game from './screens/Game.svelte';
  // import {
  //   select
  // } from './select';
  import {
    load_image
  } from './utils.js';
  import comparisons from './data/comparisons.json';

  // let celebs_promise;

  let state = 'welcome'; // 'welcome' or 'playing'
  let selection;

  const start = async (e) => {
    // const {
    //   celebs,
    //   lookup
    // } = await celebs_promise;

    // selection = select(celebs, lookup, e.detail.category.slug);

    selection = comparisons.map((comparison) => {
      if (!comparison.a.age) {
        comparison.a.age = differenceInYears(
          new Date(),
          parseISO(comparison.a.born)
        );
      }


      if (!comparison.b.age) {
        comparison.b.age = differenceInYears(
          new Date(),
          parseISO(comparison.b.born)
        );
      }

    });

    console.log({
      comparisons
    });
    state = 'playing';
  };



  onMount(() => {
    // celebs_promise = load_celebs();

    load_image('/icons/right.svg');
    load_image('/icons/wrong.svg');
  });
</script>

<main>
  {#if state === 'welcome'}
		<Welcome on:select={start}/>
	{:else if state === 'playing'}
		<Game selection={comparisons} on:restart={() => state = 'welcome'}/>
	{/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 800px;
		margin: 0 auto;
		height: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
	}
</style>