<template>
  <div>
    {{ version }}
  </div>
</template>

<script>
import web3 from "web3";
export default {
  setup() {
    const version = web3.version;
    return {
      version,
    };
  },
};
</script>
