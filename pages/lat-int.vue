<template>
  <div></div>
</template>
<script>
export default {
  data: {
    channel: {
      general: [1, 2, 3],
      infra: [3, 5],
      humor: [4, 6],
    },
  },
  computed: {
    res(a) {
      for (var e in this.channel) {
        console.log(e);
      }
    },
  },
};
var channel = {
  general: [1, 2, 3],
  infra: [3, 5],
  humor: [4, 6],
};
let min = 0;
let c = [];
for (var e in channel) {
  console.log(channel[e]);
  let f = channel[e].find((i) => {
    return i == 3;
  });
  if (f) {
    if (min == 0) min = channel[e].length;
    if (channel[e].length < min) {
      min = channel[e].length;
      console.log("channel", e);
      c = e;
    } else if (min == channel[e].length) {
      console.log("channel else", e);
      c.push(e);
    }
  }
}
console.log("res", c);
</script>
