<template>
  <div>
      <button @click='mintNFT(1)'>mint</button>
      <button @click='approveNFT(3)'>approve</button>
      <button @click='transferNFT(3)'>transfer</button>
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

    const transferNFT = async (tokenId) => {
      console.log('transfer')
      const web3 = await new Web3('https://ropsten.infura.io/v3/afbbf905acb14dad8bd872c628058f52')
      const NFTContractAddress = '0x9EC94bC24bFf07E6318b6D5BFf3643dd19C2b4BA'
      const myAddress = '0x32a9E70324862ef7BF8bA7610AF701822ddE5364'
      const myAddress2 = '0x3D896D141dC4eEe51E829CcA7003939be20c280A'
      const KobayashiNFT = await new web3.eth.Contract(myNFT, NFTContractAddress)
      const nonce = await web3.eth.getTransactionCount(myAddress, 'latest')
      console.log(nonce)
      const data = KobayashiNFT.methods.safeTransferFrom(myAddress, myAddress2, tokenId, '0x0').encodeABI()
      console.log(data)
      const tx = {
        from: myAddress,
        to: NFTContractAddress,
        nonce: nonce,
        gas: 500000,
        value: '0x0',
        data: data
      }
      const signedTx = await web3.eth.accounts.signTransaction(tx, '8e1f202516e7cf758a112e3964a33ba6c0d0327757c747f414ee199c892a024a').catch(err => {
        console.error(err)
      })
      const transactionReceipt = await web3.eth.sendSignedTransaction(signedTx.rawTransaction).catch(err => {
        console.error(err)
      })
      console.log(`Transaction receipt: ${JSON.stringify(transactionReceipt)}`)
    }

    const approveNFT = async (tokenId) => {
      console.log('transfer')
      const web3 = await new Web3('https://ropsten.infura.io/v3/afbbf905acb14dad8bd872c628058f52')
      const NFTContractAddress = '0x9EC94bC24bFf07E6318b6D5BFf3643dd19C2b4BA'
      const myAddress = '0x32a9E70324862ef7BF8bA7610AF701822ddE5364'
      const KobayashiNFT = await new web3.eth.Contract(myNFT, NFTContractAddress)
      const nonce = await web3.eth.getTransactionCount(myAddress, 'latest')
      console.log(nonce)
      const data = KobayashiNFT.methods.setApprovalForAll(myAddress, tokenId).encodeABI()
      console.log(data)
      const tx = {
        from: myAddress,
        to: NFTContractAddress,
        nonce: nonce,
        gas: 500000,
        value: '0x0',
        data: data
      }
      const signedTx = await web3.eth.accounts.signTransaction(tx, '8e1f202516e7cf758a112e3964a33ba6c0d0327757c747f414ee199c892a024a').catch(err => {
        console.error(err)
      })
      const transactionReceipt = await web3.eth.sendSignedTransaction(signedTx.rawTransaction).catch(err => {
        console.error(err)
      })
      console.log(`Transaction receipt: ${JSON.stringify(transactionReceipt)}`)
    }
    return {
      mintNFT,
      transferNFT,
      approveNFT
    }
  }
}
</script>
