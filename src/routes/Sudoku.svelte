<script>
	console.log('Page Load')

	fetch("../../static/sudokuData.json")
	.then(res => console.log(res))

	const sudoku = {
		seed:1337,
		difficulty:"Easy",
		puzzle:"...465......2..7..9....76..6....234..15...2.9.4...8........6..17.1...9.3..9...5.."
	}

	const sudokuBuffer = [...sudoku.puzzle]
	const sudokuArray = []
	while(sudokuBuffer.length) {
		sudokuArray.push(sudokuBuffer.splice(0,9))
	}
	
	let selectedNumber = null;

	function cellClicked(event) {
		if(selectedNumber == null) return
		const myCell = event.target
		myCell.textContent = selectedNumber
		const i = myCell.getAttribute("data-i-index")
		const j = myCell.getAttribute("data-j-index")

		selectThisCell(myCell)

		sudokuArray[i][j] = selectedNumber
	}

	let selectedCell = null;
	function selectThisCell(cell) {
		if(selectedCell != null) selectedCell.id = ''
		selectedCell = cell
		selectedCell.id = 'selected-cell'
	}

	let kC = 0
	function onKeyboardAction(event) {
		if (selectedCell == null) return
		let dir = ''
		let newCell = null
		let i = Number(selectedCell.getAttribute("data-i-index"))
		let j = Number(selectedCell.getAttribute("data-j-index"))

		
		switch(event.keyCode) {
			case 37:
				j--
				break
			case 38:
				i--
				break
			case 39:
				j++
				break
			case 40:
				i++
				break
		}

		var toBeSelected = (i * 9) + j + 1
		kC = toBeSelected
		if(toBeSelected > 81) {toBeSelected -=  81}
		else if(toBeSelected < 1) {toBeSelected += 81}

		newCell = document.querySelector(`.cell:nth-child(${toBeSelected})`)
		selectThisCell(newCell)
	}

</script>

<div class='sudoku-grid'>
{#each sudokuArray as row, i}
	{#each row as cell, j}
		{#if sudoku.puzzle[i*9 + j] != '.'}
			<div class="cell forever" data-i-index={i} data-j-index={j}>
				{cell}
			</div>
		{:else}
			<div class="cell" on:click={cellClicked} data-i-index={i} data-j-index={j}/>
		{/if}
	{/each}
{/each}
</div>
<div class="numbers-keyboard">
{#each [1,2,3,4,5,6,7,8,9] as number}
	<label>
		<input bind:group={selectedNumber} type="radio" name="number" id="{number}" value={number}>
		<span>{number}</span>
	</label>
{/each}
</div>
<svelte:window on:keydown|preventDefault={onKeyboardAction}/>

<style>
@import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap');

.numbers-keyboard {
	font-family: 'Share Tech Mono', monospace;
	width: fit-content;
	height: fit-content;
	margin: 1rem auto 0 auto;

	display: grid;
	grid-template-rows: repeat(3, 1fr);
	grid-template-columns: repeat(3, 1fr);
	gap: 0.3rem;
}
label {
	position: relative;
	width: 2rem;
	height: 2rem;
}
label > span {
	position: absolute;
	width: min-content;
	height: min-content;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
}
input[type='radio'] {
	position: absolute;
	width: 100%;
	height: 100%;
	top: 0%;
	left: 0%;
	background-color: "black";
	border: 2px solid black;
	border-radius: 50%;

}
input[type="radio"]:checked {
	background-color: 'black';
}
input[type="radio"]:checked ~ span:first-of-type {
  color: white;
}

.sudoku-grid {
	margin: 140px auto auto auto;
	width: fit-content;
	height: fit-content;
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
	color: #6f6f6f;

	display: flex;
	justify-content: center;
	align-items: center;
	font-family: 'Share Tech Mono', monospace;
	font-weight: 600;
}
.cell.forever {
	color: #0f0f0f;
}

#selected-cell:not(.forever) {
	background-color: #6699CC;
	color: white;
}

#selected-cell {
	background-color: #e0e0e0;
	color: grey;
}
</style>
