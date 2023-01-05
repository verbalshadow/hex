<script lang="ts">
    import type { PageData } from './$types';
    
    let refreshTimes = [3, 6, 9, 30, 60];
    // export let data: PageData;
</script>

<section class="card">
    <form action="refresh">
        <label for="refreshrat">Refresh Rate</label>
        <select name="refreshrate" id="refreshrate">
            {#each refreshTimes as rate } 
            <option value="{rate}">{rate} Secs</option>
            {/each}
        </select>
    </form>
</section>