<script>
  //import { validate } from './validate.js';	// NOTE: for this JS to work in Svelte we must export the validate var in validate.js
  import Field from './controls/Field.svelte';	// used to build our form fields
  import FormField from './sections/form-field.svelte';	// just for show
  import { storeFE } from './store/fieldStore.ts';	// store our form state
	import { createEventDispatcher } from 'svelte';

  let objForm;	// @testing - used to listen for changes in our form state
  const delay = (ms = 3000) => new Promise(r => setTimeout(r, ms));  
  const dispatch = createEventDispatcher();
  async function getFieldMeta() {
    dispatch('loading', true);
    let response = await fetch('./assets/form-fields.json');
    let users = await response.json();
    await delay();
    dispatch('loading', false);
    return users;
  }
  const promise = getFieldMeta();
  const unsubscribe = storeFE.subscribe(value => {objForm = value;});
  //$storeFE = objFormConfig;
</script>

<div class="p-4">
	<div class="mb-3">
		<a href="#about" class="anchor" aria-hidden="">About this app. (instructions below)</a>
	</div>
  <div>
    {#await promise}
      <p>Loading...</p>
    {:then objFormConfig}
      <div class="form-container">
        <form id="main" novalidate>
        {#each objFormConfig.controls as control}
          <FormField>
            <Field objAttributes={control}></Field>
          </FormField>
        {/each}
        </form>
      </div>
    {:catch error}
      <p style="color: red">{error.message}</p>
    {/await}	
  </div>
</div>

<style>
  .form-container {    
		border: 1px solid var(--fieldBorderColor);
		border-radius: 2px;
		box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
		padding: 1em;
		margin: 0 0 1em 0;
  }
</style>
