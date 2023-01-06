<script lang="ts">
	// Components
	import {Alert, Avatar, Paginator } from '@skeletonlabs/skeleton';
	// Utilities
	import { createDataTableStore, dataTableHandler, tableInteraction, tableA11y } from '@skeletonlabs/skeleton';
  const sourceData = [
	 { position: 1, delta: -0.25, weight: 1.0079, symbol: 'HIVE' },
	 { position: 2, delta: 0.25, weight: 4.0026, symbol: 'HBD' },
	 { position: 3, delta: -0.75, weight: 6.941, symbol: 'SWAP.BTC' },
	 { position: 4, delta: 0.25, weight: 9.0122, symbol: 'INDEX' },
	 { position: 5, delta: -0.25, weight: 10.811, symbol: 'SPS' },
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

<section class="card gap-4 m-4">
	<!-- Search Input -->
	<div class="card-header">
		<input bind:value={$dataTableStore.search} type="search" placeholder="Search Transactions..." />
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
						<th>From</th>
						<th>To</th>
						<th data-sort="title">Type</th>
						<th data-sort="body">Amount</th>
						<th class="table-cell-fit"></th>
					</tr>
				</thead>
				<tbody>
					{#each $dataTableStore.filtered as row, rowIndex}
						<tr class:table-row-checked={row.dataTableChecked} aria-rowindex={rowIndex + 1}>
							<!--
							<td role="gridcell" aria-colindex={1} tabindex="0">
								<input type="checkbox" bind:checked={row.dataTableChecked} />
							</td>
											<td role="gridcell" aria-colindex={2} tabindex="0">
								<em class="opacity-50">{row.position}</em>
							</td>  -->
							<td role="gridcell" aria-colindex={3} tabindex="0">
								<Avatar src={`https://i.pravatar.cc/?img=${row.position +1}`} width="w-12" /> 
																		</td>
																		<td>
								<Avatar src={`https://i.pravatar.cc/?img=${1}`} width="w-12" /> 
							</td>
							<td role="gridcell" aria-colindex={4} tabindex="0" class="md:!whitespace-normal capitalize">
								{row.symbol}
							</td>
							<td role="gridcell" aria-colindex={5} tabindex="0" class="md:!whitespace-normal">
								{row.weight}
							</td>
							<td role="gridcell" aria-colindex={6} tabindex="0" class="table-cell-fit">
								<button class="btn btn-ghost-surface btn-sm" on:click={()=>{console.log(row,rowIndex)}}>View TX</button>
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