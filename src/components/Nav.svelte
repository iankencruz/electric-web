<script>
	import { onMount } from "svelte";

	// Show mobile icon and display menu
	let showMobileMenu = false;

	// List of navigation items
	const navItems = [
		{ label: "About", href: "/about" },
		{ label: "Services", href: "/services" },
		{ label: "Contact", href: "/contact" },
	];

	// Mobile menu click event handler
	const handleMobileIconClick = () => (showMobileMenu = !showMobileMenu);

	// Media match query handler
	const mediaQueryHandler = (e) => {
		// Reset mobile state
		if (!e.matches) {
			showMobileMenu = false;
		}
	};

	// Attach media query listener on mount hook
	onMount(() => {
		const mediaListener = window.matchMedia("(max-width: 767px)");

		mediaListener.addListener(mediaQueryHandler);
	});
</script>

<nav>
	<a href="/" class="nav-logo">
        <img
            src="/images/icons/Logo.webp"
            alt="image alt"
            width="230"
            height="90"
        />
    </a>
	<div class="inner">
        
		<div
			on:click={handleMobileIconClick}
			class={`mobile-icon${showMobileMenu ? " active" : ""}`}
		>
			<div class="middle-line" />
		</div>
		<ul class={`navbar-list${showMobileMenu ? " mobile" : ""}`}>
			{#each navItems as item}
				<li>
					<a href={item.href}>{item.label}</a>
				</li>
			{/each}
		</ul>
	</div>
</nav>

<style>
	nav {
		background-color: #272727;
		font-family: "Helvetica Neue", "Helvetica", "Arial", sans-serif;
		height: 6rem;
		z-index: 999;
		width: 100%;
		display: flex;
		flex-wrap: wrap;
		/* justify-content: space-between; */
		align-items: center;
		margin: 0 auto;
		padding: 1rem 4rem;
	}

    .active {
        color: blue;
    }

	.inner {
		max-width: 980px;
		padding: 0 2rem;
		box-sizing: border-box;
		display: flex;
		align-items: center;
		height: 100%;
		z-index: 999;
	}

	.mobile-icon {
		width: 25px;
		height: 14px;
		position: relative;
		cursor: pointer;
		z-index: 999;
	}

	.mobile-icon:after,
	.mobile-icon:before,
	.middle-line {
		content: "";
		position: absolute;
		width: 100%;
		height: 2px;
		background-color: #fff;
		transition: all 0.4s;
		transform-origin: center;
		z-index: 999;
	}

	.mobile-icon:before,
	.middle-line {
		top: 0;
	}

	.mobile-icon:after,
	.middle-line {
		bottom: 0;
	}

	.mobile-icon:before {
		width: 66%;
	}

	.mobile-icon:after {
		width: 33%;
	}

	.middle-line {
		margin: auto;
	}

	.mobile-icon:hover:before,
	.mobile-icon:hover:after,
	.mobile-icon.active:before,
	.mobile-icon.active:after,
	.mobile-icon.active .middle-line {
		width: 100%;
	}

	.mobile-icon.active:before,
	.mobile-icon.active:after {
		top: 50%;
		transform: rotate(-45deg);
	}

	.mobile-icon.active .middle-line {
		transform: rotate(45deg);
	}

    .nav-logo {
        display: none;
    }
	.navbar-list {
		display: none;
		width: 100%;
		justify-content: space-between;
		margin: 0;
		padding: 0 40px;
		z-index: 999;
	}

	.navbar-list.mobile {
		background-color: #272727;
		position: fixed;
		display: block;
        padding-top: 4rem;
		height: calc(100% - 45px);
		bottom: 0;
		left: 0;
		z-index: 999;
	}

	.navbar-list li {
		list-style-type: none;
		position: relative;
		z-index: 999;
        margin: 0 4rem;
	}

	.navbar-list li:before {
		content: "";
		position: absolute;
		bottom: 0;
		left: 0;
		width: 100%;
		height: 1px;
		background-color: #424245;
		z-index: 999;
	}

	.navbar-list a {
		color: #fff;
		text-decoration: none;
		display: flex;
		height: 45px;
		align-items: center;
		padding: 0 10px;
		font-size: 13px;
	}

	@media screen and (min-width: 1000px) {
        nav {
            height: 12rem;
            padding: 0 16rem;
        }

        .inner {
            
            padding: 0 16rem;
        }

        .nav-logo {
            display: flex;
        }
		.mobile-icon {
			display: none;
		}

		.navbar-list {
			display: flex;
			padding: 0;
			z-index: 999;
		}

		.navbar-list a {
			display: inline-flex;
			z-index: 999;
		}
	}
</style>
