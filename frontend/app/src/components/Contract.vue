<template>
  <div>
      <button @click="mintNFT(1)">mint</button>
  </div>
</template>

<script>
import Web3 from 'web3'
import myNFT from '../assets/MyNFT.json'
export default {
  async setup () {
    const mintNFT = async (tokenURI) => {
      const web3 = await new Web3('https://ropsten.infura.io/v3/afbbf905acb14dad8bd872c628058f52')
      const NFTContractAddress = '0x9EC94bC24bFf07E6318b6D5BFf3643dd19C2b4BA'
      const KobayashiNFT = await new web3.eth.Contract(myNFT, NFTContractAddress)
      // NFTの名前を表示
      const NFTname = await KobayashiNFT.methods.name().call()
      console.log(NFTname)
      const myAddress = '0x32a9E70324862ef7BF8bA7610AF701822ddE5364'
      const nonce = await web3.eth.getTransactionCount(myAddress, 'latest')
      console.log(nonce)

      const tx = {
        from: myAddress,
        to: NFTContractAddress,
        nonce: nonce,
        gas: 500000,
        maxPriorityFeePerGas: 2999999987,
        data: KobayashiNFT.methods.mintNFT(myAddress, tokenURI).encodeABI()
      }

      const signedTx = await web3.eth.accounts.signTransaction(tx, '8e1f202516e7cf758a112e3964a33ba6c0d0327757c747f414ee199c892a024a')
      const transactionReceipt = await web3.eth.sendSignedTransaction(signedTx.rawTransaction)
      console.log(`Transaction receipt: ${JSON.stringify(transactionReceipt)}`)
    }
    return {
      mintNFT
    }
  }
}
</script>
