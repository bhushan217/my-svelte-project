<script >
	import { createEventDispatcher } from 'svelte';

  export const multiple = false;
	export const disabled = true;
  export let noDefault = false;
  export let defaultValue = [{label:'-Select-',value:''}]
	export let options = [];
	export let anySelected = false;
	export let selectedIndex = -1;
  export let checked = false;
	export let value = [...defaultValue];
	let optionsEl;
	const dispatch = createEventDispatcher();

  const onClick = (option) => {
    if(disabled) return
    checked = !checked
		dispatch('change', {value: checked ? option : undefined}) 
  }
  const focusout = (ev)=>{
    //console.log('focusout()', ev)
    optionsEl.classList.remove('active')
  }
  </script>
  
{#each options as option, i}
<div class=b2k-checkbox-container tabindex="0" disabled={disabled}
on:click={() => onClick(option)} on:focusout={focusout}>
  <span class="b2k-checkbox {checked? 'checked':''}" bind:this={optionsEl}>
  </span>
  <div class=b2k-label >
    {option.label}
  </div>  
</div>
{/each}
<style>
  .b2k-checkbox-container{
    display: flex;
    cursor: pointer;
    position: relative;
    margin-bottom: 5px;
  }
  .b2k-checkbox{
    border-radius: 6px;
    border: 1px solid var(--fieldBgColor2);
    background-color: var(--fieldBgColor);
    color: var(--text-color);
    display: inline-flex;
    align-items: center;
    width: 16px;
    height: 16px;
  }
  .b2k-label{
    align-self: flex-end;
    margin-left: 10px;
  }
  :global(.b2k-checkbox.checked){
    border: 1px solid var(--brand-color);
    background-color: var(--brand-color);
    color: var(--text-color-2);
    position: relative;
  }
  :global(.b2k-checkbox.checked::after){
    content:'\2714';
    padding-left: 0 5px;
    position: absolute;
    left: 1px;
  }

</style>