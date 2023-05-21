<script>
  import AdSlot from "./components/AdSlot.svelte";
</script>

<style>
  :global(body) {
    background: black;
    font-family: "Inter" !important;
  }
</style>

<div class="w-[700px] m-auto text-white/40 p-10">
  <h2 class="text-xl text-white font-semibold">Anzeigen-Dashboard</h2>
  <p class="my-3">Verwalte die Classboard-Anzeigen hier.</p>

  <div class="w-full mt-5 text-xs flex">
    {#each [6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17] as item}
      <div class="min-w-[50px] w-[50px] pl-[4px] border-l border-white/20">
        {item}
      </div>
    {/each}
  </div>

<div class="w-[600px] overflow-hidden">
     <AdSlot backgroundColor="bg-green-500">
      Anzeige Nr. 4098
    </AdSlot>
     <AdSlot backgroundColor="bg-blue-500">
      Anzeige Nr. 4095
    </AdSlot>
</div>

</div>