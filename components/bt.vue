<template>
  <div class="connect">
    <button class="button" @click="connect" @mousemove="moveMe">
      <span>Connect</span>
    </button>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      device: {},
      server: {}
    }
  },
  methods: {
    attach: async function(device) {
      console.log(device.id)

      // Connect to device server
      const server = await device.gatt.connect()

      this.device = device
      this.server = server
    },
    connect: async function () {
      const device = await navigator.bluetooth.requestDevice({
        filters: [{ services: ['ef680100-9b35-4933-9b10-52ffa9740042'] }],
        optionalServices: [
          "ef680200-9b35-4933-9b10-52ffa9740042",
          "ef680300-9b35-4933-9b10-52ffa9740042",
          "ef680400-9b35-4933-9b10-52ffa9740042",
          "ef680500-9b35-4933-9b10-52ffa9740042"
        ]
      });
      this.attach(device)
    },
    moveMe(e) {
      const x = e.pageX - e.target.offsetLeft
      const y = e.pageY - e.target.offsetTop

      e.target.style.setProperty('--x', `${ x }px`)
      e.target.style.setProperty('--y', `${ y }px`)
    }
  }
}
</script>

<style>
.connect {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

.button {
  position: relative;
  appearance: none;
  background: transparent;
  padding: 1em 2em;
  border: none;
  color: var(--fg);
  font-size: 1em;
  cursor: pointer;
  outline: none;
  overflow: hidden;
  border-radius: 100px;
  opacity: 0;
  transition: opacity 0.2s ease;
}

.button:hover {
  opacity: 1;
}

.button span {
  position: relative;
  pointer-events: none;
}

.button::before {
  --size: 0;
  content: '';
  position: absolute;
  left: var(--x);
  top: var(--y);
  width: var(--size);
  height: var(--size);
  background: radial-gradient(circle closest-side, hotpink, transparent);
  transform: translate(-50%, -50%);
  transition: width .5s ease, height .5s ease, opacity 0.5s ease;
  opacity: 0;
}
.button:hover::before {
  --size: 30vw;
  opacity: 1;
}
</style>
