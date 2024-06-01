/*
Assessment Requirements
1. Create a variable that can hold a number of NFT's. What type of variable might this be?
2. Create an object inside your mintNFT function that will hold the metadata for your NFTs. 
   The metadata values will be passed to the function as parameters. When the NFT is ready, 
   you will store it in the variable you created in step 1
3. Your listNFTs() function will print all of your NFTs metadata to the console (i.e. console.log("Name: " + someNFT.name))
4. For good measure, getTotalSupply() should return the number of NFT's you have created
*/

let nftCollection = [];

function mintNFT(name,sex,shirtsytpe,eyeColor) {
    const nft = {
        Name: name,
        Sex: sex,
        Shirt_Type: shirtsytpe,
        Eye_Color: eyeColor
    };
    nftCollection.push(nft);
}

function listNFTs() {
    for (let i = 0; i<nftCollection.length; i++) {           // created a loop that will go through an array of NFTs' and will a.t.requirement
        console.log("Name: "+ nftCollection[i].Name);
        console.log("Sex: "+ nftCollection[i].Sex);
        console.log("Shirt Type: "+ nftCollection[i].Shirt_Type);
        console.log("Eye Color: "+ nftCollection[i].Eye_Color);
        console.log();
    }
}
function getTotalSupply() {
    console.log("Total NFTs Minted: "+ nftCollection.length);  // Total no. of NFTs data added
}

// Call your functions below this line
mintNFT("Gurdeep Singh", "M", "Polo", "Brown");
mintNFT("Jackal Sen","M","Shirt","Grey");
mintNFT("Alice J.", "F", "T-shirt", "Blue");
mintNFT("Sean Pole","F","T-Shirt","Green")

listNFTs();
getTotalSupply();
