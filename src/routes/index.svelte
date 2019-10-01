<script>
	import Menu from '../components/Menu.svelte';

	const dataFile = 'data.json';

	let promise = getData();
	// let menuData;

    async function getData() {
		const res = await fetch(dataFile);
		const data = await res.json();

		if (res.ok) {
			return data;
		} else {
			throw new Error(data);
		}
	}
</script>

<style>
</style>

<header class="masthead">
	<div class="masthead__wrap">
		<img class="masthead__logo" src="chill-out-logo.svg" alt="Chill Out Cafe Logo" />
		<div class="masthead__subheading">Dine-In &#8226; Carry-Out &#8226; Delivery</div>
		<a class="masthead__phone" href="&#116;&#101;&#108;:(&#053;&#048;&#052;)&#032;&#056;&#055;&#050;&#045;&#057;&#054;&#050;&#056;">(&#053;&#048;&#052;)&#032;&#056;&#055;&#050;&#045;&#057;&#054;&#050;&#056;</a>
		<div class="masthead__address">729 Burdette St., New Orleans, LA 70118
		</div>
	</div>
</header>

<main class="main">
	<h1 class="page-title visibly-hidden">Menu</h1>
	<div class="main__decoration main__decoration--left" role="presentation">
		<div class="main__decoration__inner"></div>
	</div>
	<div class="main__decoration main__decoration--right" role="presentation">
		<div class="main__decoration__inner"></div>
	</div>

	{#await promise}
		<p>...loading</p>
	{:then menus}
		{#each menus as menu}
			<Menu {menu}/>
		{:else}
			<p class="error">No menus found!</p>
		{/each}
	{:catch error}
		<p style="color: red">{error.message}</p>
	{/await}
</main>