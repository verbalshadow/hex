<script type="ts">
  import {
    Table, 
    tableMapperValues, 
    createDataTableStore,
    dataTableHandler,
  } from '@skeletonlabs/skeleton';
  import { Pie } from 'svelte-chartjs';
  import { Chart as ChartJS, Title, Tooltip, Legend, ArcElement, CategoryScale } from 'chart.js'

  ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale)

  const sourceData = [
	 { position: 1, usd: 125.25, amount: 1.0079, symbol: 'Coins' },
	 { position: 2, usd: 35.24, amount: 4.0026, symbol: 'Tokens' },
	 { position: 5, usd: 255.27, amount: 10.811, symbol: 'Pools' },
	 { position: 4, usd: 65.25, amount: 9.0122, symbol: 'Games' },
	 { position: 3, usd: 15, amount: 6.941, symbol: 'Other' },
  ];
  
  let chartdata = sourceData.reduce((hold, curr) => { 
    hold.push(curr.amount)
    return hold}, [])
//   let total = chartdata.reduce(
//   (accumulator, currentValue) => accumulator + currentValue,
//   initialValue
// );
  const tableSimple = {
	 // A list of heading labels.
	 head: ['Symbol', 'Amount', 'USD'],
	 // The data visibly shown in your table body UI.
	 body: tableMapperValues(sourceData, ['symbol', 'amount', 'usd']),
	 // Optional: The data returned when interactive is enabled and a row is clicked.
	 meta: tableMapperValues(sourceData, ['position', 'symbol', 'amount', 'usd',]),
	 // Optional: A list of footer labels.
	 foot: ['<h3>Total</h3>', '', '<h3>15845.24</h3>']
  };
  
  let data = {
    labels: ["Coins", "Tokens", "Pools", "Games", "Other"],
    datasets: [
      {
        data: chartdata,
        backgroundColor: [
          "#F7464A",
          "#46BFBD",
          "#FDB45C",
          "#949FB1",
          "#4D5360",
          "#4D5360",
          "#AC64AD"
        ],
        hoverBackgroundColor: [
          "#FF5A5E",
          "#5AD3D1",
          "#FFC870",
          "#A8B3C5",
          "#616774",
          "#616774",
          "#DA92DB"
        ]
      }
    ]
  }
 let options = {
    responsive: true,
    position: 'chartArea'
  }
  const mySelectionHandler = () => {return true};
  

const dataTableStore = createDataTableStore(
	// Pass your source data here:
	sourceData,
	// Provide optional settings:
	{
		// The current search term.
		search: '',
		// The current sort key.
		sort: '',
		// Paginator component settings.
		pagination: { offset: 0, limit: 5, size: 0, amounts: [1, 2, 5, 10] }
	}
);

// This automatically handles search, sort, etc when the model updates.
dataTableStore.subscribe((model) => dataTableHandler(model));
</script>

<section class="card grid grid-cols-2 gap-4 m-4">
<div class="shrink p-4">
<Pie {data} {options}/>
</div>
<Table source={tableSimple} interactive={true} on:selected={mySelectionHandler} />
</section>

