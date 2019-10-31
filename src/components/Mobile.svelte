<script>
	export let sessions;

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
		display: block;
	}

	.comment_title {
		width: 250px;
		font-size: 16px;
	}

</style>

<form action='https://realtimepoll-server.herokuapp.com/results' 
	oninput='document.getElementsByName("output")[0].src="about:blank"' 
	method="POST" >
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
		<td>Я - лектор</td>
		<td><input type="checkbox" name="lector"></td>
	</tr>
	<tr>
		<td>Форма</td>
		<td><input type=number name="form" min=0 max=10 placeholder=5></td>
	</tr>
	<tr>
		<td>Содержание</td>
		<td><input type=number name="content" min=0 max=10 placeholder=5></td>
	</tr>
	<tr>
		<td>Интерес</td>
		<td><input type=number name="interest" min=0 max=10 placeholder=5></td>
	</tr>
	</table>

	<p class='comment_title'>Напиши, что ты думаешь о лекции и о лекторе, что понравилось, а что можно подтянуть</p>
	<textarea name='comment' cols="20" rows="5"></textarea>

	<button type="reset">Очистить</button>
	<button type="submit" formtarget="output">Готово</button>
</form>

<iframe title='output' name="output"></iframe>