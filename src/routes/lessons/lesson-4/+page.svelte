<script>
	import Quiz from '../../../components/Quiz.svelte';
	import RadioGroup from '../../../components/RadioGroup.svelte';
</script>

<svelte:head>
	<title>Lesson 4: Testing Web Accessibility | W3b Dojo</title>
	<meta
		name="description"
		content="Learn how to test your website for accessibility using tools like Lighthouse and screen readers. Understand how to identify and fix accessibility issues."
	/>
	<meta
		name="keywords"
		content="accessibility testing, Lighthouse, screen readers, web accessibility, a11y"
	/>
</svelte:head>

<h1>Testing Accessibility</h1>

<p>
	This section of the tutorial assumes you are using the Chrome or Firefox Browser. (If you aren't
	you should, as this is the standard for web development)
</p>
<p>
	You might have heard the term "Lighthouse scores" in web development circles. What it means is a
	score that gets assigned to a webpage measuring four categories. Performance, Accessibility, Best
	Practices and SEO. Obviously we are only concerned with Accessibility. But keep in mind that you
	should strive to have high lighthouse scores in general.
</p>

<h2>How to get Lighthouse scores in Chrome</h2>
<ol>
	<li>
		<h4>Open Chrome and navigate to the website you want to test.</h4>
	</li>
	<li>
		<h4>
			Press <strong>F12</strong> to open <strong>DevTools</strong>, or right-click anywhere on the
			page and select Inspect.
		</h4>
	</li>
	<li>
		<h4>Go to the <strong>Lighthouse</strong> tab in DevTools.</h4>
	</li>
	<li>
		<h4>
			Choose the type of report you want (Mobile/Desktop, Performance, Accessibility, SEO, etc.).
		</h4>
	</li>
	<li>
		<h4>Click <strong>Generate Report</strong>.</h4>
	</li>
	<li>
		<h4>
			After a few moments, the Lighthouse report will appear with scores and suggestions for
			improvement.
		</h4>
	</li>
</ol>

<div class="mt-8 h-px w-full bg-neutral-900 dark:bg-neutral-200"></div>

<h2>How to get Lighthouse scores in Firefox</h2>
<ol>
	<li>
		<h4>Install the Lighthouse extension from the Chrome Web Store (works in Firefox).</h4>
	</li>
	<li>
		<h4>After installation, click the Lighthouse icon in the toolbar.</h4>
	</li>
	<li>
		<h4>Select the type of report you want (Mobile/Desktop, Performance, Accessibility, etc.).</h4>
	</li>
	<li>
		<h4>Click <strong>Generate Report</strong>.</h4>
	</li>
	<li>
		<h4>The report will show up in a new tab with scores and improvement tips.</h4>
	</li>
</ol>

<p>
	Great, now that will be a tool you can take with you and make great use of in the future. Another
	great tool to have is a screen reader, so you can personally test how a screen reader will behave
	on your website. The two screen readers we'll recommend are NVDA and JAWS, both of which are free
	and open source! We won't cover installation steps and how to use them, as you can find that
	information for your screen reader on their respective websites.
</p>

<Quiz>
	<RadioGroup
		name="What are the four categories measured by Lighthouse scores?"
		options={[
			'Responsiveness, Accessibility, SEO and Design',
			'Performance, Style, Accessibility and SEO',
			'Accessibility, Performace, SEO, Responsiveness',
			'Performance, Accessibility, Best Practices and SEO'
		]}
		correctAnswer="Performance, Accessibility, Best Practices and SEO"
	/>
	<RadioGroup
		name="What are the recommended free screen readers?"
		options={['NVIDIA and WAWS', 'NVDA and JAWS', 'WNBA and NBA', 'All of the above']}
		correctAnswer="NVDA and JAWS"
	/>
	<RadioGroup
		name="Why am I learning how to make the web a more inclusive place?"
		options={['Because I am awesome.']}
		correctAnswer="Because I am awesome."
	/>
</Quiz>
