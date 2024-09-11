<script>
	let display = "NKǑ' SÁHWŪ: RESULAM.COM"; // Default text for the calculator display
	let isFirstClick = true; // Flag to check if it's the first button click
	let resultDisplayed = false; // Flag to check if the result is currently displayed

	// Mapping dictionary for custom text labels to numbers
	const charToNumberMap = {
		"Nshʉ̀'": '1',
		'Pʉ́ɑ́': '2',
		'Tāā': '3',
		'Kwɑ̀': '4',
		'Tî': '5',
		'Ntòhō': '6',
		'Sə̀ə̀mbʉ́ɑ́': '7',
		'Hə̀ə̄': '8',
		"Vʉ̀'ʉ̄": '9',
		'Nèhē': '0'
	};

	// Function to handle button clicks
	function handleButtonClick(value) {
		if (isFirstClick) {
			// Clear the display on the first click
			display = '';
			isFirstClick = false; // Set the flag to false after the first click
		}

		if (value === 'C') {
			// Clear the display and reset to default
			display = "NKǑ' SÁHWŪ: RESULAM.COM";
			isFirstClick = true; // Reset the flag to true
			resultDisplayed = false; // Reset result displayed flag
		} else if (value === '=') {
			try {
				// Replace custom text with corresponding numbers using the mapping dictionary
				let expression = display;
				for (const [key, val] of Object.entries(charToNumberMap)) {
					expression = expression.split(key).join(val);
				}

				// Remove consecutive operators
				expression = expression.replace(/([+\-*/])\1+/g, '$1');
				// Handle cases like 4-+5, 3*/2 etc.
				expression = expression.replace(/([+\-*/])([+\-*/])/g, '$2');

				// Evaluate the expression if it's a valid mathematical operation
				const sanitizedDisplay = expression.replace(/[^0-9+\-*/.]/g, '');
				if (sanitizedDisplay.trim() === '') {
					display = 'Error'; // Display error if no valid mathematical expression is found
				} else {
					// Evaluate the sanitized expression
					display = eval(sanitizedDisplay).toString();
				}
				resultDisplayed = true; // Set flag to indicate result is displayed
			} catch (e) {
				// Display error if expression is invalid
				display = 'Error';
			}
		} else if (['+', '-', '*', '/'].includes(value)) {
			// Prevent multiple consecutive operators
			if (!/[\+\-\*\/]$/.test(display)) {
				display += value;
				resultDisplayed = false; // Reset result displayed flag
			}
		} else {
			// If a number is clicked after displaying the result, reset the display
			if (resultDisplayed) {
				display = '';
				resultDisplayed = false; // Reset result displayed flag
			}
			// For any other value (custom text), append it to the display
			display += value;
		}
	}
</script>

<style>
	body {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100vh;
		margin: 0;
		background-color: #f7f7f7;
	}

	.calculator {
		max-width: 450px;
		width: 100%;
		margin: 0 auto;
		padding: 15px;
    /* padding: 5px 15px 15px 15px; 
    sets the padding in the order of 
    top, right, bottom, and left: */
    padding: 2px 30px 15px 30px; 
    
		border: 1px solid #ddd;
		border-radius: 30px;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
		background-color: white;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

  

	.display {
		width: 100%;
		padding: 15px;
		margin-bottom: 20px;
		font-size: 24px;
		text-align: right;
		border: 1px solid #ccc;
		border-radius: 5px;
	}

	.buttons {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		gap: 10px;
		width: 100%;
		margin-bottom: 20px;
	}

	button {
		padding: 15px;
		font-size: 18px;
		border: none;
		background-color: #f0f0f0;
		border-radius: 5px;
		cursor: pointer;
		transition: background-color 0.2s;
	}

	button:hover {
		background-color: #27a986;
	}

	.footer {
		margin-top: 10px;
		font-size: 12px;
		text-align: center;
		color: #555;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.footer img {
		width: 30px; /* Adjust size as needed */
		margin-bottom: 5px; /* Space between the logo and text */
	}
</style>

<div class="calculator">

  <!-- Header for the calculator -->
	<h3 class="header">NKǑ' SÁHWŪ</h3>

	<!-- Display screen with default text -->
	<div class="display">{display}</div>

	<!-- Calculator buttons -->
	<div class="buttons">
		<button on:click={() => handleButtonClick("Nshʉ̀'")}>Nshʉ̀'</button>
		<button on:click={() => handleButtonClick('Pʉ́ɑ́')}>Pʉ́ɑ́</button>
		<button on:click={() => handleButtonClick('Tāā')}>Tāā</button>
		<button on:click={() => handleButtonClick('+')}>+</button>

		<button on:click={() => handleButtonClick('Kwɑ̀')}>Kwɑ̀</button>
		<button on:click={() => handleButtonClick('Tî')}>Tî</button>
		<button on:click={() => handleButtonClick('Ntòhō')}>Ntòhō</button>
		<button on:click={() => handleButtonClick('-')}>-</button>

		<button on:click={() => handleButtonClick('Sə̀ə̀mbʉ́ɑ́')}>Sə̀ə̀mbʉ́ɑ́</button>
		<button on:click={() => handleButtonClick('Hə̀ə̄')}>Hə̀ə̄</button>
		<button on:click={() => handleButtonClick("Vʉ̀'ʉ̄")}>Vʉ̀'ʉ̄</button>
		<button on:click={() => handleButtonClick('*')}>*</button>

		<button on:click={() => handleButtonClick('C')}>CWĀH</button>
		<button on:click={() => handleButtonClick('Nèhē')}>Nèhē</button>
		<button on:click={() => handleButtonClick('=')}>=</button>
		<button on:click={() => handleButtonClick('/')}>÷</button>
	</div>

	<!-- Footer with professional credits and logo -->
	<div class="footer">
		<img src="/assets/resulam_logo_egg_300_px.png" alt="Resulam Logo" />
		<div>
			© 2024 Resulam. Calculator designed by Shck Tchamna. <br>Visit us at <a href="https://www.resulam.com" target="_blank">www.resulam.com</a>
		</div>
	</div>
</div>
