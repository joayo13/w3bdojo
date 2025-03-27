<script lang="ts">
	// Interface for Contrast Result
	interface ContrastResult {
		ratio: string;
		passesAANormal: boolean;
		passesAAANormal: boolean;
		passesAALarge: boolean;
		passesAAALarge: boolean;
	}

	// Function to calculate relative luminance
	function getLuminance(r: number, g: number, b: number): number {
		const a = [r, g, b].map((v) => {
			v /= 255;
			return v <= 0.03928 ? v / 12.92 : Math.pow((v + 0.055) / 1.055, 2.4);
		});
		return a[0] * 0.2126 + a[1] * 0.7152 + a[2] * 0.0722;
	}

	// Function to convert hex to RGB
	function hexToRgb(hex: string): [number, number, number] {
		// Remove # if present
		hex = hex.replace(/^#/, '');

		// Handle 3-digit and 6-digit hex codes
		const bigint = parseInt(
			hex.length === 3
				? hex
						.split('')
						.map((char) => char + char)
						.join('')
				: hex,
			16
		);

		const r = (bigint >> 16) & 255;
		const g = (bigint >> 8) & 255;
		const b = bigint & 255;

		return [r, g, b];
	}

	// Calculate contrast ratio
	function calculateContrastRatio(color1: string, color2: string): ContrastResult | null {
		try {
			const [r1, g1, b1] = hexToRgb(color1);
			const [r2, g2, b2] = hexToRgb(color2);

			const l1 = getLuminance(r1, g1, b1);
			const l2 = getLuminance(r2, g2, b2);

			const lighter = Math.max(l1, l2);
			const darker = Math.min(l1, l2);

			const contrastRatio = (lighter + 0.05) / (darker + 0.05);

			return {
				ratio: contrastRatio.toFixed(2),
				passesAANormal: contrastRatio >= 4.5,
				passesAAANormal: contrastRatio >= 7,
				passesAALarge: contrastRatio >= 3,
				passesAAALarge: contrastRatio >= 4.5
			};
		} catch (error) {
			return null;
		}
	}

	let color1: string = '#000000';
	let color2: string = '#FFFFFF';
	let contrastResult: ContrastResult | null = calculateContrastRatio(color1, color2);
</script>

<div class="color-contrast-checker">
	<h2>Color Contrast Ratio Checker</h2>

	<div class="input-group">
		<label>
			Color 1:
			<input
				type="color"
				bind:value={color1}
				on:input={() => (contrastResult = calculateContrastRatio(color1, color2))}
			/>
			<input
				type="text"
				bind:value={color1}
				on:input={() => (contrastResult = calculateContrastRatio(color1, color2))}
			/>
		</label>

		<label>
			Color 2:
			<input
				type="color"
				bind:value={color2}
				on:input={() => (contrastResult = calculateContrastRatio(color1, color2))}
			/>
			<input
				type="text"
				bind:value={color2}
				on:input={() => (contrastResult = calculateContrastRatio(color1, color2))}
			/>
		</label>
	</div>

	{#if contrastResult}
		<div class="results">
			<h3>Contrast Ratio Results</h3>
			<p>Ratio: {contrastResult.ratio}:1</p>

			<div class="compliance">
				<h4>WCAG Compliance</h4>
				<ul>
					<li>
						Normal Text AA:
						{#if contrastResult.passesAANormal}
							<span class="pass">PASS</span>
						{:else}
							<span class="fail">FAIL</span>
						{/if}
					</li>
					<li>
						Normal Text AAA:
						{#if contrastResult.passesAAANormal}
							<span class="pass">PASS</span>
						{:else}
							<span class="fail">FAIL</span>
						{/if}
					</li>
					<li>
						Large Text AA:
						{#if contrastResult.passesAALarge}
							<span class="pass">PASS</span>
						{:else}
							<span class="fail">FAIL</span>
						{/if}
					</li>
					<li>
						Large Text AAA:
						{#if contrastResult.passesAAALarge}
							<span class="pass">PASS</span>
						{:else}
							<span class="fail">FAIL</span>
						{/if}
					</li>
				</ul>
			</div>
		</div>
	{/if}
</div>

<style>
	.color-contrast-checker {
		max-width: 400px;
		margin: 0 auto;
		padding: 20px;
		font-family: Arial, sans-serif;
	}

	.input-group {
		display: flex;
		flex-direction: column;
		gap: 10px;
		margin-bottom: 20px;
	}

	label {
		display: flex;
		align-items: center;
		gap: 10px;
	}

	input[type='color'] {
		width: 50px;
		height: 50px;
		padding: 0;
	}

	input[type='text'] {
		flex-grow: 1;
		padding: 5px;
	}

	.results {
		background-color: #f4f4f4;
		padding: 15px;
		border-radius: 5px;
	}

	.compliance ul {
		list-style-type: none;
		padding: 0;
	}

	.pass {
		color: green;
		font-weight: bold;
	}

	.fail {
		color: red;
		font-weight: bold;
	}
</style>
