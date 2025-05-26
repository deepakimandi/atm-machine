# atm-machine

## Functional Requirements

- Users can insert their card and enter a PIN for authentication.
- The system validates the PIN before allowing access to account operations.
- Users can perform basic operations like cash withdrawal and balance inquiry.
- The ATM dispenses cash only if the user has a sufficient balance and the machine has enough inventory.
- The system transitions through various states: Idle, Has Card, Select Operation, Transaction.
- After completing a transaction, the system ejects the card and returns to the Idle state.
- The ATM maintains a cash inventory with multiple denominations.
- The system logs transactions for auditing purposes.
- Maintenance mode disables user operations during servicing.



## Entity/Data Model

- **Card**
  - `cardNumber`: String  
  - `pin`: int  
  - `accountNumber`: String  

- **Account**
  - `accountNumber`: String  
  - `balance`: double  

- **ATMInventory**
  - `cashInventory`: Map<CashType, Integer>  

- **CashType**
  - `value`: int  
  - *(Enum values: `BILL_100`, `BILL_50`, `BILL_20`, `BILL_10`, `BILL_5`, `BILL_1`)*

- **ATMMachineContext**
  - `currentState`: ATMState  
  - `currentCard`: Card  
  - `currentAccount`: Account  
  - `atmInventory`: ATMInventory  
  - `accounts`: Map<String, Account>  
  - `stateFactory`: ATMStateFactory  
  - `selectedOperation`: TransactionType  

- **ATMStateFactory**
  - `instance`: ATMStateFactory  

- **TransactionType**
  - *(Enum values: `WITHDRAW_CASH`, `CHECK_BALANCE`)*

- **ATMState** (Abstract Interface)
  - `getStateName()`: String  
  - `next(context: ATMMachineContext): ATMState`  

- **IdleState**
  - Inherits from `ATMState`  
  - Represents the ATM waiting for a card  

- **HasCardState**
  - Inherits from `ATMState`  
  - Represents the state when a card is inserted  

- **SelectOperationState**
  - Inherits from `ATMState`  
  - Represents the state to select an operation (withdraw/check balance)  

- **TransactionState**
  - Inherits from `ATMState`  
  - Represents the transaction processing state  

---

## API Design
