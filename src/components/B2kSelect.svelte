<script >
	import { createEventDispatcher } from 'svelte';
import App from '../App.svelte';

	export const multiple = false;
	export const disabled = false;
  export let noDefault = false;
  export let defaultValue = {label:'-Select-',value:''}
	export let options = [];
	export let anySelected = false;
	export let selectedIndex = -1;
	export let value = {...defaultValue};
	let optionsEl;
	const dispatch = createEventDispatcher();
	
  const openOptions = (ev) => {
    // console.log('openOptions()',  ev.screenY , ev.clientY, ev.currentTarget.offsetY, screen.availHeight, ev)
    if(screen.availHeight - ev.clientY < 200){
      optionsEl.classList.add('pos-top')
    }else{
      optionsEl.classList.remove('pos-top')
    }
    optionsEl.classList.toggle('active')
  }
  const focusout = (ev)=>{
    //console.log('focusout()', ev)
    optionsEl.classList.remove('active')
  }

	const select = (option, i, e) => { 
    //console.log('select()', option);
    optionsEl.querySelectorAll('.b2k-option').forEach((el,i)=>el.classList.remove('selected'))
    e.currentTarget.classList.toggle('selected')
		selectedIndex = +i;
    anySelected = true;
    value = option;
		dispatch('change', {value: option}) 
	}
	
</script>

<div class=b2k-select-container tabindex="0" disabled
  on:click={openOptions} on:focusout={focusout}>
  <div class=b2k-caption >
    {value.label}
  </div>  
	<span class="b2k-options" bind:this={optionsEl}>
    {#if !noDefault}    
		<div class="b2k-option {defaultValue.value===value.value ? 'selected':''}" on:click={(e) => select(defaultValue, -1, e)} >
			<span class=b2k-option-label title="{defaultValue.label}">{defaultValue.label}</span>
		</div>
    {/if}
		{#each options as option, i}
		<div class="b2k-option {option.value===value.value ? 'selected':''}" on:click={(e) => select(option,i,e)} >
			<span class=b2k-option-label title="{option.label}">{option.label}</span>
		</div>
		{/each}
	</span>
</div>	

<style>
  .b2k-select-container{
    background-color: var(--fieldBgColor);
    border: 1px solid var(--fieldBorderColor);
    max-width: 400px;
    /* height: 32px; 
    overflow: hidden;
    text-overflow: ellipsis;*/
    position: relative;
    display: flex;
    flex-direction: column;
  }
  .b2k-caption{
    padding: 5px 2px;
    position: relative;
  } 
  .b2k-caption:hover, .b2k-option:hover{cursor: pointer;}
  .b2k-options {
    background-color: var(--fieldBgColor2);
    width: 99.9%;
    
    position: absolute;
    display: block;
    top: 100%;
    left: 0;
    right: 0;
    border: 1px solid var(--fieldBorderColor);
    border-top: 0;
    transition: all 0.3s;
    opacity: 0;
    visibility: hidden;
    pointer-events: none;
    z-index: 2;
  }
  /** use :global when css not applied in template*/
  :global(.b2k-options.pos-top) { 
    transform: translateY(calc(-100% - 26px));
  }
  .b2k-options .b2k-option {    
    position: relative;
    display: block;
    border-top: 1px solid var(--fieldBorderColor);
    color: var(--text-color);
    width: 99%;
    padding: 5px 2px;
  }
  .b2k-option:hover{    
    background-color: var(--fieldBgColor);
  }
  :global(.b2k-options .b2k-option.selected) {
    /* font-weight: 600; */
    color: var(--text-color-2);
  }
  :global(.b2k-options.active) {
    opacity: 1 !important;
    visibility: visible !important;
    pointer-events: all !important;
  }
  .b2k-caption::after {
    content: "";
    top: 12px;
    right: 10px;
    position: absolute;
    border-style: solid;
    border-width: 5px 5px 0 5px;
    border-color: var(--text-color) transparent transparent transparent;
  }
  
</style>