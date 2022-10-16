<script>
	import Menu from '../components/Menu.svelte';
	import './styles.css';
</script>

<div class="app">
	<Menu/>
	<main>
		<div class="position-main">
			<slot />
		</div>
	</main>
</div>

<style lang="scss">
	.app {
		display: flex;
		align-items: center;
		width: 40%;
		height: 315px;
		background: white;
		border-radius: 15px;
		overflow: hidden;
		border: 1px solid rgb(223, 223, 223);
		position: relative;

		@media screen and (max-width: 800px) {
			& {
				width: 95%;
				flex-direction: column;
				height: 400px;
			}
		}

		main {
			width: 100%;
			display: flex;
			justify-content: right;

			@media screen and (max-width: 800px) {
				& {
					height: 230px;
					justify-content: center;
					align-items: center;
				}
			}
			.position-main {
				width: 80%;
				display: flex;
				flex-direction: column;
				align-items: center;	
			}
		}
	}
</style>
