---
description: >-
  Allow NFT owners to borrow stable coins, or other tokens against their NFT
  assets.
---

# NFT Lending

### **listToken**

**Input:** 

* NFT address, the tokenID
* Address in which they want to get paid and the amount 
* Loan duration

**Output:**

* Tx ID

This function will be used by borrowers to list a new loan opportunity.   
****When called, the user will be asked to approve the transaction, and the NFTs will be transferred to the smart contract as collateral. The function will generate a unique trade ID.

### Lend

**Inputs:**

* Tx ID

This function will be called by investors to perform a trade by sending the trade ID. The function will get the tokens to pay with from them.

### **withdraw**

**Inputs:**

* Tx ID

This function will be called by borrower to pay back their loans with interest and get back the NFT

### **cancleLoan**

**Inputs:**

* Tx ID

This function will be called by the investor to get NFT from the smart contract when the borrower fails to pay back on time.

### **listLoans**

**Inputs:** None

**Outputs:** List of available NFT for sale with details.

