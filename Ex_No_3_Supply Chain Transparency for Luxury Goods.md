# Aim:
To develop a smart contract that tracks the supply chain of luxury goods, ensuring authenticity.
# Algorithm:
The manufacturer records product creation details on-chain.


The product moves through different supply chain checkpoints.


The ownership of the product can be transferred securely.


Buyers can verify the product’s authenticity.


# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract LuxurySupplyChain {
    struct Product {
        string name;
        address currentOwner;
        bool verified;
    }

    mapping(uint256 => Product) public products;

    event ProductRegistered(uint256 productId, string name);
    event OwnershipTransferred(uint256 productId, address newOwner);

    function registerProduct(uint256 productId, string memory name) public {
        require(products[productId].currentOwner == address(0), "Product already registered");
        products[productId] = Product(name, msg.sender, true);
        emit ProductRegistered(productId, name);
    }

    function transferOwnership(uint256 productId, address newOwner) public {
        require(products[productId].currentOwner == msg.sender, "Not the owner");
        products[productId].currentOwner = newOwner;
        emit OwnershipTransferred(productId, newOwner);
    }

    function verifyProduct(uint256 productId) public view returns (string memory, address, bool) {
        Product memory p = products[productId];
        return (p.name, p.currentOwner, p.verified);
    }
}
```
# Expected Output:
A luxury good (e.g., BOTTLE) is registered on-chain.

<img width="1600" height="898" alt="image" src="https://github.com/user-attachments/assets/86fba348-4b76-4f78-a337-4cb7753c51c4" />

<img width="1600" height="892" alt="image" src="https://github.com/user-attachments/assets/0f456c2d-57e5-4a7d-a04b-c7e98754b815" />

Ownership is transferred at every checkpoint.

<img width="1600" height="897" alt="image" src="https://github.com/user-attachments/assets/0fbc30e4-a110-464b-b303-aaa5bea6648d" />

Buyers can check the authenticity before purchasing.

<img width="1600" height="899" alt="image" src="https://github.com/user-attachments/assets/f56e59cb-424c-4194-81dd-e7d44810a62f" />


# High-Level Overview:
Helps prevent counterfeit luxury goods.


Teaches real-world supply chain use cases.

# RESULT : 
Thus a smart contract that tracks the supply chain of luxury goods ensuring authenticaly is executed sucessfully

