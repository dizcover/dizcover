<script lang="ts">
	import { page } from '$app/state';
	import type { Icon as IconType } from 'lucide-svelte';

	type NavLink = {
		href: string;
		name: string;
		icon: typeof IconType;
	};

	type Props = {
		links: NavLink[];
	};

	const { links }: Props = $props();
	let activeRoute = $derived(page.url.pathname);
</script>

<div
	class="bottom-nav glass z-90 fixed bottom-0 grid w-full grid-cols-3 place-items-center gap-x-4 border-t border-white/10 bg-white/5 px-4 py-3 shadow-md"
>
	{#each links as link}
		<a
			href={link.href}
			class="flex flex-col items-center justify-center gap-1"
			data-sveltekit-reload
		>
			<link.icon class="size-4" />
			<span
				class="text-sm {activeRoute === link.href
					? 'font-semibold text-white'
					: 'text-muted-foreground'}">{link.name}</span
			>
		</a>
	{/each}
</div>

<style>
	.bottom-nav {
		box-shadow:
			0 -10px 15px -3px rgb(0 0 0 / 0.1),
			0 -4px 6px -4px rgb(0 0 0 / 0.1);
	}

	.glass {
		--blur: 12px;
		backdrop-filter: blur(var(--blur));
		-webkit-backdrop-filter: blur(var(--blur));
	}
</style>
