<script>
  import { storeFE } from './../store/fieldStore.ts';
  export let objAttributes = {};
  const {index, id, label, disabled} = {...objAttributes};
  
  
  console.log("textarea here, showing you my field attributes:");
  console.log(objAttributes);
  </script>
<label class="field-label">{label}</label>
  <!-- <textarea bind:value={$storeFE.formElements[fIndex].fValue}></textarea> -->
  <textarea bind:value={objAttributes.value} ></textarea>
<style>
  .field-label { padding-right: 10px; font-weight: 500;}
  label { order: 2; }
  input { order: 1; }
</style>