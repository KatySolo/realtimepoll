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

    .header,
    table {
        display: flex;
        justify-content: space-around;
        align-items: center;
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
			Выберите сессию
			<select class='sessionSelect' name='sessionId'>
				{#each sessions as session}
					<option value={session.id}>{session.name}</option>
				{:else}
					<option>Загрузка....</option>
				{/each}
			</select>
		</div>
         <div class='lector_checkbox'>
            Я - лектор 
            <input type="checkbox" name="lector">
        </div>
		<input class='usernameInput' type="text" placeholder="Введите имя" name='username'>
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
