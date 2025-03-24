<script lang="ts">
	import { theme } from '$lib/state';

	function toggle() {
		theme.current = theme.current === 'light' ? 'dark' : 'light';
	}

	$effect(() => {
		document.documentElement.classList.remove('light', 'dark');
		document.documentElement.classList.add(theme.current);
	});
</script>

<svelte:head>
	<script>
		{
			const theme = localStorage.getItem('theme');

			document.documentElement.classList.add(
				!theme || theme === 'system'
					? window.matchMedia('(prefers-color-scheme: dark)').matches
						? 'dark'
						: 'light'
					: theme
			);
		}
	</script>
</svelte:head>

<button
	onclick={toggle}
	type="button"
	aria-pressed={theme.current === 'dark'}
	aria-label="Toggle dark mode"
></button>
