<script>
	import axios from "axios";
	import { onMount } from 'svelte';
	import Mobile from './components/Mobile.svelte';
	import Desktop from './components/Desktop.svelte';
	// FIXME empty
	let y;
	let sessions = [{id: 56, name: 'test'}];

	onMount(async () => {
		// FIXME написать фаил кофигурации
		// axios.get('https://realtimepoll-server.herokuapp.com/sessions').then(res => sessions = res.data);
		// axios.get('http://localhost:8080/sessions').then(res => sessions = res.data);
	});
</script>

<svelte:window bind:innerWidth= {y} />
{#if y < 600}
<Mobile sessions = {sessions}/>
{:else}
<Desktop sessions = {sessions}/>
{/if}	