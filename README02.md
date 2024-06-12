Assessment02 Explaination

 Contract Overview:

 1)Public Variables:
  So there is public variable tokenName which is initialized to "DOGGYDO". This is the name of out token
  Public variable tokenAbbre string is also instantiated as "DOGO" This is a short name, an abbreviation of our token name.
  Total Supply: totalSupply variable: This keeps the total number of tokens minted. Initially, it is set to zero.

 2)Balances Mapping:
  Balances to store the balances of all token holders in an address => balance mapping. It helps to monitor the number of tokens each address owns.

3)Mint Function:
  We can use the mint function to create new tokens. Tx> is a special type which takes 2 parameters; address and value. When we call this function,
  This increases the totalSupply by the amount specified and takes that amount from the address provided.

4)Burn Function:
  Function burn (uint amount) Used to burn tokens. It also has two arguments, an address, and a value This function verify if the address has the amount of tokens to burn.
  In case it does, token will be subtracted from the totalSupply and from the balance of that address.

-->Let's look at an illustration. Assume that 1000 tokens are needed to be minted for an address:
  
  We pass the address and the value 1000 to the mint function call.
  There is an increase of 1000 in both the balance of that address and the totalSupply.
  Comparably, from the same address, if we wish to burn 500 tokens:

  We pass the address and the value 500 to the burn function when we call it.
  The function determines whether the address possesses 500 tokens or more. In that case, there is a 500 reduction in both the balance of that address and the totalSupply.


CODE:

    /*REQUIREMENTS:
    1. Your contract will have public variables that store the details about your coin (Token Name, Token Abbrv., Total Supply)
    2. Your contract will have a mapping of addresses to balances (address => uint)
    3. You will have a mint function that takes two parameters: an address and a value. 
       The function then increases the total supply by that number and increases the balance 
       of the “sender” address by that amount
    4. Your contract will have a burn function, which works the opposite of the mint function, as it will destroy tokens. 
       It will take an address and value just like the mint functions. It will then deduct the value from the total supply 
       and from the balance of the “sender”.
    5. Lastly, your burn function should have conditionals to make sure the balance of "sender" is greater than or equal 
       to the amount that is supposed to be burned.
    */ 




    contract MyToken{
    //public variable here
    string public tokenName = "DOGGYDO";
    string public tokenAbbre = "DOGO";
    uint public totalSupply = 0;

    //mapping variable here
    mapping(address => uint) public balances;

    //mint function
    function mint (address _address,uint _value) public {
        totalSupply += _value;
        balances[_address] += _value;
    }
    
    //burn function
        function burn (address _address,uint _value) public {
        if(balances[_address] >= _value){    
        totalSupply -= _value;
        balances[_address] -= _value;
        }
      }
    }
