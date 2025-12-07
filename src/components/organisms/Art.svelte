<script>
	import ArtGrid from '../../components/molecules/ArtGrid.svelte';
	import Tooltip from '../atoms/Tooltip.svelte';
</script>

<section>
	<div class="wrapper" id="aw">
		<Tooltip tip="Click on an artwork">
			<h2><span>art</span></h2>
		</Tooltip>
	</div>
	<ArtGrid />
</section>

<style lang="scss">

	/* ———————————————————————
	   FIX: “art” TITLE → PUTIH
	   ——————————————————————— */
	span {
		color: #ffffff !important;
	}

	h2 {
		display: inline-block;
		margin-bottom: 1rem;
	}

	div {
	display: flex;
	justify-content: center; /* CENTER DEFAULT (DESKTOP) */
	margin-top: 0;

	@media (max-width: 868px) {
		justify-content: flex-start; /* MOBILE pindah ke kiri */
		margin-bottom: 0.3rem;
	}
}
</style>
