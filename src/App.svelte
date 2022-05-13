<script>
	// Quiz Q & A
	let questions = [
		{
			question: '2 + 2',
			options: ['2', '5', '4', '3'],
			correctIndex: 2,
		},
		{
			question: '5 + 2',
			options: ['7', '9', '3', '6'],
			correctIndex: 0,
		},
		{
			question: '4 + 2',
			options: ['5', '2', '6', '8'],
			correctIndex: 2,
		},
		{
			question: '6 + 3',
			options: ['8', '4', '7', '9'],
			correctIndex: 3,
		},
		{
			question: '3 + 2',
			options: ['8', '9', '5', '6'],
			correctIndex: 2,
		},
		{
			question: '4 + 4',
			options: ['5', '8', '4', '7'],
			correctIndex: 1,
		},
		{
			question: '5 + 5',
			options: ['8', '5', '7', '10'],
			correctIndex: 3,
		},
		{
			question: '5 + 3',
			options: ['8', '5', '4', '6'],
			correctIndex: 0,
		},
		{
			question: '3 + 2',
			options: ['2', '4', '5', '6'],
			correctIndex: 2,
		},
		{
			question: '4 + 3',
			options: ['6', '7', '8', '9'],
			correctIndex: 1,
		},
	];
	let answers = new Array(questions.length).fill(null);
	let questionPointer = -1;

	//functions
	function getScore() {
		let score = answers.reduce((acc, val, index) => {
			if (questions[index].correctIndex == val) {
				return acc + 1;
			}
			return acc;
		}, 0);
		return (score / questions.length) * 100 + '%';
	}
	function restartQuiz() {
		answers = new Array(questions.length).fill(null);
		questionPointer = 0;
	}
</script>

<style>
	button {
		font-weight: bold;
		cursor: pointer;
	}
	.app {
		position: absolute;
		top: 0;
		left: 0;
		width: 100vw;
		height: 100vh;
	}
	.app > div {
		width: 100%;
		height: 100%;
	}
	.title {
		position: absolute;
		text-align: center;
		margin: 0;
		padding: 1.5rem 0;
		width: 100%;
		font-size: 3rem;
		background-color: #4a77dc;
		color: #eee;
	}
	.start-screen,
	.score-screen {
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.start-screen button,
	.score-screen button {
		padding: 10px 20px;
		background-color: #4a77dc;
		color: #eee;
		border: none;
		outline: none;
		border-radius: 20px;
		transition: 0.4s ease-in-out;
	}
	.start-screen button:hover,
	.score-screen button:hover {
		background-color: #eee;
		color: #4a77dc;
		border: 2px solid #4a77dc;
	}
	.main {
		padding: 50px;
	}
	.main h2 {
		text-align: center;
		font-size: 2rem;
	}
	.options {
		display: flex;
		justify-content: space-between;
		flex-wrap: wrap;
	}
	.options button {
		width: 45%;
		margin: 10px 0;
		border-radius: 20px;
		transition: 0.1s ease-in-out;
	}
	.options button:hover {
		outline: 2px solid #4a77dc;
	}
	.options button.selected {
		background-color: #4a77dc;
		color: #eee;
	}
	.footer {
		position: absolute;
		bottom: 0;
		left: 0;
		width: 100%;
		height: 50px;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	.footer > div {
		margin: 0 10px;
	}
	.progress-bar {
		height: 10px;
		width: 150px;
		background: #aaa;
		border-radius: 10px;
		overflow: hidden;
	}
	.progress-bar div {
		height: 100%;
		background: #4a77dc;
	}
	.buttons {
		display: flex;
		justify-content: space-around;
		width: 50%;
	}
	.buttons .left,
	.buttons .right {
		width: 48%;
		background-color: #4a77dc;
		color: #eee;
		border-radius: 20px;
		cursor: pointer;
	}
	.score-screen {
		flex-direction: column;
	}
	.score-screen h1 {
		margin-bottom: 10px;
	}
</style>

<div class="app">
	{#if questionPointer == -1}
		<h1 class="title">Starting Math</h1>
		<div class="start-screen">
			<button
				on:click={() => {
					questionPointer = 0;
				}}
			>
				Start Quiz
			</button>
		</div>
	{:else if !(questionPointer > answers.length - 1)}
		<div class="quiz-screen">
			<div class="main">
				<h2>
					{questions[questionPointer].question}
				</h2>

				<div class="options">
					{#each questions[questionPointer].options as opt, i}
						<button
							class={answers[questionPointer] == i ? 'selected' : ''}
							on:click={() => {
								answers[questionPointer] = i;
							}}
						>
							{opt}
						</button>
					{/each}
				</div>
			</div>
			<div class="footer">
				<div class="progress-bar">
					<div style="width: {(questionPointer / questions.length) * 100}%" />
				</div>
				<div class="buttons">
					<button
						class="left"
						on:click={() => {
							questionPointer--;
						}}
					>
						&lt;
					</button>
					<button
						class="right"
						on:click={() => {
							questionPointer++;
						}}
					>
						&gt;
					</button>
				</div>
			</div>
		</div>
	{:else}
		<div class="score-screen">
			<h1>
				Your score: {getScore()}
			</h1>
			<button on:click={restartQuiz}> Restart Quiz </button>
		</div>
	{/if}
</div>
