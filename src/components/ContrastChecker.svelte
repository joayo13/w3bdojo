<script lang="ts">
	interface ContrastResult {
		ratio: string;
		passesAANormal: boolean;
		passesAAANormal: boolean;
		passesAALarge: boolean;
		passesAAALarge: boolean;
	}

	function getLuminance(r: number, g: number, b: number): number {
		const a = [r, g, b].map((v) => {
			v /= 255;
			return v <= 0.03928 ? v / 12.92 : Math.pow((v + 0.055) / 1.055, 2.4);
		});
		return a[0] * 0.2126 + a[1] * 0.7152 + a[2] * 0.0722;
	}

	function hexToRgb(hex: string): [number, number, number] {
		hex = hex.replace(/^#/, '');
		const bigint = parseInt(
			hex.length === 3
				? hex
						.split('')
						.map((c) => c + c)
						.join('')
				: hex,
			16
		);
		const r = (bigint >> 16) & 255;
		const g = (bigint >> 8) & 255;
		const b = bigint & 255;
		return [r, g, b];
	}

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
	let color2: string = '#ffffff';
	let contrastResult: ContrastResult | null = calculateContrastRatio(color1, color2);
</script>

<div class="my-12 space-y-6 rounded-xl text-slate-800 dark:text-slate-100">
	<div class="space-y-4">
		<div class="flex items-center gap-4">
			<input
				type="color"
				bind:value={color1}
				class="h-12 w-12 rounded border"
				on:input={() => (contrastResult = calculateContrastRatio(color1, color2))}
			/>
			<input
				type="text"
				bind:value={color1}
				class="flex-1 rounded border p-2 dark:border-slate-700 dark:bg-slate-800"
				on:input={() => (contrastResult = calculateContrastRatio(color1, color2))}
			/>
		</div>
		<div class="flex items-center gap-4">
			<input
				type="color"
				bind:value={color2}
				class="h-12 w-12 rounded border"
				on:input={() => (contrastResult = calculateContrastRatio(color1, color2))}
			/>
			<input
				type="text"
				bind:value={color2}
				class="flex-1 rounded border p-2 dark:border-slate-700 dark:bg-slate-800"
				on:input={() => (contrastResult = calculateContrastRatio(color1, color2))}
			/>
		</div>
	</div>

	{#if contrastResult}
		<div class="space-y-3 rounded-md bg-white p-4 dark:bg-slate-800">
			<h3 class="text-3xl">Contrast Ratio Results</h3>
			<p class="text-3xl font-bold">
				Ratio: <span class="font-mono">{contrastResult.ratio}:1</span>
			</p>

			<div>
				<h4 class="font-bold">WCAG Compliance</h4>
				<ul class=" space-y-1">
					<li>
						Normal Text AA:
						<span class="font-bold">
							{contrastResult.passesAANormal ? 'PASS' : 'FAIL'}
						</span>
					</li>
					<li>
						Normal Text AAA:
						<span class="font-bold">
							{contrastResult.passesAAANormal ? 'PASS' : 'FAIL'}
						</span>
					</li>
					<li>
						Large Text AA:
						<span class="font-bold">
							{contrastResult.passesAALarge ? 'PASS' : 'FAIL'}
						</span>
					</li>
					<li>
						Large Text AAA:
						<span class="font-bold">
							{contrastResult.passesAAALarge ? 'PASS' : 'FAIL'}
						</span>
					</li>
				</ul>
			</div>
		</div>
	{/if}
</div>
