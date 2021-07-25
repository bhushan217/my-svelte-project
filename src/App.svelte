<script>
	import Layout from './layout/Layout.svelte';
	import B2kSelect from './components/B2kSelect.svelte';
	export let name ='B2k'
	let options = [{label:'12A', value:'12A'},{label:'12B', value:'12B'}];
	let optionsGender = [{label:'Male', value:'M'},{label:'Female', value:'F'}];
  let user = {id: 1, name}
	let selectedValue;
	let gender;
</script>>

<Layout header hideHeader headerHeight={56} footerHeight={24} let:scroller>
  <div slot="header">
    <div class="header" class:shadow={!!scroller.scroll}>
			Page title
		</div>
  </div>

  <div>
    {#each Array(1) as _, i}
      <div class="item">Row {i}</div>
    {/each}
		<br/>
		<B2kSelect bind:options={options} bind:value={selectedValue} on:change={(option)=>console.log(option)}></B2kSelect>
		<br/>
		<B2kSelect bind:options={optionsGender} bind:value={gender} on:change={(option)=>console.log(option)}></B2kSelect>
  </div>
  <div slot="footer">
    <div class="footer" class:shadow={!!scroller.scroll}>
			DynoFields💙
		</div>
  </div>
</Layout>

<style>
	.header {
		background-color: #ce0a0a;
		height: 56px;
		line-height: 56px;
		color: #FFFFFF;
		padding-left: 16px;
	}

	.footer {
		background-color: #eee;
		text-align: center;
		height: 24px;
	}
	
	.shadow {
  	box-shadow: 0px 2px 8px #00000088;
	}
	
</style>