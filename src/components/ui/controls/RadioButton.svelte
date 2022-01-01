<script>
  /* Here we want to get the store index */
  import { storeFE } from './../store/fieldStore.ts';
  export let objAttributes = {};
  const {id, index, label, disable, options} = objAttributes;
  function fnDisable() {
    if (disable) {
      console.log('do some stuff like check: '+disable);
    }
  }
  console.log("radio here, showing you my field attributes:");
  console.log(objAttributes);
</script>
<label class="field-label">{label}</label>
{#if options}
{#each options as option, i}
<label for="{id+'_'+i}">
  <input type=radio name="{id}" id={id+'_'+i} value={option.value} bind:group={objAttributes.value} on:change={fnDisable}>
  {option.label}
</label>
{/each}
{/if}
<style>
  .field-label { padding-right: 10px; font-weight: 500;}
  label { order: 2; }
  input { order: 1; }
</style>