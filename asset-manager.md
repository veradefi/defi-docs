# Asset Manager

### Preparation

We need to deploy erc20 and erc721 contracts before deploying AssetManager contract. Any standard erc20 and erc721 contracts will work.

### Deployment

The constructor needs 5 params:

```c
pub fn new(
            erc20_address: AccountId,
            erc721_address: AccountId,
            interest_rate: u64,
            transfer_rate: Balance,
            enabled: bool,
        ) -> Self 
```

1. erc20 contract address
2. erc721 contract address
3. yearly interest rate
4. transfer rate per token \(e.g. 200 erc20 per erc721\)
5. enable/disable borrowing

### Ownership

By default, the owner of AssetManager is same as the one who instantiates contract. There are certain actions that can only be performed by owner like modifying interest rate, modifying transfer rate, enabling/disabling borrowing etc. Ownership can be transferred to another account using `transfer_ownership(new_owner)`.

### Approvals

After deployment, the owner of the erc20 and erc721 needs to grant approval to the AssetManager contract to make transfers on their behalf. By default, the owner of AssetManager is considered the owner of the erc20 and erc721 contracts and all transfer takes place to/from this account. To change these addresses, there are utility methods `set_erc20_owner(erc20_owner)` and `set_erc721_owner(erc721_owner)` which can be called by owner of AssetManager to modify these accounts.

### Borrowing

Before borrowing erc20 tokens in exchange for erc721 token, the caller must grant approval to AssetManager contract to spend/transfer erc721 token on their behalf. The main method used to borrow is called `deposit(token_id, on_behalf_of)`. The caller specifies the erc721 `token_id` they want to deposit and `on_behalf_of` of address which can be used to send erc20 tokens to address other than caller if needed. The `erc20_owner` must have sufficient balance and must grant approval to AssetManager for the transfer to take place.

```c
pub fn deposit(
                &mut self,
                token_id: u32,
                on_behalf_of: AccountId
                ) -> Result<(), Error>
```

### Repayment

Before repaying erc20 tokens to release erc721 tokens from hold, the caller must grant approval to AssetManager contract to spend/transfer erc20 tokens on their behalf. The main method used to borrow is called `withdraw(token_id, on_behalf_of)`. The caller specifies the erc721 `token_id` they want to release and `on_behalf_of` of address which can be used to settle debt owed by another address. The `erc721_owner` must grant approval to AssetManager for the transfer to take place.

```c
pub fn withdraw(
                &mut self,
                token_id: u32,
                on_behalf_of: AccountId
                ) -> Result<(), Error>
```

### Interest Calculation

Interest is specified on contract instantiation in yearly interval and can be adjusted later on using `set_interest_rate(_interest_rate)` method. This can only be called by owner. Existing debts will not be affected by any interest rate adjustment and it will only affect future borrowings. Interest is compounded daily and calculated using binomial expansion.

```c
fn calculate_interest(
        &self,
        amount: u128,
        interest_rate: u64,
        current_timestamp: u64,
        date_borrowed: u64,
    ) -> Balance {
        let difference_in_secs: u128 =
            ((current_timestamp - date_borrowed) as u128 / 1000_u128).into(); // Total time elapsed in seconds
        let secs_in_day: u128 = 24 * 60 * 60;
        let difference_in_days: u128 = difference_in_secs / secs_in_day;
        let mut days_since_borrowed = difference_in_days;
        if difference_in_secs - (difference_in_days * days_since_borrowed) > 0 {
            days_since_borrowed = days_since_borrowed + 1;
        }
        let mut s = 0;
        let mut n = 1;
        let mut b = 1;
        let q: u128 = 365 * 100 / interest_rate as u128;
        for x in 0..8 {
            s = s + amount * n / b / (q.pow(x));
            if days_since_borrowed < x.into() {
                break;
            }
            n = n * (days_since_borrowed - x as u128);
            b = b * (x as u128 + 1);
        }
        s - amount
    }
```

### Transfer Rate

Transfer rate is specified on contract instantiation and can be adjusted later on using `set_trannsfer_rate(_transfer_rate)` method. This can only be called by owner and is specified in `number of erc20 tokens per erc721 token`. Existing debts will not be affected by any transfer rate adjustment and it will only affect future borrowings.

### Enabling/Disabling Borrowing

Owner can enable/disable borrowing on contract instantiation and later using `enable()` and `disable()` methods. On disable state, no borrowing takes place however repayment can be done in any state.

