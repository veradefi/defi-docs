# Lending Manager



```text
    pub fn list_token(
        &mut self,
        nft_address: AccountId,
        token_id: TokenId,
        beneficiary_address: AccountId,
        amount: u64,
        loan_duration: u64,
    ) -> Result<(), Error> {
        assert_eq!(self.is_enabled(), true, "Listing is not enabled");
        let caller = self.env().caller();
        let contract_address = self.env().account_id();
        // Transfer tokens from caller to contract

        let erc721_transfer =
            Self::transfer_erc721_token(nft_address, caller, contract_address, token_id);
        assert_eq!(
            erc721_transfer.is_ok(),
            true,
            "ERC721 Token transfer failed"
        );

        let loan_result = self.handle_listing(
            caller,
            nft_address,
            token_id,
            beneficiary_address,
            amount,
            loan_duration,
        );
        assert_eq!(loan_result.is_ok(), true, "Error listing token");

        let loan = loan_result.unwrap();
        self.env().emit_event(LoanListed {
            borrower: caller,
            nft_address: loan.nft_address,
            loan_id: loan.id,
            token_id: token_id,
            beneficiary_address: loan.beneficiary_address,
            amount: amount as u128,
            loan_duration: loan.duration,
        });

        Ok(())
    }
```

