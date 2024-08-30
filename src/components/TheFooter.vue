<template>

	<footer class="footer">
		<div class="footer__inner">
			<p class="footer__copyright">
				SPACEX &copy; 2024
			</p>

			<div class="footer__links">
				<a href="#" class="footer__link">PRIVACY POLICY</a>
				<a href="#" class="footer__link">SUPPLIERS</a>
			</div>
		</div>
	</footer>
</template>

<style lang="scss" scoped>

.footer {
	background: $secondary-color;

	&__inner {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: $padding-md;
		gap: $padding-md;

		@media all and (min-width: 600px) {
			flex-direction: row;
			gap: $padding-lg;
			padding: $padding-lg;
		}
	}

	&__copyright {
		color: $primary-color;
		font-size: 0.75rem;
	}

	&__links {
		display: flex;
		gap: $padding-sm;

		@media all and (min-width: 600px) {
			gap: $padding-lg;
		}
	}

	&__link {
		color: $primary-color;
		font-size: 0.75rem;
		text-decoration: none;
		font-weight: 700;
		transition: opacity 0.4s;

		&:hover {
			opacity: 0.5;
			transition: opacity 0.4s;
		}
	}

}

</style>