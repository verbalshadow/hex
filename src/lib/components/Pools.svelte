<script lang="ts">
	import { Paginator } from '@skeletonlabs/skeleton';
	import {
		createDataTableStore,
		dataTableHandler,
		tableInteraction,
		tableA11y
	} from '@skeletonlabs/skeleton';

	const sourceData = [
		{
			position: 1,
			lastprice: -0.25,
			amount: [
				{ name: 'Swap.HIVE', total: 2500 },
				{ name: 'HBD', total: 7500 }
			],
			symbol: 'Swap.HIVE:HBD',
			usd: 245,
			chart: ''
		},
		{
			position: 2,
			lastprice: 0.25,
			amount: [
				{ name: 'Swap.HIVE', total: 2500 },
				{ name: 'DEC', total: 7500 }
			],
			symbol: 'Swap.HIVE:DEC',
			usd: 48,
			chart: ''
		},
		{
			position: 3,
			lastprice: -0.75,
			amount: [
				{ name: 'Swap.HIVE', total: 2500 },
				{ name: 'SPS', total: 7500 }
			],
			symbol: 'Swap.HIVE:SPS',
			usd: 2450,
			chart: ''
		},
		{
			position: 4,
			lastprice: 0.25,
			amount: [
				{ name: 'DEC', total: 2500 },
				{ name: 'SPS', total: 7500 }
			],
			symbol: 'DEC:SPS',
			usd: 1500,
			chart: ''
		},
		{
			position: 5,
			lastprice: -0.25,
			amount: [
				{ name: 'VOUCHER', total: 2500 },
				{ name: 'SPS', total: 7500 }
			],
			symbol: 'VOUCHER:SPS',
			usd: 45,
			chart: ''
		}
	];
	// Store
	const dataTableStore = createDataTableStore(sourceData, {
		sort: '',
		search: '',
		pagination: { offset: 0, limit: 10, size: 0, amounts: [10, 20, 50, 100] }
	});
	dataTableStore.subscribe((model) => dataTableHandler(model));

	let poolList = ['Swap.HIVE:HBD', 'Swap.HIVE:DEC', 'Swap.HIVE:SPS'];
</script>

<section class="card gap-4 m-4">
	<!-- Search Input -->
	<div class="card-header">
		<input bind:value={$dataTableStore.search} type="search" placeholder="Search Pools..." />
	</div>
	<!-- Table -->
	<div class="p-4">
		<div class="table-container">
			<table class="table table-hover" role="grid" use:tableInteraction use:tableA11y>
				<thead
					on:click={(e) => {
						dataTableStore.sort(e);
					}}
					on:keypress
				>
					<tr>
						<th data-sort="symbol">Pool</th>
						<th>Amounts</th>
						<th data-sort="usd">USD</th>
						<th class="table-cell-fit">Add Liquidity</th>
					</tr>
				</thead>
				<tbody>
					{#each $dataTableStore.filtered as row, rowIndex}
						<tr class:table-row-checked={row.dataTableChecked} aria-rowindex={rowIndex + 1}>
							<td role="gridcell" aria-colindex={0} tabindex="0">
								<p class="text-lg">{row.symbol}</p>
							</td>
							<td role="gridcell" aria-colindex={1} tabindex="0" class="md:!whitespace-normal flex">
								<div class="flex-grid-col">
									<p class="text-lg"><b>{row.amount[0].name}: </b>{row.amount[0].total}</p>
									<p class="text-lg"><b>{row.amount[1].name}: </b>{row.amount[1].total}</p>
								</div>
							</td>
							<td>
								<p class="text-xl">
									{row.usd}
								</p>
							</td>
							<td role="gridcell" aria-colindex={2} tabindex="0" class="table-cell-fit">
								<form class="flex flex mt-6 space-x-3 w-400">
									<input
										type="number"
										id="order"
										class="block w-full"
										placeholder="0.000"
										required
									/>
									<select name="poolcoin" id="poolcoin">
										{#each row.amount as opt}
											{opt}
										{/each}
									</select>
									<button type="submit" class="btn btn-filled-success btn-sm">Add</button>
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

<div class="card gap-4 m-4 p-4 flex w-full justify-right items-center">
	<form action="addpool">
		<label for="addpool" class="block m-2">
			Add Pool
			<select name="addpool" id="addpool" class="gap-4 flex-auto col-span-3">
				{#each poolList as pool}
					<option value={pool}>{pool}</option>
				{/each}
			</select>
		</label>
	</form>
	<input type="button" value="Add" class="btn btn-filled-success btn-xlg" />
</div>
