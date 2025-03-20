# NPCI Blockchain Assignment-9

## Lending & Borrowing Platform on Hyperledger Fabric [10 Marks]

## Assignment Objective

This assignment involves implementing a **lending and borrowing platform on Hyperledger Fabric**. The objective is to **develop a chaincode-based decentralized lending system**, allowing borrowers to request loans, lenders to provide funds, and loan repayments to be securely recorded on a Fabric blockchain network.

By completing this assignment, students will gain practical experience in:

*   Setting up a **Hyperledger Fabric network**.
*   Developing **chaincode** for loan issuance, repayments, and tracking.
*   Implementing **role-based access** for lenders, borrowers, and regulators.
*   Deploying and interacting with the lending system using **CLI and Fabric SDK**.

## Prerequisites

To successfully complete this assignment, ensure you have the following:

*   **GitHub Account** (for code submission).
*   **Docker** and **Docker Compose** installed.
*   **Go Programming Knowledge** (for writing chaincode).
*   **Basic Understanding of Hyperledger Fabric** (peer, orderer, chaincode concepts).
*   **Access to `fabric-samples` repository**: [Hyperledger Fabric Samples](https://github.com/hyperledger/fabric-samples).

## Steps to Follow

- This GitHub repository will be accessible to you once you accept the Assignment.
- You have to work directly in this GitHub repository. It is like your own copy of the original repository.
- You can use GitHub Codespace, or your own system to work on the Assignment. 
- To start a new Codespace, select `Code` dropdown >> `Create Codespace on main`. It will have Docker and Go language preinstalled.

**Note:** 
- It may take few minutes for the Codespace to start after you click on "Create Codespace on main".
- Use **Hyperledger Fabric v2.5.10** in GitHub Codespace for your implementation.
- Use the below commands to install Fabric samples, Docker images, and binaries:

  **Get the install script:**
    
  `curl -sSLO https://raw.githubusercontent.com/hyperledger/fabric/main/scripts/install-fabric.sh && chmod +x install-fabric.sh`

  **Run the script:**
    
  `./install-fabric.sh --fabric-version 2.5.10`


## Assignment Tasks

### 1. Setup Hyperledger Fabric Network [2 Marks]

*   Use **Hyperledger Fabric's `test-network`** to create a blockchain network.
*   The network should include:
    *   **Three peer organizations**: `RBI`, `HDFC`, and `SBI`.
    *   **One orderer organization** with a single orderer node.
    *   Each peer organization should have **at least one peer node**.

### 2. Implement Chaincode for ERC20-like Token [2 Marks]

*   Create a **chaincode in Go** for token operations similar to an ERC20 token.
*   The chaincode should support the following operations:
    *   **Loan Request (`RequestLoan`)**: Borrowers can request a loan specifying the **amount, duration, and interest rate**.
    *   **Loan Approval (`ApproveLoan`)**: Lenders review and approve loan requests.
    *   **Loan Disbursement (`DisburseLoan`)**: Once approved, the lender transfers funds to the borrower.
    *   **Loan Repayment (`RepayLoan`)**: Borrowers make repayments on the loan.
    *   **Loan Status (`CheckLoanStatus`)**: Verify if a loan is **`Pending`, `Active`, `Repaid`, or `Defaulted`**.
    *   **Loan Default (`MarkAsDefaulted`)**: Mark loans as defaulted if repayments are not made on time.
    *   **Collateral Handling (`AddCollateral`)**: Optionally, borrowers can provide collateral for secured loans.
    *   **Regulatory Audits (`GetLoanHistory`)**: Regulators can view the loan history for compliance checks.

### 3. Develop a Loan Management Portal [2 Marks]

*   Build a **web/api-based portal** for lenders and borrowers.
*   The portal should:
    *   Allow borrowers to request loans.
    *   Enable lenders to review, approve, and fund loans.
    *   Display loan balances, repayment schedules, and transaction history.
    *   Implement role-based authentication (borrowers, lenders, and regulators).
    *   Integrate with Fabric REST APIs to fetch ledger data.

### 4. Deploy and Test the Lending System [2 Marks]

*   Deploy the Fabric network and install chaincode on peers.
*   Run test transactions using CLI & Fabric SDK.
*   Perform the following operations:
    *   User A (borrower) requests a loan of `1000 USD` for `12 months` at `5% interest`.
    *   User B (lender) approves the loan and disburses funds.
    *   User A repays `300 USD` towards the loan.
    *   User A fails to repay in time, and the system marks the loan as defaulted.
*   Ensure data consistency across all peers.

### 5. Query and Validate Ledger Data [2 Marks]

*   **Query blockchain ledger to verify**:
    *   Loan approval and disbursement transactions.
    *   Repayment tracking and loan status updates.
    *   Collateral records and loan history.
    *   Access control enforcement (only lenders can approve loans, borrowers can only request loans).
*   **Validate that the system maintains compliance with financial regulations**.

### Sample Loan Object Model

```go
type Loan struct {
	LoanID         string   `json:"loanId"`          // Unique loan identifier
	BorrowerID     string   `json:"borrowerId"`      // ID of the borrower
	LenderID       string   `json:"lenderId"`        // ID of the lender (empty if loan is pending)
	Amount         float64  `json:"amount"`          // Loan amount requested
	InterestRate   float64  `json:"interestRate"`    // Interest rate for the loan
	Duration       int      `json:"duration"`        // Loan duration in months
	Status         string   `json:"status"`          // Loan status (Pending, Approved, Active, etc)
	DisbursementDate string `json:"disbursementDate"`// Timestamp of fund disbursement
	RepaymentDue   float64  `json:"repaymentDue"`    // Total amount due for repayment
	RemainingBalance float64 `json:"remainingBalance"` // Remaining balance to be repaid
	Collateral     string   `json:"collateral"`      // Collateral details (if any)
	Defaulted      bool     `json:"defaulted"`       // True if the loan is defaulted
	AuditHistory   []string `json:"auditHistory"`    // List of loan status changes
}
```


## Deliverables

* GitHub repository containing the following:
  * Fabric network setup scripts.
  * Chaincode implementation (`lendingChaincode.go`).
  * Transaction execution scripts (`invoke.sh`, `query.sh`).

* Screenshots or logs demonstrating:
  * Successful chaincode deployment.
  * Execution of loan requests, approvals, disbursements, repayments, and defaults.
  * Ledger queries showing loan history.

## Additional Notes

* Ensure all dependencies (Docker, Fabric binaries, Go) are installed before starting.
* Debug any issues using Fabric logs (`docker logs <peer/container_name>`).
* Implement TLS encryption & authentication for secure access.
* Use event listeners to capture and notify users of loan status update.

Good luck, and Happy coding! 🚀
