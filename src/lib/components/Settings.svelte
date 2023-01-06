<script lang="ts">
    // import type { PageData } from './$types';
    
    let refreshTimes = [3, 6, 9, 30, 60];
    // export let data: PageData;
</script>

<section class="card gap-4 m-4 p-4 flex">
    <form action="refresh">
        <label for="refreshrat" class="block m-2">
            <span>Refresh Rate</span> 
        <select name="refreshrate" id="refreshrate" class="gap-4 flex-auto">
            {#each refreshTimes as rate } 
            <option value="{rate}">{rate} Secs</option>
            {/each}
        </select>
        </label>
        <label for="oldest" class="block m-2">
            <span>Oldest Date Pulled</span> 
        <input type="datetime-local" name="oldest" id="oldest" class="gap-4 flex-auto">
        <input type="button" value="Save" class="btn btn-filled-success btn-xlg gap-4 m-4 justify-end float-right">
        </label>
    </form>
</section>