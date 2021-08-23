<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  let main;
  export let isCompactMenu = false;
  export let scroller = {
    scroll: 0,
    direction: true,
    delta: 0,
    hide: false,
    initialScroll: 0,
  };
  export let header = false;
  export let headerHeight = 64;
  export let hideHeader = false;
  export let footer = false;
  export let footerHeight = 64;
  export let hideFooter = false;
  export let threshold = 64;

  const Scroll = (e) => {
    const scroll = e.target.scrollTop;

    scroller = {
      scroll,
      direction: scroll > scroller.scroll,
      delta: scroll - scroller.initialScroll,
      hide:
        scroll > threshold && scroller.hide
          ? scroll - scroller.initialScroll > -threshold
          : scroll - scroller.initialScroll > threshold,
      initialScroll:
        scroll > scroller.scroll != scroller.direction
          ? scroll
          : scroller.initialScroll,
    };

    dispatch("scroller", scroller);
  };
  const logoClick = (e) => {
    console.log(e);
    isCompactMenu = !isCompactMenu;
  }
  $: if (main) {
    main.style.setProperty("--header-height", headerHeight + "px");
    main.style.setProperty("--footer-height", footerHeight + "px");
  }
</script>

<main bind:this={main} class:header class:footer>
<!-- <main bind:this={main} class:header class:footer on:scroll={Scroll}> -->
  <div id="sidebar" class="app-sidebar {isCompactMenu?'compact':''}">
    <slot name="menus"/>
  </div>
  <div class="main-container {isCompactMenu?'compact':''}">
    <slot {scroller} />
  </div>
</main>

<div class="slotHeader" class:hide={hideHeader && scroller.hide}>
  <slot name="header" />
</div>

<div class="slotFooter" class:hide={hideFooter && scroller.hide}>
  <slot name="footer" />
</div>

<style>
  main {
    height: 100vh;
    overflow-y: auto;
    background-color: var(--bg-color);
    display: flex;
		flex-grow: 5;
  }
  .main-container{
    flex-grow: 4;
    margin-left:140px ;
  }
  :global(.main-container.compact){
    margin-left:64px !important ;
  }
  main.header {
    padding-top: var(--header-height, 0px);
  }
  main.footer {
    padding-bottom: var(--footer-height, 0px);
  }
  .slotHeader {
    position: fixed;
    top: 0px;
    left: 0px;
    width: 100%;
    transition: all 0.2s ease-in-out;
  }
  .slotHeader.hide {
    transform: translateY(-100%);
  }
  .slotFooter {
    position: fixed;
    bottom: 0px;
    left: 0px;
    width: 100%;
    transition: all 0.2s ease-in-out;
  }
  .slotFooter.hide {
    transform: translateY(100%);
  }

  .app-sidebar {
    height: 100vh;
    background-color: var(--bg-color);
    border: 1px solid var(--fieldBorderColor);
    box-shadow: 2px 2px 3px var(--fieldBorderColor);
    min-width: 48px;
    max-width: 200px;
    flex-shrink: 1;
    display: flex;
    flex-direction: column;
    margin-right: 5px;
    position: fixed;
  }

  .app-sidebar.compact {
    max-width: 48px !important;
  }
</style>
