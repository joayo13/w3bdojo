<h1 class="text-4xl">Visual Accessibility</h1>

<h2 class="mt-8 text-2xl">Use of color</h2>
<p class="mt-2">
	Here we’ll use our quiz sections as an example. Imagine if we changed the border colors to green
	for correct and red for incorrect answers. For someone who’s color blind, they wouldn’t even be
	able to tell what they got correct!
</p>
<p class="mt-2">
	This is why we chose to use text content and symbols to display information. While you can use
	colors to inform, you should always have other ways to display that information and never rely on
	color alone.
</p>
<h2 class="mt-8 text-2xl">Rules of contrast</h2>
<p class="mt-2">
	For users with poor vision or colorblind users, we also must ensure our elements have at the least
	these contrast ratios:
</p>
<ol class="mt-8 flex flex-col gap-2">
	<li>
		<h4 class="font-bold">Normal body text: 4.5:1</h4>
	</li>
	<li>
		<h4 class="font-bold">Other elements and larger text: 3:1</h4>
	</li>
</ol>
<p class="mt-8">You are right to ask: what do those numbers mean?</p>
<p class="mt-2">
	It’s two numbers that each reflect relative luminance (how bright a color is). Together, they
	create a contrast ratio. 21:1 being black on white. We won’t go over the math behind this but be
	aware of this ratio, and use your browsers accessibility dev tools or
	<a href="https://webaim.org/resources/contrastchecker/">Web aim's contrast checker</a> to make sure
	all your elements respect this ratio.
</p>
