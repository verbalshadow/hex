<script lang="ts">
	import { Paginator } from '@skeletonlabs/skeleton';
	import {
		createDataTableStore,
		dataTableHandler,
		tableInteraction,
		tableA11y
	} from '@skeletonlabs/skeleton';
	let poolList = ['Swap.HIVE:HBD', 'Swap.HIVE:DEC', 'Swap.HIVE:SPS'];
</script>

<section class="card gap-4 m-4">
	<!-- Search Input -->
	<div class="card-header">
		<input bind:value={$dataTableStore.search} type="search" placeholder="Search Coins/Tokens..." />
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
							<td
								role="gridcell"
								aria-colindex={4}
								tabindex="0"
								class="md:!whitespace-normal capitalize table-cell-fit"
							>
								{row.lastprice}
							</td>
							<td
								role="gridcell"
								aria-colindex={5}
								tabindex="0"
								class="md:!whitespace-normal table-cell-fit"
							>
								{row.amount}
							</td>
							<td class="table-cell-fit">
								{row.usd}
							</td>
							<td role="gridcell" aria-colindex={6} tabindex="0">
								<form>
									<div class="relative">
										<div
											class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none"
										/>
										<input
											type="number"
											id="order"
											class="block w-full"
											placeholder="0.000"
											required
										/>
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

<div class="card gap-4 m-4 flex w-full justify-right items-center">
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
