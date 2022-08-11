<script>
    import Confetti from "$lib/components/Confetti.svelte";
  
    const duration = 2000
  
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
  
  
  
  <div class="box" on:click={moveConfetti}>
    <span>Click in me</span>
  
    {#each things as thing}
      <div class="mover" style="left: {thing.x}px; top: {thing.y}px">
        <Confetti y={[-0.5, 0.5]} fallDistance=20px amount=10 {duration} />
      </div>
    {/each}
  </div>
  
  
  
  <style>
    .box {
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
      height: 100%;
      width: 100%;

      background: none;
      min-height: 100vh;
      overflow: hidden;
    }
  
    .mover {
      position: absolute;
    }
  
    span {
      pointer-events: none;
    }
  </style>