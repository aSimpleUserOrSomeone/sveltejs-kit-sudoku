<script>
	console.log('Page Load')
	//https://rapidapi.com/gregor-i/api/sudoku-generator1

	const options = {
		method: 'GET',
		headers: {
			'X-RapidAPI-Key': 'SIGN-UP-FOR-KEY',
			'X-RapidAPI-Host': 'sudoku-generator1.p.rapidapi.com'
		}
	};	

	fetch('https://sudoku-generator1.p.rapidapi.com/sudoku/generate?seed=1337', options)
		.then(response => response.json())
		.then(response => console.log(response))
		.catch(err => console.error(err));

	const sudoku = {
		seed:1337,
		difficulty:"Easy",
		puzzle:"...465......2..7..9....76..6....234..15...2.9.4...8........6..17.1...9.3..9...5.."
	}
	let sudokuBuffer = [...sudoku.puzzle]
	const sudokuArray = []
	while(sudokuBuffer.length) {
		sudokuArray.push(sudokuBuffer.splice(0,3))
	}
	console.log(sudokuArray)
</script>

<div class='sudoku-grid'>
{#each sudokuArray as row}
	{#each row as cell}
		<div class="cell">
		{#if cell != '.'}
			{cell}
		{/if}
		</div>
	{/each}
{/each}
</div>

<style>
@import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap');

.sudoku-grid {
	margin: 140px auto auto auto;
	width: fit-content;
	aspect-ratio: 1;
	display: grid;
	grid-template-rows: repeat(9, 7.5vmin);
	grid-template-columns: repeat(9, 7.5vmin);
	gap: 0.1rem;

	background-color: #1f1f1f;
}

.cell {
	user-select: none;
	box-sizing: border-box;
	background-color: var(--color-bg-2);

	display: flex;
	justify-content: center;
	align-items: center;
	font-family: 'Share Tech Mono', monospace;
	font-weight: 600;
}

.cell:not(.forever)
</style>
