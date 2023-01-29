<script>
	let rowCount = 0;
	let colCount = 0;
	function display() {
		const table = document.getElementById("table");
		const htmlCode = table.outerHTML;
		let textarea = document.querySelector(".result_text");
		textarea.value = htmlCode;
	}
	function handleSubmit(event) {
		event.preventDefault();
	}
	function reset() {
		rowCount = 0;
		colCount = 0;
	}

	async function copyToClipboard() {
	try {
		const textarea = document.querySelector(".result_text");
		await navigator.clipboard.writeText(textarea.value);
		let success = document.querySelector(".Success-Copy")
		console.log("Copied")
		success.innerHTML = "Copied Successfully!"
		setTimeout(() =>
		success.innerHTML = " ",4500)
	} catch (err) {
		console.error('Failed to copy text: ', err);
	}
	}
</script>

<main>
	<body>
		<h1>HTML Code Generator</h1>
		<form on:submit|preventDefault={handleSubmit}>
			<div class="labels">
				<label>
					Number of Rows:
					<input type="number" bind:value={rowCount} />
				</label>
				<label>
					Number of Columns:
					<input type="number" bind:value={colCount} />
				</label>
			</div>
			<div class="buttons">
				<button class="btn" type="button" on:click={reset}>Reset</button>
				<button class="btn focus" type="button" on:click={display}>Display Code</button>
				<button type="button" class="btn cpy-button focus" on:click={copyToClipboard}>Copy</button>
			</div>
			<div class = "Success-Copy"></div>
		</form>
		<table id="table">
			<tr class="border">
				{#each Array.from({ length: colCount }, (_, i) => i + 1) as col}
					<th class="border">Header {col}</th>
				{/each}
			</tr>
			{#each Array.from({ length: rowCount }, (_, i) => i + 1) as row}
				<tr class="border">
					{#each Array.from({ length: colCount }, (_, i) => i + 1) as col}
						<td class="border">{`${row},${col}`}</td>
					{/each}
				</tr>
			{/each}
		</table>
		<div class="result">
			<textarea class="result_text" type="text" rows="5" />
		</div>
	</body>
</main>

<style>
	@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@600&display=swap");

	* {
		margin: 0;
		padding: 0;
		font-family: "Poppins", sans-serif;
	}

	.border {
		border: 1px solid black;
	}

	body {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	form {
		margin-top: 3.5%;
	}
	label {
		margin-left: 50px;
		font-size: 25px;
	}
	h1{
		background-color: black;
		color: white;
		margin-top: 10%;
		border-radius: 10px;
		padding: 0px 15px;
	}
	textarea {
		margin-top: 20px;
		height: 400px;
		width: 400px;
		border-radius: 10px;
		box-shadow: 0px 0px 0px 2px rgba(0, 0, 0, 0.05),
			0px 15px 30px rgba(0, 0, 0, 0.12);
	}
	.btn {
		height : 50px;
		width: 160px;
		box-sizing: border-box;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		padding: 8px 14px;
		gap: 8px;
		position: relative;
		background: #0066ff;
		border: 1px solid #0066ff;
		border-radius: 8px;
		color: #eeeeee;
		font-size: 18px;
	}

	input {
		background: #ffffff;
		box-shadow: 0px 0px 0px 1px rgba(0, 0, 0, 0.05),
			0px 15px 30px rgba(0, 0, 0, 0.12);
		border-radius: 8px;
		padding-left: 5px;
		height: 40px;
		width: 200px;
		font-size: 25px;
	}
	.buttons {
		display: flex;
		gap: 10px;
		justify-content: center;
		margin-top: 30px;
	}

	.btn:hover {
		background-color: #000;
		cursor: pointer;
	}

	.focus:focus {
		background: #12b76a;
	}

	.Success-Copy{
		margin-top: 20px;
		text-align: center;
	}
</style>
