<script>
	import axios from "axios";
	import { onMount } from 'svelte';
	let fa;
	let ca;
	let ia;
	let fd;
	let cd;
	let id;
	let sessions = [];

	onMount(async () => {
		axios.get('https://realtimepoll-server.herokuapp.com/sessions').then(res => sessions = res.data);
	});
</script>
<style>
	iframe {
		border: 0px solid black;
		height: 50px;
		width: 210px;
	}
	
	.dataInputs {
		width: 200px;
		border-collapse: collapse;
	}

	td {
		align-content: center;
		justify-content: center;
		padding: 5px;
	}
	td > input {
		margin: 0;
	}

	.usernameInput{
		border-width: 0 0 1px 0;
	}

	button {
		width: 210px;
		border-radius: 5px;
		margin-top: 10px;
	}

</style>

<form action='https://realtimepoll-server.herokuapp.com/results' 
	oninput='document.getElementsByName("output")[0].src="about:blank"' 
	method="POST" 
	onsubmit="this.submit(); this.reset();">
	<div class='header'>
		<div class='selectSession'>
			Выберите сессию
			<select class='sessionSelect' name='sessionId'>
				{#each sessions as session}
					<option value={session.id}>{session.name}</option>
				{:else}
					<option>Загрузка....</option>
				{/each}
			</select>
		</div>
		<input class='usernameInput' type="text" placeholder="Введите имя" name='username'>
	</div>

	<table class='dataInputs'>
	<tr>
		<td>Ф(А)</td>
		<td><input type=number bind:value={fa} name="fa" min=0 max=10></td>
		<td>Ф(Д)</td>
		<td><input type=number bind:value={fd} name="fd" min=0 max=10 value="5"></td>
	</tr>
	<tr>
		<td>C(А)</td>
		<td><input type=number bind:value={ca} name="ca" min=0 max=10></td>
		<td>C(Д)</td>
		<td><input type=number bind:value={cd} name="cd" min=0 max=10 value="5"></td>
	</tr>
	<tr>
		<td>И(А)</td>
		<td><input type=number bind:value={ia} name="ia" min=0 max=10 value="5"></td>
		<td>И(Д)</td>
		<td><input type=number bind:value={id} name="id" min=0 max=10 value="5"></td>
	</tr>
	</table>

	<button type="submit" formtarget="output">Готово</button>
</form>

<iframe title='output' name="output"></iframe>