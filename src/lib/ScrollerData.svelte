<script>
  
  export let index
  export let offset
  export let progress
  
</script>

<div class="scroller-data">
  <div class="progress-box">
    <div class="progress-bar" style="transform: scaleX({progress});"/>
  </div>
  <p>INDEX: {index}</p>
  <p>OFFSET: {offset < 0 ? 0 : offset?.toFixed(2)}</p>
  <p>PROGRESS: {progress?.toFixed(2)}</p>
</div>

<style>
  .scroller-data {
    position: relative;
    background: #010101dd;
    padding: 0.625rem 0.5rem;
    width: 100%;
    color: #fafbfc;
    font-size: 0.75rem;
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-wrap: nowrap;
    overflow-x: auto;
  }

  p {
    margin: 0;
    font-variant-numeric: tabular-nums;
  }

  .progress-box {
    height: 0.125rem;
    width: 100%;
    background: #000000;
    position: absolute;
    top: 0;
    left: 0;
  }

  .progress-bar {
    height: 0.125rem;
    background-color: #ff4700;
    transform-origin: left;
  }

</style>
