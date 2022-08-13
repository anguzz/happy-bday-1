<script lang="ts">
  import Page from "$lib/components/Page.svelte";
  import Text from "$lib/components/Text.svelte";
  import { primaryBackground } from "$lib/utils/constants";
  export let backgroundClass = primaryBackground;
  import Confetti from "$lib/components/Confetti.svelte";
  import CollapsibleCard from 'svelte-collapsible-card'
  export let link:string;
  import { signatures } from "./signatures";
  /**------------------------------ below script for tap confetti----------------------------- */
  const duration = 1500
  
  /**
* @type {any[]}
*/
  let things = []
  /**
* @type {string | number | NodeJS.Timeout | undefined}
*/
  let timeout

  async function moveConfetti(event) {
    const { target, clientX, clientY } = event

    const elementY = target.getBoundingClientRect().top
    const elementX = target.getBoundingClientRect().left

    const x = clientX - elementX
    const y = clientY - elementY

    things = [...things, { x, y }]

    clearTimeout(timeout)

    timeout = setTimeout(() => things = [], duration)
  }
  
</script>


<!-----------------confetti click should encapsulate page---------------------------->
<div class="box" on:click={moveConfetti}>
  {#each things as thing}
    <div class="mover" style="left: {thing.x}px; top: {thing.y}px">
      <Confetti y={[-0.5, 0.5]} fallDistance=20px amount=10 {duration} />
    </div>
  {/each}
<Page id="content" title=" " {backgroundClass}><!-- edit page below-->

 <!-----------------collapsible card below---------------------------->
  <ul>
	
    { #each signatures as signature }
      <li>
        <CollapsibleCard>
          <div slot='header' class='header'>
            <div class='names'>
              <h2>{ signature.name }</h2>
            </div>
          </div>
          <div slot='body' class='body'>
            { signature.message } <br><br>
            <p>{ signature.message2 }</p>
            <a href={signature.link} class="link-text" target="_blank" rel="noopener noreferrer">
              { signature.link }
          </div>
        
        </CollapsibleCard>
      </li>
    { /each }
  
  </ul>
<!-----------------collapsible card below---------------------------->

</Page>
</div>
<!--------------------------------------------css--------------------------------------------------->
<style>
  .box {
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
      height: 100%;
      width: 100%;
      background: none;
      overflow: hidden;
    }
  
    .mover {
      position: absolute;
    }
  
    

    /*--------------------------------------------collpasible css --------------------------------------------*/
    ul {
		list-style: none;
		padding: 0;
		margin: 0 auto;
		width:80%;
		color: #f6aca2;
		font-size: 1.5rem;
    font-weight:bold;
    background-color:rgb(149, 106, 250);
    border-radius: 10px;
    
	}
	
	li {
		margin-bottom: 0em;
		border-bottom: 1px solid rgb(212, 137, 247);
	}
	
	.header {
		padding: 0.3em;
		display: flex;
    background-color: #9f6ee7;
    border-radius: 10px;
	}
	

	.names {
		padding: 0 0 0 1em;
		display: flex;
		flex-direction: column;
		justify-content: center;

	}
	
	h2 {
		margin: 0;
		width: 100%;
    
	}
	
	p {
		margin: 0;
	}
	
	.body {
    padding: 0 0 0 1em;
	}
  .link {
		background-color: var(--text);
		display: flex;
		align-items: center;
		justify-content: center;
		color: var(--left);
		font-size: 1.5rem;
		margin: 0;
		padding: 0.5em;
	}

	.link-text {
		color: #a1b0f6;
		border: 2px solid var(--left);
		border-radius: 0.25rem;
		padding: 0.25rem;
	}

	.link-text:hover {
		background-color: var(--left);
		color: #97e0ce;
	}
</style>

