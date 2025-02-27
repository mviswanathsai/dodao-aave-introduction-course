## Header
This is the course header. This will be added on top of every page. Go to [DoDAO.io](https://www.dodao.io) to know more.

 ---
 
 ## Other Features of AAVE
 
 **Flash Loans**        
#### What are Flash Loans?
* Flash loans are special transactions that allow you to borrow and repay assets, but unlike traditional DeFi borrowing, the money must be repaid within a single transaction. 
* Flash loans do not require any collateral to function, and are instantaneous, hence the term “flash”. 
* Flash loans are typically repaid in the same transaction, and they are only valid for as long as the liquidity remains in the pool. 
* However, if a flash loan trade doesn't return the full amount of liquidity to the pool, the entire transaction will be reversed, which will also reverse all previous actions.

#### Transactions
* A transaction is a way of transferring value or any other type of token using Blockchain. 
* In order to transfer cryptocurrency, you must have a digital wallet. This wallet must have a public and private key. 
* If your wallet is your bank account, your public key is your account number, other users use this to send you assets. 
* Similarly, your private key is your pin code, which allows you to access the assets in your wallet. 
* On every transaction, a fee is added, which acts as an incentive to miners to keep the chain secure.

#### Working of flash loans
##### **`flashLoan`** 
* Allows borrowers to access liquidity of *multiple reserves* in a single *flashLoan* transaction. 
* The borrower also has an option to open a stable or variable rate debt position backed by supplied collateral or 
 credit delegation in this case.

##### **`flashLoanSimple`:** 
  * Allows borrowers to access liquidity of *single reserve* for the transaction. 
  * In this case flash loan fee is not waived nor can the borrower open any debt position at the end of the transaction. 
  * This method is gas efficient for those trying to take advantage of simple flash loans with a single reserve asset.

#### Execution Flow
1. Your contract calls the Pool contract, requesting for a flash loan of a certain amount from reserve(s) using `flashLoanSimple()`` or `flashLoan()``.

2. After some sanity checks, the pool transfers the requested amount from reserve(s) to your smart contract, then calls `executeOperation()`` on the receiver contract.

3. Your smart contract, now holding the flash loaned amount, executes any arbitrary operation in its code.
    * In case of a `flashloanSimple`, your code has finished. You just need to approve the pool the loaned amount + fee. 
    * If you are doing a `flashLoan`,  then depending on the interest rate mode and whether or not you want to open a debt position after the flash loan, you must either approve the 
      flash loan + fee to the pool or provide sufficient collateral or credit delegation should be available to open the debt position.
    * If the amount owed is not available to the pool due to lack of balance or insufficient approved amount, then all changes made in the transaction are reverted.

4. All the above happens in one transaction block.

 #### Applications of flash loans

 **Arbitrage:** 
 * Users can earn a decent profit by trading assets at different platforms that offer different values. 
 * With flash loans, traders can launch an arbitrage without any existing assets. 
 * Therefore, arbitrage trades using a flash loan become "cost-free" as long as the traders can afford the gas and flash loan fee to launch the transaction.

 **Swapping collateral:**
 * Crypto asset investors can use collateral swapping to change out their investments without having to repay the debt of the original investment. 
 * Collateral swapping lets an investor replace their position with borrowed assets. 
 * Users can choose to pay back their CDP debt and take out all collateral, using part of it to repay flash loans and keeping the remaining for themselves.

 **Self Liquidation:**
 * Markets can be very volatile and can lead to liquidation of the sensitive positionsand liquidation can be quite expensive on certain platforms.  
 * There are many applications that make use of flash loans and liquidate the position on user’s behalf saving the user hefty liquidation fees of the protocol.
 
 
