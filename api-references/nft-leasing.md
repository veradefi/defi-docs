---
description: Allow NFT owners to list their tokens to be rented by other users.
---

# NFT Leasing

### **listToken:**

**Input:** 

* NFT address, the tokenID
* Rent Amount daily. 
* Max lease duration

**Output:**

* Tx ID

Allow NFT owners to list their NFT assets for lease. 

### rent

**Input:** 

* Tx ID

  This function will be called by renter to lease a specific NFT asset.

### payRent

**Input:** 

* Tx ID

  This function will be called by borrower to pay rent

