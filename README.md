# Project Title
 smart contract to create your own ERC20 token 

 # Functionality

 This ERC20 contract provides the basic functionality required for a token that conforms to the ERC20 standard.name Stores the name of the token 
symbol Stores the symbol of the token (e.g., "MTK").
decimals Defines how divisible the token is. Commonly set to 18, meaning the token can be divided down to 18 decimal places.totalSupply The total amount of tokens that will ever exist._balances Keeps track of the token balance of each address._allowances Keeps track of allowances, which are permissions granted by a token holder to another address to transfer a certain number of tokens on their behalf.Event Transfer Triggered when tokens are transferred from one address to another.
Event Approval Triggered when an address approves another address to spend a certain amount of tokens on its behalf The constructor initializes the token with a name, symbol, total supply, and assigns the total supply to the contract creator's address balanceOf:Purpose to Retrieves the token balance of a specific address.Functionality to Checks if the address is valid and then returns the balance of that address.transferPurpose to Transfers tokens from the caller's address to another address.Functionality to Checks if the caller has enough balance and then transfers the specified amount to the recipient.
allowance Purpose to Returns the remaining amount of tokens that a spender is allowed to transfer from the owner's address.Functionality to Retrieves and returns the allowance from the _allowances mapping.

 #Code
 
 // SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;
 
 contract ERC20{
    string public name;
    string public symbol;
    uint8 public immutable decimals;
    uint256 public immutable totalSupply;
    mapping(address => uint256) _balances;
    mapping(address=> mapping(address => uint256)) _allowances;

    event Transfer(address indexed _from, address indexed _to, uint256 _value);
    event Approval(address indexed _owned, address indexed _spender,uint256 _value);

    constructor( string memory _name,string memory _symbol,uint256 _totalSupply)
       {
        name=_name;
        symbol=_symbol;
        decimals=20;
        totalSupply=_totalSupply;
        _balances[msg.sender]=_totalSupply;
        }

        function balanceOf(address _owner) public view returns(uint256)
        {
            require(_owner!= address(0), "!Za");
            return _balances[_owner];
        }

        function transfer(address _to, uint256 _value) public returns(bool)
        {
        require((_balances[msg.sender] >= _value) && (_balances[msg.sender] > 0), "!Bal");
        _balances[msg.sender] -= _value;
        _balances[_to] += _value;
        emit Transfer(msg.sender, _to, _value);
        return true;
         }

     function transferFrom(address _from, address _to, uint256 _value) public returns(bool)
     {
        require(_allowances[msg.sender][_from] >= _value, "!Alw");
        require((_balances[_from] >= _value) && (_balances[_from] > 0), "!Bal");
        _balances[_from] -= _value;
        _balances[_to] += _value;
        _allowances[msg.sender][_from] -= _value;
        emit Transfer(_from, _to, _value);
        return true;
    }

    function approve(address _spender, uint256 _value) public returns(bool) 
    {
        require(_balances[msg.sender] >= _value, "!bal");
        _allowances[_spender][msg.sender] = _value;
        emit Approval(msg.sender, _spender, _value);
        return true;
    }

    function allowance(address _owner, address _spender) public view returns(uint256)
    {
        return _allowances[_spender][_owner];
    }
}
      
# Author
Harmandeep Singh

mail:harmandeep7448@icloud.com
