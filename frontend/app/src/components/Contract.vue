<template>
  <div>
  </div>
</template>

<script>
import Web3 from 'web3'
import helloworld from '../assets/HelloWorld.json'
import myNFT from '../assets/MyNFT.json'
export default {
  async setup () {
    const web3 = await new Web3('https://ropsten.infura.io/v3/afbbf905acb14dad8bd872c628058f52')
    const contractAddress = '0xF00125Fa190be6f186e50aA44bC35bb8F508Dd6e'
    const contract = await new web3.eth.Contract(helloworld, contractAddress)
    const helllo = await contract.methods.hello().call()
    console.log(helllo)

    const NFTContractAddress = '0x12eCD20dd90B5a06498A1690cF369E1BA3fE9366'
    const KobayashiNFT = await new web3.eth.Contract(myNFT, NFTContractAddress)
    // NFTの名前を表示
    const NFTname = await KobayashiNFT.methods.name().call()

    alert(NFTname)
    return {
      contract
    }
  }
}
</script>
