<script>
    import { tick } from 'svelte'
  
    export let toggleOnce = false
    export let relative = true
  
    let active = false
  
    async function click() {
      active = true
    }
  </script>
  
  
  
  <span on:click={click} class:relative>
    <slot name="label" />
  

      <div class="confetti">
        <slot />
      </div>
 
  </span>
  
  
  
  
  <style>
    .relative {
      position: relative;
    }
  
    .relative .confetti {
      position: absolute;
      top: 50%;
      left: 50%;
    }
  
    .confetti {
      pointer-events: none;
    }
  </style>
  