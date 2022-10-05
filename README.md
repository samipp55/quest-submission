# quest-submission

## Chapter 1 Day 1 
1. Blockchain is decentralized, open, database that anyone can view
2. Smart Contracts are programs, or "rulebooks" that developers make. Smart Contracts are fast, and there is no middleman. The Blockchain, and thus Smart Contracts, are extremely secure if we make them that way. Hard to get right: While Smart Contracts are cool, they are NOT smart. Can be malicious if the developer is mean. must make sure you interact with Smart Contracts that you know are secure. Cannot undo something
3. a transaction CHANGES the data on the Blockchain and a script is used to VIEW data on the Blockchain, they do not change it

## Chapter 1 Day 2
1. 1. Safety and Security, 2. Clarity, 3. Approachability, 4. Developer Experience and 5. Resource Oriented Programming
2. Those 5 pillars generates safety, clear, managetable, efficient and fast way to code and excecute code in Flow blockchain.

## Chapter 2 Day 1

``` cadence
pub contract JacobTucker {

pub let is: String

init() {
    self.is = "the best"
}
}
```
2. import JacobTucker from 0x03
```cadence
pub fun main(): String {
    return JacobTucker.is
    }
```
<img width="700" alt="Screenshot 2022-09-30 at 17 56 08" src="https://user-images.githubusercontent.com/114108357/193298113-0ccbd9a0-59db-4eb4-a239-62076f10fa7b.png">


## Chapter 2 Day 2
1. Script is for viewing not Changing anything
2. You sign transaction with AuthAccount type and way like that you can access the data in your account
3. Prepare phase is to access the information/data in your account and Execute phase do stuff to change the data on the blockchain
4.aAdd two new things inside your contract:
```cadence
    pub contract HelloWorld {
        pub var greeting: String
        pub var myNumber: Int
        pub fun changeGreeting(newGreeting: String) {
            self.greeting = newGreeting
        }
        pub fun updateMyNumber(newNumber: Int){
            self.myNumber = newNumber
        }
        init() {
            self.greeting = "Hello, World!"
            self.myNumber = 0
        }
    }
```

4.b Add a script that reads myNumber from the contract
```cadence
import HelloWorld from 0x01

pub fun main(): Int {
    return HelloWorld.myNumber
}
```
4.c Add a transaction that takes in a parameter named myNewNumber and passes it into the updateMyNumber function. Verify that your number changed by running the script again.
```cadence
import HelloWorld from 0x01
transaction(myNewNumber: Int) {
  prepare(acct: AuthAccount) {
  }
  execute {
    HelloWorld.updateMyNumber(newNumber: myNewNumber)
  }
}
```

## Chapter 2 Day 3
1. In a script, initialize an array (that has length == 3) of your favourite people, represented as Strings, and log it.
```cadence
pub fun main() {
    let ListOfText: [String] = ["Katja", "Osku", "Yoey"]
    log (ListOfText)
}
```

2. In a script, initialize a dictionary that maps the Strings Facebook, Instagram, Twitter, YouTube, Reddit, and LinkedIn to a UInt64 that represents the order in which you use them from most to least. For example, YouTube --> 1, Reddit --> 2, etc. If you've never used one before, map it to 0!

```cadence
pub fun main() {
    let distionaryOfSoMe: {String: UInt64} = {"Instagram": 1, "Youtube": 2, "Facebook": 3, "LinkedIn": 4, "Twitter": 5, "Reddit": 6}

    log (distionaryOfSoMe)
}
```

3. Explain what the force unwrap operator ! does, with an example different from the one I showed you (you can just change the type).

Unwrap operation ! Stops use optional types. e.g. if we have defined String? to value can be either String or nil. And after ! only String value is ok and if it is nil comes error.

4. Using this picture below, explain...

What the error message means: types are not right, optional type need to be added 

Why we're getting this error: I'm not sure, because for me it seems that returning value is String "Three". Of course if I try to return address 0x04 with String? program can return null, but this is not the case now... 

How to fix it: Add ? after String in line one --> pub fun main(): String?

## Chapter 2 Day 4

1. Deploy a new contract that has a Struct of your choosing inside of it (must be different than Profile).
2. Create a dictionary or array that contains the Struct you defined.
3. Create a function to add to that array/dictionary.
4. Add a transaction to call that function in step 3.
5. Add a script to read the Struct you defined.

Contract
```cadence
pub contract HelloWorld {

    pub var guitarGallery: {Address: GuitarFeatures}

    pub fun addGuitar(guitarFeatures: GuitarFeatures) {
        let address: Address = guitarFeatures.address
        self.guitarGallery[address] = guitarFeatures
        }

    pub struct GuitarFeatures {
        pub let address: Address
        pub let neckMaterial: String
        pub let bodyMaterial: String
        pub let fingerboardMaterial: String
        pub let bridgeType: String
        pub let pickupConfiguration: String
        pub let serialNumber: Int

    // `init()` gets called when this Struct is created...
    // You have to pass in 7 arguments when creating this Struct.
        init(_Address: Address, _NeckMaterial: String, _BodyMaterial: String, _FingerboardMaterial: String, _BridgeType: String, _PickupConfiguration: String, _SerialNumber: Int) {
            self.address = _Address
            self.neckMaterial = _NeckMaterial
            self.bodyMaterial = _BodyMaterial
            self.fingerboardMaterial = _FingerboardMaterial
            self.bridgeType = _BridgeType
            self.pickupConfiguration = _PickupConfiguration
            self.serialNumber = _SerialNumber
        }
    }
    init() {
        self.guitarGallery = {}
    }
}

```
Transaction:
```cadence

import HelloWorld from 0x01

transaction(address: Address, neckMaterial: String, bodyMaterial: String, fingerboardMaterial: String, bridgeType: String, pickupConfiguration: String, serialNumber: Int) {
  prepare(acct: AuthAccount) {
  }
  execute {
    let guitarFeatures = HelloWorld.GuitarFeatures(
            address: address,
            neckMaterial: neckMaterial,
            bodyMaterial: bodyMaterial,
            fingerboardMaterial: fingerboardMaterial,
            bridgeType: bridgeType,
            pickupConfiguration: pickupConfiguration,
            serialNumber: serialNumber
    )
    
    HelloWorld.addGuitar(guitarFeatures: guitarFeatures)
  }
}

```
Script (return)
```cadence

import HelloWorld from 0x01

pub fun main(): {Address: HelloWorld.GuitarFeatures} {
    return HelloWorld.guitarGallery
}
```

Script (log)
```cadence

import HelloWorld from 0x01

pub fun main() {
    log(HelloWorld.guitarGallery)
}
```
## Chapter 3 Day 1

1. In words, list 3 reasons why structs are different from resources.

Resource Must be destroyed after the use
Resource can exists in one location at the a time
Resource must be used exactly once

2. Describe a situation where a resource might be better to use than a struct.

When you need very secure solution
nft is good example that can exist in one place at the time


3. What is the keyword to make a new resource?

create

4. Can a resource be created in a script or transaction (assuming there isn't a public function to create one)?

transaction. It is action not look

5. What is the type of the resource below?

Boolean (true or falls)

6. I Spy 4 things wrong with this code. Please fix them
```cadense
pub contract Test {

    // Hint: There's nothing wrong here ;)
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): @Jacob { // there is 1 here 
        let myJacob <- create Jacob() // there are 2 here
        return <- myJacob // there is 1 here
```
