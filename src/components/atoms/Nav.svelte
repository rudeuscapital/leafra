<script lang="ts">
	import { goto } from '$app/navigation';
	import { page } from '$app/stores';

	export let href = '#';
	export let section = 'home';
	export let isSelected: boolean;

	$: currentPage = $page.url.pathname;

	async function handleClick() {
		if (href.startsWith('/')) {
			await goto(href);
			return;
		}

		if (currentPage === '/') {
			const el = document.querySelector(href);
			if (el) el.scrollIntoView({ behavior: 'smooth' });
		} else {
			window.location.href = `/${href}`;
		}
	}
</script>

<li class:selected={isSelected}>
	<button on:click={handleClick}>
		<div class="icon-container">
			<slot />
		</div>
		<h5>{section}</h5>
	</button>
</li>

<style lang="scss">
li {
	list-style: none;
}

button {
	background: transparent;
	border: none;
	display: flex;
	align-items: center;
	gap: 0.6rem;
	padding: 10px 18px;
	border-radius: 50px;
	cursor: pointer;
	transition: 0.3s ease;
}

.icon-container {
	display: none;
}

h5 {
	font-weight: 400;
	opacity: 0.9;
}

.selected h5 {
	font-weight: 600;
	opacity: 1;
}

/* MOBILE */
@media (max-width: 868px) {
	button {
		flex-direction: column;
		align-items: center;
		gap: 0.3rem;
		padding: 6px 10px;
		font-size: 0.75rem;
	}

	h5 {
		font-size: 0.7rem;
	}

	.icon-container {
		display: block;
		padding: 6px 14px;
		border-radius: 50%;
	}

	button:hover .icon-container,
	.selected .icon-container {
		background: rgba(0,0,0,0.1);
	}
}
</style>
