<script lang="ts">
    // import type { PageData } from './$types';
    
    let refreshTimes = [3, 6, 9, 30, 60];
    // export let data: PageData;
</script>

<section class="card gap-4 m-4 p-4">
    <form action="refresh">
        <label for="refreshrat" class="block">
            <span>Refresh Rate</span> 
        <select name="refreshrate" id="refreshrate" class="gap-4 p-4">
            {#each refreshTimes as rate } 
            <option value="{rate}">{rate} Secs</option>
            {/each}
        </select>
        </label>
        <label for="oldest">
            <span>Oldest Date Pulled</span> 
        <input type="datetime-local" name="oldest" id="oldest">
        <input type="button" value="Save" class="btn btn-filled-success btn-xlg gap-4 m-4 bottom-0 right-0">
        </label>
    </form>
</section>