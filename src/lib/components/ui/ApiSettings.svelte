<script>
  import { apiurl, pburl } from "$lib/scripts/req";
</script>

<p class="label">Quartz URL</p>
<div class="flex space-x-2">
  <input
    id="webport"
    class="input-bordered input-primary input w-full max-w-xs bg-base-300"
    type="text"
    placeholder={apiurl}
  />
</div>
<p class="label">Pocketbase URL</p>
<div class="flex space-x-2">
  <input
    id="webport"
    class="input-bordered input-primary input w-full max-w-xs bg-base-300"
    type="text"
    placeholder={pburl}
  />
</div>
