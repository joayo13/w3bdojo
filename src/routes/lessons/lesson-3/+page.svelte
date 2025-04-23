<script>
	import CodeBlock from '../../../components/CodeBlock.svelte';
	import LessonLink from '../../../components/LessonLink.svelte';
	import Quiz from '../../../components/Quiz.svelte';
	import RadioGroup from '../../../components/RadioGroup.svelte';
	let isSubmitted = $state(false);
	const jsCode = `document.getElementById('shopLink').addEventListener('mouseover', function() {
      const dropdown = document.getElementById('dropdown');
      const expanded = this.getAttribute('aria-expanded') === 'true';
      dropdown.style.display = expanded ? 'none' : 'block';
      this.setAttribute('aria-expanded', expanded ? 'false' : 'true');
  });`;

	// The full HTML snippet
	const codeSnippet = `<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>ARIA Example</title>
</head>
<body>

    <a href="#" id="shopLink" aria-controls="dropdown" aria-expanded="false">Shop</a>
    <ul id="dropdown" style="display:none;">
        <li>T-shirts</li>
        <li>Pants</li>
        <li>Socks</li>
    </ul>

    <script>
        ${jsCode}
    <\/script>
</body>
</html>`;
</script>

<svelte:head>
	<title>Lesson 3: ARIA Attributes and Roles | W3b Dojo</title>
	<meta
		name="description"
		content="Learn about ARIA attributes and roles for web accessibility. Understand how to enhance the accessibility of your web applications with ARIA."
	/>
	<meta
		name="keywords"
		content="ARIA, web accessibility, a11y, roles, attributes, screen readers"
	/>
</svelte:head>

<h1 class="text-4xl font-semibold">ARIA 101</h1>
<p class="mt-8">
	ARIA can be used to add extra accessibility information to tags. It's how we would add
	accessibility to a plain div that is trying to emulate a select or other tag. So in general, you
	will mostly avoid ARIA unless you are trying to create custom versions of native elements. But,
	there are instances that ARIA can be used to enhance native HTML. Here, we'll cover 3 Key ARIA
	Attributes: aria-controls, aria-expanded, and aria-label
</p>
<h2 class="mt-8 text-2xl">3a: Aria controls and aria-expanded</h2>
<p class="mt-2">
	Imagine that you are building a navigation for a shopping website, and when you hover over the
	shop link, you want a dropdown of some options to appear: t-shirts, pants, socks etc. Once you
	have built the dropdown menu, you need a way to communicate this relationship of link to dropdown
	to a screen reader. With aria-controls, we are saying to the screen reader "This link controls
	this element with this id" the element in this example being the dropdown menu. Aria-expanded says
	"if i am true then the dropdown is showing, if i am false then it is not". Here is a code snippet
	that demonstrates this.
</p>
<CodeBlock language="html" code={codeSnippet} />
<h2 class="text-2xl">Aria Label</h2>
<p class="mt-2">
	If you've ever had a window popup when on a website, you'll have likely seen the common convention
	of a X button in the top corner of the popup, that will close the popup upon being clicked. For a
	screen reader, it wouldn't be able to decipher what the image of an x would be. It would therefore
	have no meaning and just be some button. It would be useful if we could have a message for screen
	readers that will say that this button closes the window. This is where we'd use aria-label. This
	is nice and simple. Just add the aria-label attribute to your element and fill it in with text
	such as "Close Popup".
</p>
<Quiz
	><RadioGroup
		name="When should you add an aria-label to something?"
		options={[
			'When it is aria',
			'When it needs to swap places with another element',
			'When a screen reader needs additional info',
			'All of the above'
		]}
		correctAnswer="When it needs to swap places with another element"
	/>
	<RadioGroup
		name="What does aria-controls do?"
		options={[
			'Controls my arias',
			'Indicates which element id this element is controlling',
			'Indicates which element class this element is controlling',
			'None of the above'
		]}
		correctAnswer="Indicates which element id this element is controlling"
	/>
	<RadioGroup
		name="What does aria-expanded do?"
		options={[
			'Controls my arias',
			'Indicates whether an element is open or expanded',
			'Expands my arias',
			'All of the above'
		]}
		correctAnswer="Indicates whether an element is open or expanded"
	/>
</Quiz>
<LessonLink href="/lessons/lesson-4" text="Start Lesson 4" />
