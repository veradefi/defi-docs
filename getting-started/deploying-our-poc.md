# Deploying Our PoC

### Follow the steps below to test our proof of concept that's deployed [here](http://sandbox.vera.financial/#/contracts)

1. Upload contract metadata and wasm \(.contract files\) for erc20, erc721 and AssetManager 
2. Instantiate erc20 and erc721 contracts first using Alice as owner. erc20 initial supply is set to 1 billion units and both contracts get 10 units endowment. 
3. Instantiate assetmanager contract using Alice as owner. Erc20 and Erc721 addresses will be set to the above deployed contracts; interest rate is set to 10 \(% per year\); transfer rate is set to 1 million \(erc20 per erc721 token\) and enabled is set to true. 
4. Alice, being owner of erc20 and erc721, grants approval to assetmanager calling `approve` and `setApprovalForAll` of erc20 and er721 respectively. 
5. Now Bob \(or any else with balance\) can mint an erc721 token, grant approval to assetmanager contract to spend this token, and `deposit` it in the assetmanager contract in exchange for 1 million erc20 tokens. These tokens are deducted from erc20 owner account \(in this case Alice\). 
6. There are some utility methods that can be called by anyone to check Bob's outstanding balance and interest payable etc. 
7. To repay, Bob needs to grant approval to assetmanager to spend his erc20 tokens. After that, he can call `withdraw` method providing the token\_id he is withdrawing. The assetmanager contract will deduct principal balance \(1 million\)+ interest from Bob's erc20 balance, deposit it in erc20 owner \(Alice\) and transfer erc721 token from Alice to Bob.

