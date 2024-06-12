Assessment02 Contract Overview:

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
