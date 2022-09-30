# quest-submission

## Chapter 1 Day 1 
1. Blockchain is decentralized, open, database that anyone can view
2. Smart Contracts are programs, or "rulebooks" that developers make. Smart Contracts are fast, and there is no middleman. The Blockchain, and thus Smart Contracts, are extremely secure if we make them that way. Hard to get right: While Smart Contracts are cool, they are NOT smart. Can be malicious if the developer is mean. must make sure you interact with Smart Contracts that you know are secure. Cannot undo something
3. a transaction CHANGES the data on the Blockchain and a script is used to VIEW data on the Blockchain, they do not change it

## Chapter 1 Day 2
1. 1. Safety and Security, 2. Clarity, 3. Approachability, 4. Developer Experience and 5. Resource Oriented Programming
2. Those 5 pillars generates safety, clear, managetable, efficient and fast way to code and excecute code in Flow blockchain.

## Chapter 2 Day 1
1. pub contract JacobTucker {

pub let is: String

init() {
    self.is = "the best"
}
}

2. import JacobTucker from 0x03

pub fun main(): String {
    return JacobTucker.is
    }

<img width="700" alt="Screenshot 2022-09-30 at 17 56 08" src="https://user-images.githubusercontent.com/114108357/193298113-0ccbd9a0-59db-4eb4-a239-62076f10fa7b.png">


## Chapter 2 Day 2
1. Script is for viewing not Changing anything
2. You sign transaction with AuthAccount type and way like that you can access the data in your account
3. Prepare phase is to access the information/data in your account and Execute phase do stuff to change the data on the blockchain
4.a Add two new things inside your contract:

pub var myNumber: Int
init() {
  self.myNumber = 0
  }

4.b
pub fun updateMyNumber(): Int {
  
A function named updateMyNumber that takes in a new number named newNumber as a parameter that has type Int and updates myNumber to be newNumber
Add a script that reads myNumber from the contract

Add a transaction that takes in a parameter named myNewNumber and passes it into the updateMyNumber function. Verify that your number changed by running the script again.
