<script lang="ts">
import IoIosRadioButtonOff from 'svelte-icons/io/IoIosRadioButtonOff.svelte'
 import IoIosCloseCircleOutline from 'svelte-icons/io/IoIosCloseCircleOutline.svelte'
 import IoIosCheckmarkCircleOutline from 'svelte-icons/io/IoIosCheckmarkCircleOutline.svelte'
 export let checkedFrom:number = 0;
</script>

<div class="tile">
  {#if checkedFrom === 1}
    <IoIosCloseCircleOutline/>
  {:else if checkedFrom === 2}
    <IoIosCheckmarkCircleOutline/>
  {:else}
  <IoIosRadioButtonOff/>
  {/if}
</div>

<style>
.wrapper{
display: flex;
align-items:strech;
}
.tile{
  display: flex;
  place-items: center;
  width: 100%;
  height: 100%;
  background-color:#242424;
  border-radius: 8%;
}
.inner-bg{
  display:flex;
  place-items:center;
  width: 98%;
  height: 98%;
  background-color:#242424;
  border-radius: 5px;
}
.marker{
  display:inline-block;
}
svg{
  max-width:100%;
  max-height:100%;
}
</style>