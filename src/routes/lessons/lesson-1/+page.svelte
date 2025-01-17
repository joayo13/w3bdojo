<script>
	import CodeBlock from '../../../components/CodeBlock.svelte';
	import Quiz from '../../../components/Quiz.svelte';
	import RadioGroup from '../../../components/RadioGroup.svelte';
	let isSubmitted = $state(false);
</script>

<h1 class="text-4xl">Keyboard Navigation and Semantic HTML</h1>
<p class="mt-8">
	As you know, there are plenty of folks in the world that cannot use both hands. Or maybe some
	can’t see the mouse on the screen due to visual impairment. Whatever the case, accommodating these
	users is an absolute necessity. So make sure to pay close attention here.
</p>
<h2 class="mt-8 text-2xl">1a: How does keyboard navigation work?</h2>
<p class="mt-2">
	As you likely already know there are many types of elements or “tags” within HTML. Most commonly
	seen are tags such as "a"(otherwise known as anchor tags, these are what links are on a page),
	"button", "select" etc. We will stick to these as they are simple examples, but take note that
	there are <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element"
		>many many more elements.</a
	> You can navigate through elements by using tab to move forwards, and shift + tab to move backwards.
</p>
<h2 class="mt-8 text-2xl">Here's a button:</h2>
<button
	onclick={() => alert('Yay!')}
	class="tab-button my-8 rounded-sm border border-inherit px-4 py-2 text-2xl">Tab to me!</button
>
<p class="mt-2">
	Notice how if you press your tab key to navigate forward or shift+tab to navigate backward, when
	navigating to the button it will have a line around it to indicate that it is in a “focus” state.
	This is meant to be very noticeable by default. Which is great since it’ll be easy to see for our
	visually impaired users.
</p>
<p class=" mt-8">
	Pressing the “Enter” or “Space” key will trigger the associated action on the element. Try doing
	that to the button.
</p>
<h2 class="mt-8 text-2xl">Select an option:</h2>
<p class="mt-8">
	Let’s interact with the "select" tag that has a few corresponding "option"’s. Use tab or shift +
	tab as before followed by Enter or Space, but once selected, you can navigate the options with the
	arrow keys. Navigate to “spongebob” and press Enter or Space key.
</p>
<select
	class="mt-8 text-neutral-900"
	onchange={(e) => (e.currentTarget.value === 'Spongebob' ? alert("I'm ready!") : null)}
>
	<option>Shrek</option>
	<option>Spiderman</option>
	<option>Spongebob</option>
</select>
<p class="mt-8">
	As you can see, these tags are already designed to handle keyboard navigation, which is very
	convenient for us as developers. This leads us into an important realization: using the correct
	HTML tags for the job will make a web application accessible by default.
</p>
<h2 class="mt-8 text-2xl">1b: Semantic HTML &gt; Custom Roles and Attributes</h2>
<p class="mt-2">
	By understanding what HTML tags to use for the job, we can already make accessible applications!
	But there are some cases where we need to add styles or functionality that the native tag does not
	offer. This is often seen with the select element. As you may have noticed, it looks rather bland.
	And it can only be stylized to a certain extent. If we wanted to, we could build one from scratch
	with a div. Then we would be able to control all of the styles 100%. However, just a div alone
	would now strip away the accessibility that came with the select element. How do we handle this?
	That is where we use roles and attributes.
</p>
<div class="mx-auto w-[95vw] md:w-[26rem] lg:w-[40rem]">
	<CodeBlock
		language="html"
		code="<div role='select' aria-expanded='false' aria-haspopup='listbox' tabindex='0' aria-labelledby='select-label'>
	    <span id='select-label'>Choose an option</span>
	  </div>"
	/>
</div>
<h3 class="mt-8 text-2xl">Explanation of the Attributes</h3>
<ol class="mt-2 flex flex-col gap-2">
	<li>
		<h4 class="text-green-600">role ="select"</h4>
		<p>Indicates that the element acts as a custom select dropdown.</p>
	</li>
	<li>
		<h4 class="text-green-600">aria-expanded="false"</h4>
		<p>
			Specifies whether the dropdown is expanded (true) or collapsed (false). Update this
			dynamically when the dropdown opens or closes.
		</p>
	</li>
	<li>
		<h4 class="text-green-600">aria-haspopup="listbox"</h4>
		<p>Indicates that the dropdown will display a listbox (typically the dropdown options).</p>
	</li>
	<li>
		<h4 class="text-green-600">tabindex="0"</h4>
		<p>
			Makes the div focusable via keyboard navigation. Users can navigate to it with the Tab key.
		</p>
	</li>
	<li>
		<h4 class="text-green-600">aria-labelledby="select-label"</h4>
		<p>
			Associates the div with a label ("span" in this case) so screen readers announce what the
			dropdown represents. The label text is "Choose an option" in this example.
		</p>
	</li>
</ol>
<p class="mt-8">
	That was exhausting.. All of this just to emulate what was already there in the select tag. And we
	haven’t even added support for using the up and down arrow keys on the options. Now you can see
	why it is best to avoid custom implementations like this as much as possible, to save yourself the
	headache. That’s not to say it isn’t useful to know these roles and attributes. In later lessons
	we'll dive deeper into good use cases for these roles and attributes.
</p>
<Quiz bind:isSubmitted
	><RadioGroup
		name="Who benefits from accessible web applications?"
		options={[
			'Visually Impaired Users',
			'Physically Disabled Users',
			'Cognitively Impaired Users',
			'All of the above'
		]}
		correctAnswer="All of the above"
		{isSubmitted}
	/></Quiz
>
