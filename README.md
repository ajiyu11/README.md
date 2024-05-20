## Public Variables for Coin Details

Token Name: A string that holds the name of the token.
Token Abbreviation: A shorter version of the token name.
Total Supply: The total number of tokens available.

string public tokenName;
string public tokenAbbrv;
uint256 public totalSupply;

## Mapping of Addresses to Balances

This mapping will associate each address (which represents a user) with a balance (number of tokens they hold

mapping(address => uint256) public balances;

## Mint Function

Parameters: An address and a value.
Functionality:
Increases the total supply by the value.
Increases the balance of the specified address by the same value.

function mint(address _to, uint256 _value) public {
    totalSupply += _value;
    balances[_to] += _value;
}

## Burn Function

Parameters: An address and a value.
Functionality:
Decreases the total supply by the value.
Decreases the balance of the specified address by the same value, ensuring that the address has enough balance to burn.


Parameters: An address and a value.
Functionality:
Decreases the total supply by the value.
Decreases the balance of the specified address by the same value, ensuring that the address has enough balance to burn.

## Conditional Check in Burn Function

Ensures the sender’s balance is sufficient to burn the specified amount of tokens, preventing negative balances.
pragma solidity ^0.8.0;

contract Token {
    // Public variables to store coin details
    string public tokenName;
    string public tokenAbbrv;
    uint256 public totalSupply;

    // Mapping of addresses to balances
    mapping(address => uint256) public balances;

    // Constructor to initialize the token details
    constructor(string memory _name, string memory _abbrv, uint256 _initialSupply) {
        tokenName = _name;
        tokenAbbrv = _abbrv;
        totalSupply = _initialSupply;
        balances[msg.sender] = _initialSupply; // Assign initial supply to contract creator
    }

    // Mint function to create new tokens
    function mint(address _to, uint256 _value) public {
        totalSupply += _value;
        balances[_to] += _value;
    }

    // Burn function to destroy tokens
    function burn(address _from, uint256 _value) public {
        require(balances[_from] >= _value, "Insufficient balance to burn");
        totalSupply -= _value;
        balances[_from] -= _value;
    }
}
