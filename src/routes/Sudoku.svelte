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
	console.log(sudokuData)
</script>

<div >
</div>

<style>

</style>
