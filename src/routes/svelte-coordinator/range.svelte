<script>
  import { coordinator, clamp, scale } from "svelte-coordinator";

  let {
    width = "auto",
    min = 0,
    max = 100,
    value = $bindable([0, 100]),
  } = $props();

  let active = $state(-1);

  const handlers = {};

  handlers.onstart = ({ left, width }) => {
    active = value.findIndex(val => {
      let px = Math.round(scale(val, [min, max], [0, width]));
      return left >= px - 10 && left <= px + 10;
    });

    console.log(active)

    return active !== -1;
  };

  handlers.onaction = ({ left, width }) => {
    value[active] = clamp(Math.round(scale(left, [0, width], [min, max])), min, max);
  };

  handlers.onend = () => {
    active = -1;
  }
</script>

<div
  {@attach coordinator(handlers)}
  style="width: {width}"
>
{#each value as val, i}
  <i class="point" class:active={i === active} style="left: {scale(val, [min, max], [0, 100])}%"></i>
{/each}
</div>

<style>
  div {
    position: relative;
    height: 20px;
    margin: 40px;
  }

  div::before {
    content: "";
    position: absolute;
    top: 50%;
    height: 4px;
    width: 100%;
    border-radius: 2px;
    transform: translateY(-50%);
    background-color: #989899;
  }

  .point {
    position: absolute;
    top: 0;
    box-sizing: border-box;
    width: var(--size, 20px);
    height: var(--size, 20px);
    border-radius: 4px;
    border: 2px solid #fff;
    background-color: #e0e0e0;
    transform: translate(-50%);
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
  }

  .point.active {
    z-index: 100;
    background-color: #fe0a63;
  }
</style>
