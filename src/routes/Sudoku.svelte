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
</script>

<div >

</div>

<style>

</style>
