---
title: How to "Freeze" Your Zorb NFT 
date: 2022-01-13
summary: "Learn how to transfer your Zorb without losing its color property! "
draft: false
tags:
- NFT
- web3
- engineering
---


In the 48 hours the [Zorb NFT drop](http://zorb.dev) was active, over 53,000 zorbs were minted. [Zorbs](https://github.com/ourzora/zorb) are colored orbs created by the [Zora](https://zora.co/) team - Zorbs are a long term branding and identity project. The main unique property of Zorbs is that the color of the Zorb depends on the wallet holding it. To explain more simply, a Zorb’s color is dependent on the wallet holding it - if you transfer your Zorb to someone else, the color WILL change.

Recently I had the chance to sit down with [Iain](twitter.com/isiain), engineer at Zora, on a Twitch stream where we minted an NFT. During that stream, the topic of Zorbs came up and Iain shared a secret - you can actually 'freeze' Zorbs! He literally deployed the contract to enable Zorb freezing mid-stream - and we froze a Zorb. I am now in possession of the first ever Frozen Zorb!

{{<youtube 7nm9h7bIkr8>}}




There’s now a way to [FREEZE your Zorb](https://github.com/ourzora/zorb/tree/main/packages/zorb-fridge-contracts), so when you send it to someone else, the colors will not change. In this article, I will walk you through how exactly to freeze your Zorb! 

# What you’ll need

- Enough ETH to pay for gas fees
- A [Zorb NFT](http://zorb.dev)
- Metamask or other [etherscan.io](http://etherscan.io)  comparable wallet

## Navigate to the contract

In this section, you will be explained how to get to the location to execute the transfer to the Zorb Fridge. 

You can also bypass this section and *[click here to get dropped directly onto the page you need to go to.](https://etherscan.io/address/0xca21d4228cdcc68d4e23807e5e370c07577dd152#writeContract)* 

1. Navigate to the Zorb contract website on [ethscan.io](http://ethscan.io) - the address of the Zorb contract is `0xCa21d4228cDCc68D4e23807E5e370C07577Dd152`. 
	![Image of Etherscan.io on the relevant contract page](/2022-01-10/NFT-1.png)

2. Click `Contract`  
	![Image showing etherscan website when you click on Contract](/posts/2022-01-10/NFT-2.png)

3. Select `Write Contract` from the submenu.


## Execute the Trade

1. Connect your wallet of choice that is holding the Zorb by clicking `Connect to Web3`
	![Image showing base etherscan open to contract page](/2022-01-10/NFT-3.png)
	![Image showing option to collect to metamask or wallet connect ](/2022-01-10/NFT-4.png)

2. Select `5. safeTransferFrom` 
    ![Etherscan safe transfer form, but empty](/2022-01-10/NFT-5.png)

3. For your `from(address)` put the address of your wallet (the one you’re connected to)

4. For the `to(address)`, use the address of the Freezer contract `0x539Fe1179b528C25E03698f3d51E2B8522B7261B`

5. Finally, select the ID of the Zorb you want to freeze.
    1. To find the ID of the Zorb, go to the etherscan of your wallet, select `Erc721 Token Txns`, and it’ll show all of your Erc721 tokens. From there, you can see all the Transfer Events that use `Zorbs(ZORB)` tokens, and the associated `Token ID`. That Token ID is what you will input into the final contact field. 
        
        ![Image showing the list of all the Zorbs Ali has minted on Etherscan, and the transaction details](/2022-01-10/NFT-6.png)
6. Click `Write`
    ![Image of the successfully filled out contract to write on etherscan](/2022-01-10/NFT-7.png)


The rest of transaction goes the same as executing a normal transaction through your wallet! Select your goal gas and wait for the transaction to go through. 

## Confirm Your Transaction

1. Go to your Zora profile
    ![Ali and Iain looking at Ali's profile on Zora](/2022-01-10/NFT-8.png)

2. Select `Minted`

3. Under Minted you will have a Zorb from the “Frozen Zorbs” collection. It’ll have the same Index ID number as the original Zorb, except the original Zorb will now be owned by the Freezer.  You will not be able to sell, trade, transfer, or burn the original, now frozen Zorb. 
    ![Ali and Iain looking at Ali's minted images on Zora](/2022-01-10/NFT-9.png)

    
    ![Ali and Iain looking at Zorb #1545's properties](/2022-01-10/NFT-10.png)


Congrats! Your Zorb is now frozen! 

<div style="width: 100%; max-width: 1240px; margin: 0 auto; position: relative;">
<style>
.nft-embed-wrapper > iframe {
width: 100%!important;
height:100%!important;
border: 0;
position: absolute;
top: 0;
left: 0;
}
</style>
<div class="nft-embed-wrapper" style="position: relative; width:100%; height:0; padding-bottom: calc(100% + 88px);"><iframe src="https://embed.zora.co/0x539Fe1179b528C25E03698f3d51E2B8522B7261B/1545?title=true&controls=false&loop=true&autoplay=true&market=false" width="100%" height="100%" scrolling="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-pointer-lock allow-same-origin allow-scripts allow-popups"></iframe></div>
</div>

Now you can give your friends the Zorb that represents your wallet! Have fun trading your custom colors! To unfreeze your Zorb, use the `unfreeze` transaction of [this contract](https://etherscan.io/address/0x539Fe1179b528C25E03698f3d51E2B8522B7261B#writeContract), `0x539Fe1179b528C25E03698f3d51E2B8522B7261B`, with the `token ID` of the Zorb you want to unfreeze. This is executed in a similar manner as above, by connecting your wallet, entering the token value, and submitting the transaction. 

**If you enjoyed this blogpost and want to donate - endingwithali.eth!**

# Bonus Video

Here’s a reading of **Blockchain for Babies**

{{<youtube ESxegjYVGgs>}}
