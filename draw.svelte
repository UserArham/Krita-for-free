<script>
  let canvas;
  let ctx;
  let drawing = false;

  function startDrawing(event) {
    drawing = true;
    ctx.beginPath();
    ctx.moveTo(event.offsetX, event.offsetY);
  }

  function draw(event) {
    if (!drawing) return;
    ctx.lineTo(event.offsetX, event.offsetY);
    ctx.stroke();
  }

  function stopDrawing() {
    drawing = false;
  }

  function clearCanvas() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
  }

  // Initialize canvas context
  function setupCanvas() {
    ctx = canvas.getContext("2d");
    ctx.lineWidth = 2;
    ctx.lineCap = "round";
    ctx.strokeStyle = "#000";
  }
</script>

<style>
  canvas {
    border: 1px solid #ccc;
    cursor: crosshair;
  }
  button {
    margin-top: 10px;
  }
</style>

<canvas
  bind:this={canvas}
  width="500"
  height="400"
  on:mousedown={startDrawing}
  on:mousemove={draw}
  on:mouseup={stopDrawing}
  on:mouseleave={stopDrawing}
  on:touchstart|preventDefault={(e) => startDrawing(e.touches[0])}
  on:touchmove|preventDefault={(e) => draw(e.touches[0])}
  on:touchend|preventDefault={stopDrawing}
  on:touchcancel|preventDefault={stopDrawing}
  on:mount={setupCanvas}
/>

<button on:click={clearCanvas}>Clear</button>
