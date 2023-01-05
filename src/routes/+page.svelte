<script>
	import { TabGroup, Tab } from '@skeletonlabs/skeleton';
	import { writable } from 'svelte/store';
	import Overview from '$lib/components/Overview.svelte';
	import Transactions from '$lib/components/Transactions.svelte'
	import Coins from '$lib/components/Coins.svelte'
	const storeTab = writable('overview');
</script>

<div class="container mx-auto flex grid grid-cols-1">
<div>
<TabGroup selected={storeTab}>
	<Tab value="overview">Overview</Tab>
	<Tab value="coins-tokens">Coins/Tokens</Tab>
	<Tab value="pools">Pools</Tab>
	<Tab value="swaps">Swaps</Tab>
	<Tab value="games">Games</Tab>
	<Tab value="transactions">Transactions</Tab>
	<Tab value="settings">Settings</Tab>
</TabGroup>

<!-- Conditionally display content -->
{#if $storeTab === 'overview'}<Overview />{/if}
{#if $storeTab === 'coins-tokens'}<Coins />{/if}
{#if $storeTab === 'pools'}Pools{/if}
{#if $storeTab === 'swaps'}Swaps{/if}
{#if $storeTab === 'games'}Games{/if}
{#if $storeTab === 'transactions'}<Transactions />{/if}
{#if $storeTab === 'settings'}Settings{/if}
</div>
</div>
