<script>
	import Layout from './layout/Layout.svelte';
	import B2kSelect from './components/B2kSelect.svelte';
import B2kCheckBox from './components/B2kCheckBox.svelte';
import { bind } from 'svelte/internal';
	
	export let name ='B2k'
  let isCompactMenu = false;
	let noDefault = true;
	let options = [{label:'Mr', value:'Mr.'},{label:'Mrs.', value:'Mrs.'}];
	let optionsGender = [{label:'Male', value:'M'},{label:'Female', value:'F'}];
  let user = {id: 1, name}
	let selectedValue;
	let gender;
	let optionsCB = [{label:'Mr', value:'Mr.'},{label:'Mrs.', value:'Mrs.'}];
	
	
	const menus = [
		{icon: '🏐', label:'Football'},
		{icon: '🏆', label:'Awards'},
		{icon: '🔊', label:'Sound'},
		{icon: '🔔', label:'Notification'},
		{icon: '⚙', label:'Reminder'},
	];

	const logoClick = (e) => isCompactMenu = !isCompactMenu;
</script>

<Layout header hideHeader headerHeight={56} isCompactMenu={isCompactMenu} footerHeight={24} menus let:scroller>
  <div slot="header">
    <div class="header" class:shadow={!!scroller.scroll}>
			<div class="brand">
				<a href="#logo" class="logo-link" on:click|preventDefault={logoClick}>
					<i class="icon">🏹⌚✋🏾</i>
					<div class="logo-text"> LOGO </div>
				</a>
			</div>
			<div class="top-menu">Page title</div>
		</div>
  </div>
	
	<div slot="menus">
		{#each menus as menu, i}
    <div class="menu-item">
      <a href="#{menu.label}" class="menu-link" title="{menu.label}">
        <i>{menu.icon}</i>
        <div class="menu-text">{menu.label}</div>
      </a>
    </div>
    {/each}
  </div>

  <div>
    {#each Array(1) as _, i}
      <div class="item">Row {i}</div>
    {/each}

		<B2kCheckBox bind:options={optionsCB} 
		on:change={(option)=>console.log(option.detail.value)}></B2kCheckBox>
		
    {#each Array(14) as _, i}
		<br/>
		<B2kSelect bind:options={options} bind:noDefault={noDefault} bind:value={selectedValue} 
		on:change={(option)=>console.log(option.detail.value)}></B2kSelect>
		<br/>
		<B2kSelect bind:options={optionsGender} bind:value={gender} 
		on:change={(option)=>console.log(option.detail.value)}></B2kSelect>
    {/each}

  </div>
  <div slot="footer">
    <div class="footer" class:shadow={!!scroller.scroll}>
			DynoFields💙
		</div>
  </div>
</Layout>

<style>
	.header {
		background-color: var(--bg-color-2);
		height: 56px;
		line-height: 56px;
		color: #FFFFFF;
		display: flex;
		flex-grow: 5;
	}
	.header .brand{
		flex-shrink: 1;
		padding-left: 10px;
		background-color: var(--brand-color);
	}
	.header .brand .logo-text {		
		font-size: 2.2em;
		color: var(--text-color-2);
		padding-left: 5px;
		letter-spacing: 6px;
		font-weight: bold;
		font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
		text-shadow: 4px 8px 3px var(--bg-color);
	}

	.header .top-menu{
		background-color: var(--brand-color-2);
		padding-left: 5px;
		flex-grow: 4;
		justify-content: flex-end;
		padding-right: 10px;
	}

	.footer {
		background-color: var(--brand-color);
		text-align: center;
		padding-top: 5px;
		height: 24px;
	}
	
	.shadow {
  	box-shadow: 0px 2px 8px #00000088;
	}
	
	
  .menu-item {
    padding: 5px;
    height: 48px;
    box-shadow: 2px 1px 3px var(--fieldBorderColor);
  }
  .menu-item:hover{
    padding: 5px;
    background-color: var(--bg-color-2);
  }
  .menu-item a{ 
    color: var(--text-color); 
    cursor: pointer;
    display: flex;
    align-items: center;
    text-decoration: none;
    transition: all 0.4s ease;
  }
  .menu-item a .menu-text {
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
	}
  .menu-item a i, i.icon{ 
    height: 36px;
    min-width: 36px;
    border-radius: 16px;
    line-height: 36px;
    font-size: 1.4em;
    font-style: normal;
    text-align: center;
  }
  .menu-item a:hover{ 
    color: var(--text-color-2) !important;
  }
</style>