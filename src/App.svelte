<script>
	import About from "./Components/About.svelte";
	import Education from "./Components/Education.svelte";
	import Nav from "./Components/Nav.svelte";
	import Banner from "./Components/Banner.svelte";
	import Resume from "./Components/Resume.svelte";
	import * as content from "./Constants";
	import Projects from "./Components/Projects.svelte";
	import Contact from "./Components/Contact.svelte";
import Footer from "./Components/Footer.svelte";

	let height;
</script>

<svelte:window bind:innerHeight={height}></svelte:window>

<header>
	<Nav content={content.NavItems}></Nav>	
	<Banner height={height} content={content.MainBanner} bind:scrollItem={content.NavItems[0]}></Banner>
</header>

<main>
	<About content={content.About}></About>
	<Education content={content.Education}></Education>
	<Resume content={content.Resume}></Resume>
	<Projects content={content.Projects}></Projects>
</main>

<footer>
	<Contact content={content.Contact}></Contact>
	<Footer content={content.Footer}></Footer>
</footer>

<style>
	footer {
		padding-top: 50px;
	}
</style>