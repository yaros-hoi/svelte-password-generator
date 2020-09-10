<script>
	const UPPERCASE_LETTERS = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
	const LOWERCASE_LETTERS = 'abcdefghijklmnopqrstuvwxyz';
	const NUMBERS = '0123456789';
	const SYMBOLS = '!@#$%^&*()_+=';

	let result = '';
	let checkedUpperCase = true;
	let checkedLowerCase = true;
	let checkedNumbers = true
	let checkedSymbols = true;
	let lengthPassword = 15;
	$: isDisabled = checkedUpperCase || checkedLowerCase || checkedNumbers || checkedSymbols;

	const getRandomValue = (type) => {
		return type[Math.floor(Math.random() * type.length)];
	};

	const generatePassword = () => {
		result = '';

		if (checkedUpperCase) {
			result += getRandomValue(UPPERCASE_LETTERS);
		}

		if (checkedLowerCase) {
			result += getRandomValue(LOWERCASE_LETTERS);
		}

		if (checkedNumbers) {
			result += getRandomValue(NUMBERS);
		}

		if (checkedSymbols) {
			result += getRandomValue(SYMBOLS);
		}

		for (let i = result.length; i < lengthPassword; i++) {
			const x = generateValue();
			result += x;
		}
	}

	const generateValue = () => {
		const value = [];

		if (checkedUpperCase) {
			value.push(getRandomValue(UPPERCASE_LETTERS));
		}

		if (checkedLowerCase) {
			value.push(getRandomValue(LOWERCASE_LETTERS));
		}

		if (checkedNumbers) {
			value.push(getRandomValue(NUMBERS));
		}

		if (checkedSymbols) {
			value.push(getRandomValue(SYMBOLS));
		}

		if (value.length === 0) return '';

		return getRandomValue(value);
	}
</script>

<div class="generator">
	<div class="form-item">
		<label for="length">Password Length</label>
		<input id="length" bind:value={lengthPassword} type="number" min="4" max="30">
	</div>
	<div class="form-item">
		<label for="upper">Contain Uppercase Letters</label>
		<input id="upper" type="checkbox" bind:checked={checkedUpperCase}>
	</div>
	<div class="form-item">
		<label for="lower">Contain Lowercase Letters</label>
		<input id="lower" type="checkbox" bind:checked={checkedLowerCase}>
	</div>
	<div class="form-item">
		<label for="number">Contain Numbers</label>
		<input id="number" type="checkbox" bind:checked={checkedNumbers}>
	</div>
	<div class="form-item">
		<label for="symbol">Contain Symbols</label>
		<input id="symbol" type="checkbox" bind:checked={checkedSymbols}>
	</div>
	<div class="form-item">
		<button on:click={generatePassword} disabled={!isDisabled}>Generate</button>
		<span>{result}</span>
	</div>
</div>

<style>
	.generator {
		max-width: 380px;
		margin: 0 auto;
	}

	.form-item {
		padding: 10px 0;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.generator-item input {
		margin-bottom: 0;
	}
</style>
