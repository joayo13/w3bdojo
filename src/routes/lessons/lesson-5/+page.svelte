<script>
	import CodeBlock from '../../../components/CodeBlock.svelte';
	import LessonLink from '../../../components/LessonLink.svelte';
	import Quiz from '../../../components/Quiz.svelte';
	import RadioGroup from '../../../components/RadioGroup.svelte';
	const codeSnippetRemoveSlider = `@media (prefers-reduced-motion: reduce) {
  .slider {
    transform: translateX(0);
    transition: none;
  }
}
`;
	const codeSnipperRemoveAllAnimations = `@media (prefers-reduced-motion: reduce) {
  * {
    animation: none !important;
    transition: none !important;
  }
}
`;
</script>

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
<h2 class="mt-8 text-2xl">Legibility of Text</h2>
<p class="mt-2">
	The bulk of most websites is information conveyed through text. That is why when we choose a font,
	we must consider its readability. As a general rule, only use decorative text for big headers, and
	use it sparingly. When using a font for body text, ensure that it is a font meant for viewing at
	small sizes. W3b Dojo uses the default system font. You may want something with a bit more style,
	but just remember that you want your fonts to be nice and readable, even at small sizes. Common
	examples include Lato, Open Sans, Inter, Roboto.
</p>
<p class="mt-2">
	Another way that readability is impacted is by letter spacing and line height. Letter spacing can
	usually be left alone provided you choose a nice standard font as discussed above. But for
	line-height, between 1.5 to 1.75 is a good range for main paragraph content. This is set with the
	line-height property in CSS, and the values can be unitless, so “line-height:1.5;” will work just
	fine! When in doubt, go with 1.5. Here, we use 1.625 for our paragraph content.
</p>
<h2 class="mt-8 text-2xl">Rem & Ems</h2>
<p class="mt-2">
	When starting out designing websites with CSS, it is common to use the px unit for everything, as
	it is easy to reason about. One of the main problems with using px, is when a user tries to zoom
	in the size will stay the same regardless. That’s because px is meant for when you want the size
	of something to be fixed.
</p>
<p class="mt-2">
	Rems and ems are meant for when you want the size to be responsive. The term em comes from the
	world of typography, where an “em” is literally the width of a capital M in a typeface. But you
	can just think of it as the size relative to font-size. So if a container has a font-size of 16px,
	2em is double that: 32px. Now a rem just means root-em, as in the root font-size being used (in
	&lt;html &gt;). This is 16px by default. To summarize, em is taking the size of the parents
	font-size as a multiplier, and rem is doing the same but on the root &lt;html&gt;.
</p>
<h2 class="mt-8 text-2xl">Use Prefers Reduced Motion</h2>
<p class="mt-2">
	We use prefers-reduced-motion for users that may get motion-sickness, or suffer from epilepsy.
	They don’t need to be seeing all your wacky animations. So we will accommodate them!
</p>
<CodeBlock language="css" code={codeSnippetRemoveSlider} />
<p class="mt-2">
	Here’s an example of how we could override the slider animation, so it instead pops in and out
	without sliding or doing anything too crazy. Or if you just want to disable it all for them:
</p>
<CodeBlock language="css" code={codeSnipperRemoveAllAnimations} />
<Quiz
	><RadioGroup
		name="What do the numbers 4.5:1 indicate?"
		options={['Controls the arias', 'K/D Ratio', 'Contrast Ratio', 'All of the above']}
		correctAnswer="Contrast Ratio"
	/>
	<RadioGroup
		name="Which unit is responsive?"
		options={['px', 'inches', 'rems', 'None of the above']}
		correctAnswer="rems"
	/>
	<RadioGroup
		name="Which of these are a suitable line-height for paragraph text?"
		options={['Over 9000', '1.5', '1.45', 'None of the above']}
		correctAnswer="1.5"
	/>
</Quiz>
<LessonLink text="Return to home" href="/" />
