<script>
  import {
    createEventDispatcher
  } from 'svelte';
  import {
    scale
  } from 'svelte/transition';
  import {
    elasticOut
  } from 'svelte/easing';

  export let celeb;
  export let showyear;
  export let winner;

  const dispatch = createEventDispatcher();
</script>

<div class="card-outer">
  <button class="card-inner" style="background-image: url(/assets/images/{celeb.image});" on:click={()=>
    dispatch('select')}
    >
    <div class="details">
      <h2>{celeb.name}</h2>

      {#if celeb.type}
        <p class="type">{celeb.type}</p>
      {/if}
    </div>

    {#if showyear}
			<div class="age" class:large={winner}>
				<span in:scale={{easing:elasticOut, duration: 800}}>age {celeb.age}</span>
			</div>
		{/if}
	</button>
</div>

<style>
	.card-outer {
		width: 100%;
		height: 100%;
	}

	.card-inner {
		position: absolute;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		background: 50% 50% no-repeat;
		background-position: 50% 0;
		background-size: cover;
		border-radius: var(--border-radius);
		box-shadow: 2px 4px 6px rgba(0,0,0,0.2);
		overflow: hidden;
		padding: 0;
		text-align: left;
	}

	.details {
		position: absolute;
		width: 100%;
		bottom: 0;
		padding: 1em 0.5em 0.5em 0.5em;
		background: linear-gradient(to bottom, transparent, rgba(0,0,0,0.6) 35%, rgba(0,0,0,0.9));
		color: white;
	}

	h2 {
		margin: 0 0 0.2em 0;
	}

	.type {
		margin: 0;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}

	.age {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		left: 0;
		background-color: rgba(0,0,0,0.3);
		color: white;
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 4em;
		font-weight: 700;
	}

	.age.large {
		font-size: 6em;
	}

	@media (min-width: 640px) {
		.card-outer {
			height: 0;
			padding: 0 0 100% 0;
		}
	}
</style>