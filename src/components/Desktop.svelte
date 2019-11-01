<script>
	export let sessions;

</script>

<style>
    form {
        margin: 0 auto;
        width: 50%;
        padding: 5px 10px;
        display: flex;
        flex-direction: column;
        justify-items: center;
    }

    table {
        display: flex;
        justify-content: space-around;
        align-items: center;
    }

    .name-input {
        display: flex;
        justify-content: center;
    
    }

    .selectSession {
        display: flex;
        width: fit-content;
        margin: 10px auto;
    }

    select {
        margin: 0;
    }

    .select-lable {
        margin: auto 5px;
    }

    .lector-checkbox,
    .usernameInput {
        margin: 0 5px;
    }

    .lector-label {
        height: fit-content;
        margin: auto 5px auto 0px;
    }

    table {
        border-spacing: 10px;
    }
    
    .comments {
        align-self: center;
        display: flex;
        flex-direction: column;
    }

    textarea {
        width: 100%;
        align-self: center;
    }

    .buttons {
        align-self: center;
        display: flex;
        width: 60%;
        justify-content: space-around;
        margin: 5px 0;
    }

    button {
        padding: 10px;
        width: 30%;
    }

    iframe {
        align-self: center;
        border: 0;
    }
</style>

<form action='https://realtimepoll-server.herokuapp.com/results' 
	oninput='document.getElementsByName("output")[0].src="about:blank"' 
	method="POST" >
	<div class='header'>
		<div class='selectSession'>
			<label class='select-lable'>Выберите сессию</label>
			<select class='sessionSelect' name='sessionId'>
				{#each sessions as session}
					<option value={session.id}>{session.name}</option>
				{:else}
					<option>Загрузка....</option>
				{/each}
			</select>
		</div>
        <div class='name-input'>
            <label for="lector" class='lector-label'>Я - лектор <input type="checkbox" name="lector" id="lector" class='lector-checkbox'></label>
		    <input class='usernameInput' type="text" placeholder="Введите имя" name='username'>
        </div>
	</div>

	<table class='dataInputs'>
	<tr>
		<td>Форма <input type=number name="form" min=0 max=10 placeholder=5></td>
        <td>Содержание <input type=number name="content" min=0 max=10 placeholder=5></td>
        <td>Интерес <input type=number name="interest" min=0 max=10 placeholder=5></td>
	</tr>
	</table>

    <div class = 'comments'>
	    <p class='comment_title'>Напиши, что ты думаешь о лекции и о лекторе, что понравилось, а что можно подтянуть</p>
	    <textarea name='comment' cols="20" rows="5"></textarea>
    </div>
    <div class = 'buttons'>
	    <button type="reset">Очистить</button>
	    <button type="submit" formtarget="output">Готово</button>
    </div>
    <iframe title='output' name="output"></iframe>
</form>
