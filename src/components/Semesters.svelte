<script>
	import Semester from '../components/Semester.svelte';
	import { onMount } from 'svelte';

	export let semesters;
	export let subtitle;

	let jsEnabled = false;

	function toggleDates({ target }) {
		if (target.nodeName == 'INPUT') {
			document.body.classList.toggle('expand');
		}
	}

	onMount(() => {
		jsEnabled = true;
		document.body.classList.remove('expand');
	});
</script>

<section class="semesters-sprints">
	<h2>{subtitle}</h2>

	{#if jsEnabled}
		<input type="checkbox" id="show-hide-dates" class="toggle" on:change={toggleDates} />
		<label for="show-hide-dates">
			<span> Show/hide holidays </span>
		</label>
	{/if}

	<div class="scroll-horo">
		{#each semesters as semester, i}
			<Semester {semester} {i} />
		{/each}
	</div>
</section>

<style>
	section {
		position: relative;
		width: 100%;
		padding: 0;
		background: var(--grey);
		border-radius: 0 0 15px 15px;
		color: var(--blueberry);
	}
	
	h2 { 
		margin: 0;
	}

	.scroll-horo {
		overflow-x: auto;
		display: flex;
		flex-direction: row;
		flex-wrap: nowrap;
		scroll-snap-type: x mandatory;
		padding: 1rem 2rem 2rem;
	}

	input[type='checkbox'].toggle {
		opacity: 0;
		position: absolute;
		left: -9000px;
		top: -9000px;
	}

	input[type='checkbox'].toggle + label {
		top: 2rem;
		right: 0;
		display: flex;
		align-items: center;
		cursor: pointer;
		color: white;
		font-family: helvetica;
		font-size: 1em;
		margin-left: 3rem;
	}

	input[type='checkbox'].toggle + label::before {
		content: '';
		width: 3rem;
		height: 1.325rem;
		border: solid 1px var(--blueberry);
		border-radius: var(--pilled);
		transition: background-color 200ms ease-in-out;
	}

	input[type='checkbox'].toggle + label::after {
		content: ''; /* \2715 x */
		position: absolute;
		width: 1.5rem;
		height: 1.5rem;
		background-color: var(--blueberry);
		color: var(--blueberry);
		border: solid 1px var(--blueberry);
		border-radius: var(--pilled);
		font-weight: normal;
		font-size: 0.9em;
		display: flex;
		justify-content: center;
		align-items: center;
		transition:
			background-color 200ms ease-in-out,
			transform 200ms ease-in-out;
	}

	input[type='checkbox'].toggle:checked + label::after {
		content: '';
		transform: translateX(1.5em);
		background-color: var(--blueberry);
		color: var(--blueberry);
	}

	input[type='checkbox'].toggle:hover + label::after, input[type='checkbox'].toggle:focus + label::after, input[type='checkbox'].toggle:checked:hover + label::after {
		background-color: var(--blueberry);
		color: var(--blueberry);
	}

	input[type='checkbox'].toggle:checked + label::before {
		background-color: var(--blueberry);
		opacity: 0.5;
		border-color: var(--blueberry);
	}

	label span {
		color: var(--blueberry);
		margin-left: 0.5em;
		font-size: 0.7em;
	}
</style>
