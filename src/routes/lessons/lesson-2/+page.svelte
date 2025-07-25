<script>
	import CodeBlock from '../../../components/CodeBlock.svelte';
	import Quiz from '../../../components/Quiz.svelte';
	import RadioGroup from '../../../components/RadioGroup.svelte';
	const skipLinkCode = `
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Skip to Main Content Example</title>
    <style>
        /* Style to visually hide the link initially */
        .skip-link {
            position: fixed;
            top: -40px;
            left: 0;
            background: #007BFF;
            color: white;
            padding: 8px 16px;
            text-decoration: none;
            z-index: 100;
        }
        /* Make the link visible when focused */
        .skip-link:focus {
            top: 0;
        }
    </style>
</head>
<body>
    <!-- Skip link -->
    <a href="#main-content" class="skip-link">Skip to Main Content</a>
    <!-- Navigation -->
    <nav>
        <ul>
            <li><a href="#">Home</a></li>
            <li><a href="#">About</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
    </nav>
    <!-- Main content -->
    <main id="main-content" tabindex="-1">
        <h1>Welcome to the Main Content</h1>
        <p>This is the main section of the webpage.</p>
    </main>
</body>
</html>
  `;
	const tabIndexCode = `
<div class="game-over">
    <h1>Game Over</h1>
    <div class="links">
        <a href="#scores" tabindex="2">Scores</a> |
        <a href="#stats" tabindex="3">Stats</a> |
        <a href="#items" tabindex="4">Items Collected</a> |
        <a href="#enemies" tabindex="5">Enemies Destroyed</a>
    </div>
    <a href="#play-again" id="play-again-btn" class="play-again-btn" tabindex="1">Play Again</a>
</div>
  `;
</script>

<svelte:head>
	<title>Lesson 2: Skip Links and Focus Management | W3b Dojo</title>
	<meta
		name="description"
		content="Learn about skip links and focus management techniques for web accessibility. Understand how to help keyboard users navigate your website more efficiently."
	/>
	<meta
		name="keywords"
		content="skip links, focus management, web accessibility, a11y, keyboard navigation"
	/>
</svelte:head>

<section>
	<h1>Skip Links and Tab Index</h1>

	<p>
		Imagine you can only use the keyboard, and you visit a news website, looking to see the main
		front page content. At the top of the page, there are links to home, about, articles, authors
		etc… This means you would have to tab through every link before being able to read what you
		wanted to in the first place. The solution to this problem is what's known as a skip link. Try
		going to a content related website like reddit or wikipedia, or even right here on W3b Dojo and
		notice that when you first use the tab key, you will get a button that shows up saying something
		along the lines of "skip to main content" — that's a skip link!
	</p>

	<h2>So how can we implement our own? Let's look at some basic HTML:</h2>

	<CodeBlock language="html" code={skipLinkCode} />

	<p>
		There's a lot to take in here, but pay attention to the <code>:focus</code> selector in our
		styles, and our <code>id</code> attribute on our <code>main</code> tag. The <code>:focus</code>
		selector is great for the skip link, because we can have it only visible in the case of someone tabbing/focusing
		into it. The reason that we use <code>tabindex="-1"</code> is because without it, when we follow
		the link, our link would still be focused. By doing this, we are programmatically focusing the
		main content — or more simply, forcing the focus onto
		<code>main</code>. This is one way that we can use the <code>tabindex</code> attribute to enhance
		our website's accessibility.
	</p>

	<p>
		Another less common scenario is when we want to override the natural flow of the tabbing through
		our website. Maybe we made a game, and at the gameover screen there are a bunch of links to
		things like scores, stats, items collected, enemies destroyed etc. but we want a keyboard user
		to immediately skip these and first tab onto the play again button.
	</p>

	<CodeBlock language="html" code={tabIndexCode} />

	<p>
		Here is how we could achieve something like this. Note that this is generally not recommended,
		as it could easily lead to confusion if overdone. But at least this example gives you an idea of
		how it works. In our next lesson, we'll take a look at how ARIA works, and when we should use
		it.
	</p>

	<Quiz>
		<RadioGroup
			name="Why should we use a skip-link?"
			options={[
				'Keyboard users can skip the main content',
				'Keyboard users can get to the main content faster',
				'Keyboard users can skip to the next link',
				'Keyboard users can skip to the bottom of the page'
			]}
			correctAnswer="Keyboard users can get to the main content faster"
		/>
		<RadioGroup
			name="When should you set tabindex?"
			options={[
				'Only when necessary',
				'When you need to create a skip-link',
				'When you need to override the default tab-order',
				'All of the above'
			]}
			correctAnswer="All of the above"
		/>
	</Quiz>
</section>
