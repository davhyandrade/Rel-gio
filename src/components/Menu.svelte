<script>
	import Clock from './ClockImage.svelte';
	import Timer from './TimerImage.svelte';
	import Stopwatch from './StopwatchImage.svelte';
</script>

<nav>
	<a href="/">
		<li>
			<Clock />
			<span>Relógio</span>
		</li>
	</a>
	<a href="/temporizador">
		<li>
			<Timer />
			<span>Temporizador</span>
		</li>
	</a>
	<a href="/cronometro">
		<li>
			<Stopwatch/>
			<span>Cronômetro</span>
		</li>
	</a>
</nav>

<style lang="scss">
	nav {
		position: fixed;
		width: 10%;
		height: 315px;
		background: rgba(245, 245, 245, 0.2);
		border-radius: 15px 0 0 15px;
		border-right: 1px solid rgb(223, 223, 223);

		@media screen and (max-width: 800px) {
			& {
				width: 100%;
				height: auto;
				display: flex;
				align-items: center;
				justify-content: space-evenly;
				position: initial;
				border-radius: initial;
				border-right: none;
				border-bottom: 1px solid rgb(223, 223, 223);
			}
		}

		a {
			text-decoration: none;
			list-style-type: none;
			color: gray;

			@media screen and (max-width: 800px) {
				& {
					width: 33%;
				}
			}

			li {
				height: 105px;
				display: flex;
				flex-direction: column;
				justify-content: center;
				align-items: center;
				overflow: hidden;

				span {
					font-size: 0.8rem;
					margin-top: 10px;
				}

				&:hover {
					transition: 1s;
					background: rgba(128, 128, 128, 0.1);
				}

				&:active {
					transition: 0.1s;
					background: rgba(128, 128, 128, 0.2);
				}
			}

			&:nth-child(1) li {
				border-radius: 15px 0 0 0;

				@media screen and (max-width: 800px) {
					& {
						border-radius: 5px 0 0 0;
					}
				}
			}

			&:nth-child(2) li {
				border-top: 1px solid rgb(223, 223, 223);
				border-bottom: 1px solid rgb(223, 223, 223);

				@media screen and (max-width: 800px) {
					& {
						border-right: 1px solid rgb(223, 223, 223);
						border-left: 1px solid rgb(223, 223, 223);
						border-top: none;
						border-bottom: none;
					}
				}
			}

			&:nth-child(3) li {
				border-radius: 0 0 0 15px;

				@media screen and (max-width: 800px) {
					& {
						border-radius: 0 5px 0 0;
					}
				}
			}
		}
	}
</style>
