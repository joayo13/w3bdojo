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

<section class="prose max-w-none lg:prose-xl dark:prose-invert">
	<h1>Keyboard Navigation and Semantic HTML</h1>

	<p>
		Getting keyboard navigation right not only assists people with motor and visual disabilities,
		but also power-users! It's a must have on any website and this lesson will introduce you to how
		you can use your keyboard to navigate, and the HTML elements we can use with keyboard support
		built in.
	</p>

	<h2>1a: How does keyboard navigation work?</h2>

	<p>
		There are many elements within HTML. Most commonly seen are elements such as "a" (a is for
		anchor, AKA links), "button", "select" etc. These are just some of the elements which support
		keyboard interactions.
	</p>

	<p>
		Notice how if you press your tab key to navigate forward or shift+tab to navigate backward, when
		navigating to the button below it will receive a border around it. That border indicates that it
		is in a "focus" state.
	</p>

	<p>
		Pressing the "Enter" or "Space" key on the button is the equivalent of clicking it. Try doing
		that to the button.
	</p>

	<button
		onclick={() => {
			addNotification('Fantabstic! 🎉');
			tabToMeConfetti = true;
		}}
		class="tab-button relative my-8 rounded-sm border border-inherit px-4 py-2 text-2xl"
	>
		Tab to me!
		<div class="mx-auto w-10">
			{#if tabToMeConfetti}
				<Confetti rounded={true} amount={100} fallDistance={'10rem'} x={[-2, 2]} />
			{/if}
		</div>
	</button>

	<p>
		Now let's interact with the select element. Use tab or shift + tab as before to focus it. But
		once focused, you can navigate its options with the arrow keys. Navigate to "Spongebob" and
		press the Enter or Space key.
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
		These elements are designed to handle keyboard navigation, which is very convenient for us as
		developers. This leads us to an important realization: using semantically correct HTML elements
		gets us most of the way there when it comes to accessibility.
	</p>

	<h2>1b: Semantic HTML &gt; Custom Roles and Attributes</h2>

	<p>
		There are some cases where we want to add additional styles or functionality that an element
		does not offer. Let’s take the select element as an example (Fun fact: <a
			href="https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Customizable_select"
			>customizable select</a
		> elements will be implemented in the near future). By default it has a very bare and simple style.
		Let's walk through building our own. We'll be adding ARIA roles and attributes to enhance the accessibility
		of our new custom select. ARIA stands for Accessible Rich Internet Applications.
	</p>
	<CodeBlock
		code="<div role='combobox' aria-expanded='false' aria-haspopup='listbox' tabindex='0' aria-labelledby='select-label'>
	    <span id='select-label'>Choose an option</span>
	  </div>"
		language="html"
	/>

	<h3>Explanation of the Attributes</h3>

	<ol>
		<li>
			<h4 class="font-mono font-bold text-green-800 dark:text-green-500">role='combobox'</h4>
			<p>
				Indicates that the element acts as an input element that controls another element such as a
				listbox. In other words, this element will have a popup with some options that we can select
				from.
			</p>
		</li>
		<li>
			<h4 class="font-mono font-bold text-green-800 dark:text-green-500">aria-expanded='false'</h4>
			<p>
				Specifies whether the element is expanded (true) or collapsed (false). Update this
				dynamically when the element opens or closes.
			</p>
		</li>
		<li>
			<h4 class="font-mono font-bold text-green-800 dark:text-green-500">
				aria-haspopup='listbox'
			</h4>
			<p>
				Indicates that the element will display a popup listbox (this will be the dropdown that
				contains our options).
			</p>
		</li>
		<li>
			<h4 class="font-mono font-bold text-green-800 dark:text-green-500">tabindex='0'</h4>
			<p>Makes the div focusable by keyboard.</p>
		</li>
		<li>
			<h4 class="font-mono font-bold text-green-800 dark:text-green-500">
				aria-labelledby='select-label'
			</h4>
			<p>
				This will make the element with the id "select-label" ("span" in this case) act as a label
				which will be read out to <a
					href="https://developer.mozilla.org/en-US/docs/Glossary/Screen_reader">screen readers</a
				>. The label text is "Choose an option" in this example.
			</p>
		</li>
	</ol>

	<p>
		That was exhausting… All of this just to emulate what was already there in the select element,
		and it's not even functional yet. Now you can see why it is best to avoid custom implementations
		like this as much as possible. Using semantic HTML isn't just good practice — it's one of the
		easiest ways to boost accessibility out of the box.
	</p>

	<Quiz>
		<RadioGroup
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
</section>
