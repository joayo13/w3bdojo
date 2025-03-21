<script>
	import LessonLink from '../../../components/LessonLink.svelte';
	import Quiz from '../../../components/Quiz.svelte';
	import RadioGroup from '../../../components/RadioGroup.svelte';
	let isSubmitted = $state(false);
</script>

<h1 class="text-4xl">Testing Accessibility</h1>
<p class="mt-8">
	This section of the tutorial assumes you are using the Chrome or Firefox Browser. (If you aren’t
	you should, as this is the standard for web development)
</p>
<p class="mt-2">
	You might have heard the term “Lighthouse scores” in web development circles. What it means is a
	score that gets assigned to a webpage measuring four categories. Performance, Accessibility, Best
	Practices and SEO. Obviously we are only concerned with Accessibility. But keep in mind that you
	should strive to have high lighthouse scores in general.
</p>
<h2 class="mt-8 text-2xl">How to get Lighthouse scores in Chrome</h2>
<ol class="mt-2 flex flex-col gap-2">
	<li>
		<h4>1. Open Chrome and navigate to the website you want to test.</h4>
	</li>
	<li>
		<h4>
			2. Press <strong>F12</strong> to open <strong>DevTools</strong>, or right-click anywhere on
			the page and select Inspect.
		</h4>
	</li>
	<li>
		<h4>3. Go to the <strong>Lighthouse</strong> tab in DevTools.</h4>
	</li>
	<li>
		<h4>
			4. Choose the type of report you want (Mobile/Desktop, Performance, Accessibility, SEO, etc.).
		</h4>
	</li>
	<li>
		<h4>5. Click <strong>Generate Report</strong>.</h4>
	</li>
	<li>
		<h4>
			6. After a few moments, the Lighthouse report will appear with scores and suggestions for
			improvement.
		</h4>
	</li>
</ol>
<div class="mt-8 h-px w-full bg-neutral-900 dark:bg-neutral-200"></div>
<h2 class="mt-8 text-2xl">How to get Lighthouse scores in Firefox</h2>
<ol class="mt-2 flex flex-col gap-2">
	<li>
		<h4>1. Install the Lighthouse extension from the Chrome Web Store (works in Firefox).</h4>
	</li>
	<li>
		<h4>2. After installation, click the Lighthouse icon in the toolbar.</h4>
	</li>
	<li>
		<h4>
			3. Select the type of report you want (Mobile/Desktop, Performance, Accessibility, etc.).
		</h4>
	</li>
	<li>
		<h4>4. Click <strong>Generate Report</strong>.</h4>
	</li>
	<li>
		<h4>5. The report will show up in a new tab with scores and improvement tips.</h4>
	</li>
</ol>

<p class="mt-8">
	Great, now that will be a tool you can take with you and make great use of in the future. Another
	great tool to have is a screen reader, so you can personally test how a screen reader will behave
	on your website. The two screen readers we’ll recommend are NVDA and JAWS, both of which are free
	and open source! We won’t cover installation steps and how to use them, as you can find that
	information for your screen reader on their respective websites.
</p>
<Quiz
	><RadioGroup
		name="What is are the four categories measured by Lighthouse scores?"
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
		name="Why did you complete this tutorial?"
		options={['Because I am awesome.']}
		correctAnswer="Because I am awesome."
	/>
</Quiz>
<LessonLink href="/lessons/lesson-5" text="Start Lesson 5" />
