<template>
  <div>
  </div>
</template>

<script lang="ts">
import Web3 from 'web3'
import helloworld from '../assets/HelloWorld.json'
export default {
  async setup () {
    const web3 = await new Web3('https://ropsten.infura.io/v3/afbbf905acb14dad8bd872c628058f52')
    const contractAddress = '0xF00125Fa190be6f186e50aA44bC35bb8F508Dd6e'
    // const helloworld = require('../asserts/HelloWorld.json')
    // console.log(JSON.stringify(decycle(helloworld)))
    const contract = await new web3.eth.Contract(helloworld.abi, contractAddress)
    console.log(contract)
    return {
      contract
    }
  }
}
</script>
