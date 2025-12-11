<script>
	import HeroImage from '../../components/atoms/HeroImage.svelte';
	import Button from '../atoms/Button.svelte';
	import Socials from '../molecules/Socials.svelte';

	function handleClick() {
		const el = document.querySelector('#aw');
		if (!el) return;
		el.scrollIntoView(true);
	}
</script>

<section id="home" class="wrapper page-eyest">
	<div>
		<h1>Leafinite</h1>

		<h2 class="leafra-desc">
			<strong>LEAFRA</strong> comes from the root word <em>leaf</em>, the universal symbol of
			growth and regeneration.
			<br /><br />
			The suffix <strong>-ra</strong> adds a sense of energy, core essence, and primordial power.
			<br /><br />
			LEAFRA represents:
			<ul>
				<li>Leaves capturing light → <strong>Data & Knowledge</strong></li>
				<li>Growth & evolution → <strong>AI models that continuously learn</strong></li>
				<li>Ecosystem → <strong>Community & blockchain networks</strong></li>
			</ul>

			<br />
			<strong>LEAFRA is the first digital leaf growing from the tree of future intelligence.</strong>
		</h2>

		<div class="socials">
			<Socials />
		</div>

		<Button side on:click={handleClick} on:keypress={handleClick}>Explore ↓</Button>
	</div>

	<HeroImage />
</section>

<style lang="scss">
	@import '../../styles/mixins.scss';

	/* ————————————————————————————————
	   FORCE TEXT WHITE IN THIS HERO
	   ———————————————————————————————— */
	.page-eyest,
	.page-eyest * {
		color: #ffffff !important;
	}

	.page-eyest svg,
	.page-eyest svg * {
		fill: #ffffff !important;
		stroke: #ffffff !important;
		color: #ffffff !important;
	}

	/* ====== BUTTON EXPLORE ====== */
	:global(.page-eyest button) {
		color: #ffffff !important;
		border: 1px solid #ffffff !important;
		background-color: transparent !important;
	}

	:global(.page-eyest .side) {
		background-color: #ffffff !important;
		color: #000000 !important;
	}

	:global(.page-eyest button:hover) {
		filter: brightness(90%);
		background-color: rgba(255, 255, 255, 0.06) !important;
		color: #ffffff !important;
	}

	:global(.page-eyest button),
	:global(.page-eyest button:focus),
	:global(.page-eyest button:focus-visible),
	:global(.page-eyest button:focus-within) {
		outline: none;
		box-shadow: none;
	}

	/* ————————————————————————————————
	   LEAFRA DESCRIPTION (H2)
	   ———————————————————————————————— */
	.leafra-desc {
		font-size: 1.05rem !important;
		line-height: 1.55rem;
		max-width: 600px;
		font-weight: 400;
		margin-top: 1rem;
	}

	.leafra-desc ul {
		margin: 0.8rem 0 0 1.2rem;
		padding: 0;
		list-style: disc;
	}

	.leafra-desc li {
		margin-bottom: 0.3rem;
		font-size: 1rem;
	}

	.leafra-desc strong {
		font-weight: 600;
	}

	@media screen and (max-width: 500px) {
		.leafra-desc {
			font-size: 0.95rem !important;
			line-height: 1.45rem;
		}
	}

	/* ———————————————————————————————— */

	section {
		scroll-margin-top: 20rem;
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 5.75rem;
		margin-top: 7rem;

		@media screen and (max-width: 868px) {
			margin-top: 4rem;
		}

		@media screen and (max-width: 768px) {
			margin-bottom: 2.75rem;
		}

		@media screen and (max-width: 500px) {
			display: block;
		}
	}

	.socials {
		margin-top: 1rem;
		margin-bottom: 1.7rem;
	}

	h4 {
		margin-top: 1rem;
	}

	h1::before {
		@include outlineText(
			$content: '',
			$translateX: -95%,
			$letterSpacing: -0.1em
		);
	}

	@media screen and (max-width: 1240px) {
		h1 {
			min-height: 0vw;
			font-size: clamp(4rem, 10vw, 6.25rem);
		}

		h4 {
			min-height: 0vw;
			font-size: clamp(1.4rem, 2.4vw, 1.5rem);
		}
	}

	@media screen and (max-width: 400px) {
		h4 br {
			content: '&#160;';
		}
	}
</style>
