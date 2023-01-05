<script lang="ts">
	// Components
	import {Alert, Avatar, Paginator } from '@skeletonlabs/skeleton';
	// Utilities
	import { createDataTableStore, dataTableHandler, tableInteraction, tableA11y } from '@skeletonlabs/skeleton';
  const sourceData = [
	 { position: 1, lastprice: -0.25, amount: 1.0079, symbol: 'HIVE', usd: 245, chart: ""  },
	 { position: 2, lastprice: 0.25, amount: 4.0026, symbol: 'HBD', usd: 48, chart: ""  },
	 { position: 3, lastprice: -0.75, amount: 6.941, symbol: 'SWAP.BTC', usd: 2450, chart: ""  },
	 { position: 4, lastprice: 0.25, amount: 9.0122, symbol: 'INDEX', usd: 1500, chart: ""  },
	 { position: 5, lastprice: -0.25, amount: 10.811, symbol: 'SPS', usd: 45, chart: "" },
  ];
		// Store
	const dataTableStore = createDataTableStore(sourceData, {
		sort: '',
		search: '',
		pagination: { offset: 0, limit: 10, size: 0, amounts: [10, 20, 50, 100] }
	});
	dataTableStore.subscribe((model) => dataTableHandler(model));

	// Manual Selection
	// dataTableStore.select('position', [1]);
</script>

<section class="card">
	<!-- Search Input -->
	<div class="card-header">
		<input bind:value={$dataTableStore.search} type="search" placeholder="Search Coins/Tokens..." />
	</div>
	<!-- Table -->
	<div class="p-4">
		<div class="table-container">
			<!-- prettier-ignore -->
			<table class="table table-hover" role="grid" use:tableInteraction use:tableA11y>
				<thead on:click={(e) => { dataTableStore.sort(e) }} on:keypress>
					<tr>
						<!--
						<th><input type="checkbox" on:click={(e) => { dataTableStore.selectAll(e.currentTarget.checked) }} /></th>
						<th data-sort="id">TX ID</th>  -->
						<th>Chart</th>
						<th data-sort="symbol">Name</th>
						<th data-sort="lastprice">Last Price</th>
						<th data-sort="amount">Amount</th>
						<th data-sort="usd">USD</th>
						<th class="table-cell-fit">Place Order</th>
					</tr>
				</thead>
				<tbody>
					{#each $dataTableStore.filtered as row, rowIndex}
						<tr class:table-row-checked={row.dataTableChecked} aria-rowindex={rowIndex + 1}>
							<td class="table-cell-fit">
								{row.chart} 
							</td>
							<td role="gridcell" aria-colindex={3} tabindex="0" class="table-cell-fit">
								{row.symbol}
							</td>
							<td role="gridcell" aria-colindex={4} tabindex="0" class="md:!whitespace-normal capitalize table-cell-fit">
								{row.lastprice}
							</td>
							<td role="gridcell" aria-colindex={5} tabindex="0" class="md:!whitespace-normal table-cell-fit">
								{row.amount}
							</td>
							<td class="table-cell-fit">
								{row.usd} 
							</td>
							<td role="gridcell" aria-colindex={6} tabindex="0">
								<form>   
									<div class="relative">
											<div class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
											</div>
											<input type="number" id="order" class="block w-full" placeholder="0.000" required>
											<button type="submit" class="btn btn-filled-success btn-sm">Buy</button>
											<button type="submit" class="btn btn-filled-warning btn-sm">Sell</button>
									</div>
							</form>
							</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
	</div>
	<div class="card-footer">
		<Paginator bind:settings={$dataTableStore.pagination} />
	</div>
</section>