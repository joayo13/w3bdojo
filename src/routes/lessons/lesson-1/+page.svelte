<script lang="ts">
	import { addNotification } from '$lib/stores/notifications';
	import CodeBlock from '../../../components/CodeBlock.svelte';
	import LessonLink from '../../../components/LessonLink.svelte';
	import Quiz from '../../../components/Quiz.svelte';
	import RadioGroup from '../../../components/RadioGroup.svelte';
	import Confetti from 'svelte-confetti';
	let tabToMeConfetti = $state(false);
	let selectMeConfetti = $state(false);
	function handleSelectChange(e: Event) {
		const value = (e.target as HTMLSelectElement).value;
		if (value === 'Spongebob') {
			addNotification('🔥 Selectacular 🔥');
			selectMeConfetti = true;
		}
	}
</script>

<svelte:head>
	<title>Lesson 1: Keyboard Navigation and Semantic HTML | W3b Dojo</title>
	<meta
		name="description"
		content="Learn about keyboard navigation and semantic HTML for web accessibility. Understand how to make your websites accessible to users who rely on keyboard navigation."
	/>
	<meta
		name="keywords"
		content="keyboard navigation, semantic HTML, web accessibility, a11y, focus management"
	/>
</svelte:head>

<h1 class="text-4xl font-semibold">Keyboard Navigation and Semantic HTML</h1>
<p class="mt-8">
	Getting keyboard navigation right not only assists people with motor and visual disabilities, but
	also power-users! It's a must have on any website and this lesson will introduce you to how you
	can use your keyboard to navigate, and the native HTML elements we can use with keyboard support
	built in.
</p>
<h2 class="mt-8 text-2xl">1a: How does keyboard navigation work?</h2>
<p class="mt-2">
	There are many types of elements or "tags" within HTML. Most commonly seen are tags such as
	"a"(otherwise known as anchor tags, these are what links are on a page), "button", "select" etc.
	We will stick to these as they are simple examples. If you didn't already know, you can navigate
	through elements by using tab to move forwards, and shift + tab to move backwards.
</p>
<p class="mt-2">
	Notice how if you press your tab key to navigate forward or shift+tab to navigate backward, when
	navigating to the button below it will have a white line around it to indicate that it is in a
	"focus" state.
</p>
<p class="mt-2">
	Pressing the "Enter" or "Space" key will trigger the associated action on the element. Try doing
	that to the button.
</p>
<button
	onclick={() => {
		addNotification('Fantabstic! 🎉');
		tabToMeConfetti = true;
	}}
	class="tab-button relative my-8 rounded-sm border border-inherit px-4 py-2 text-2xl"
	>Tab to me!
	<div class="mx-auto w-10">
		{#if tabToMeConfetti}
			<Confetti rounded={true} amount={100} fallDistance={'10rem'} x={[-2, 2]} />
		{/if}
	</div>
</button>
<p>
	Now Let's interact with the "select" tag that has a few corresponding "option"s. Use tab or shift
	+ tab as before followed by Enter or Space, but once selected, you can navigate the options with
	the arrow keys. Navigate to "Spongebob" and press Enter or Space key.
</p>
<div class="w-fit">
	<select
		aria-label="Select an option"
		class="my-8 rounded-md border border-slate-900 bg-slate-200 px-2 py-2 text-slate-900 dark:border-slate-200 dark:bg-slate-800 dark:text-slate-100"
		onchange={handleSelectChange}
	>
		<option>Shrek</option>
		<option>Spiderman</option>
		<option>Spongebob</option>
	</select>
	<div class="mx-auto w-10">
		{#if selectMeConfetti}
			<Confetti rounded={true} amount={100} fallDistance={'10rem'} x={[-2, 2]} />
		{/if}
	</div>
</div>
<p>
	As you can see, these tags are already designed to handle keyboard navigation, which is very
	convenient for us as developers. This leads us into an important realization: using the correct
	HTML tags for the job will make a web application accessible by default.
</p>
<h2 class="mt-8 text-2xl">1b: Semantic HTML > Custom Roles and Attributes</h2>
<p class="mt-2">
	By understanding what HTML tags to use for the job, we can already make accessible applications!
	But there are some cases where we need to add styles or functionality that the native tag does not
	offer. This is often seen with the select element. As you may have noticed, it looks rather bland.
	And it can only be stylized to a certain extent. If we wanted to, we could build one from scratch
	with a div. Then we would be able to control all of the styles 100%. However, just a div alone
	would now strip away the accessibility that came with the select element. How do we handle this?
	That is where we use roles and attributes.
</p>

<CodeBlock
	language="html"
	code="<div role='select' aria-expanded='false' aria-haspopup='listbox' tabindex='0' aria-labelledby='select-label'>
	    <span id='select-label'>Choose an option</span>
	  </div>"
/>

<h3 class="text-2xl">Explanation of the Attributes</h3>
<ol class="mt-2 flex flex-col gap-2">
	<li>
		<h4 class="font-mono font-bold text-green-800 dark:text-green-500">role ="select"</h4>
		<p>Indicates that the element acts as a custom select dropdown.</p>
	</li>
	<li>
		<h4 class="font-mono font-bold text-green-800 dark:text-green-500">aria-expanded="false"</h4>
		<p>
			Specifies whether the dropdown is expanded (true) or collapsed (false). Update this
			dynamically when the dropdown opens or closes.
		</p>
	</li>
	<li>
		<h4 class="font-mono font-bold text-green-800 dark:text-green-500">aria-haspopup="listbox"</h4>
		<p>Indicates that the dropdown will display a listbox (typically the dropdown options).</p>
	</li>
	<li>
		<h4 class="font-mono font-bold text-green-800 dark:text-green-500">tabindex="0"</h4>
		<p>
			Makes the div focusable via keyboard navigation. Users can navigate to it with the Tab key.
		</p>
	</li>
	<li>
		<h4 class="font-mono font-bold text-green-800 dark:text-green-500">
			aria-labelledby="select-label"
		</h4>
		<p>
			Associates the div with an element id ("span" in this case) so screen readers announce what
			the dropdown represents. The label text is "Choose an option" in this example.
		</p>
	</li>
</ol>
<p class="mt-8">
	That was exhausting.. All of this just to emulate what was already there in the select tag. And we
	haven't even added support for using the up and down arrow keys on the options. Now you can see
	why it is best to avoid custom implementations like this as much as possible. Just remember,
	native HTML elements are accessible by default!
</p>
<Quiz
	><RadioGroup
		name="Who benefits from accessible web applications?"
		options={[
			'Visually Impaired Users',
			'Physically Disabled Users',
			'Cognitively Impaired Users',
			'All of the above'
		]}
		correctAnswer="All of the above"
	/>
	<RadioGroup
		name="What do you use to add accessibility to an element?"
		options={[
			'Roles and Attributes',
			'Classes and Attributes',
			'Roles and Alternatives',
			'All of the above'
		]}
		correctAnswer="Roles and Attributes"
	/>
	<RadioGroup
		name="What does aria-labelledby do?"
		options={[
			'Associates an element to another with an id',
			'Associates an element to another with a classname',
			'Labels the aria',
			'None of the above'
		]}
		correctAnswer="Associates an element to another with an id"
	/>
</Quiz>
<LessonLink href="/lessons/lesson-2" text="Start Lesson 2" />
