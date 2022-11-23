# Installation 

If you're a Mac m1 silion chip follow these instructions 
  <a href="https://github.com/buildspace/buildspace-projects/blob/main/Solana_And_Web3/en/Section_2/Resources/m1_setup.md" /> Here <a/>

If you're a windows machine follow these instructions 
  <a href="https://github.com/buildspace/buildspace-projects/blob/main/Solana_And_Web3/en/Section_2/Resources/windows_setup.md" /> Here <a/>
  
# Frontend
1. Create an react project `npx create-react-app my-app` 
2. Cd to the project `cd my-app`
3. Start the project `npm start`
4. Install serum dependency `npm install --save @project-serum/anchor` or `yarn add @project-serum/anchor`
5. install solana web3 dependency `npm install --save @solana/web3.js` or `yarn add @solana/web3.js`
6. Make sure you have phantom wallet installed. <a href="https://phantom.app/">link </a>
7. Check if the wallet is present in browser by `window.solana.isPhantom`
```
if (window?.solana?.isPhantom) {
    console.log('Phantom wallet found!');
} else {
    alert('Solana object not found! Get a Phantom Wallet 👻');
}
```
8. Add a button to connect to the wallet
```
const connectWallet = async () => {
  const { solana } = window;

  if (solana) {
    const response = await solana.connect();
    console.log('Connected with Public Key:', response.publicKey.toString());
  }
};
```


# Solana blockchain

1. Verify if you have installed solana by `solana --version`
2. Set solana config to localhost for development `solana config set --url localhost`
3. Get solana config `solana config get`
//You will see something like this :
```
Config File: /Users/abhishek/.config/solana/cli/config.yml
RPC URL: http://localhost:8899
WebSocket URL: ws://localhost:8900/ (computed)
Keypair Path: /Users/abhishek/.config/solana/id.json
Commitment: confirmed
```
4. Run a solana test validatator by `solana-test-validator`
5. if you're using imtel mac and you see an error you need to install `OpenSSL` the easy way to install would be by using brew by `brew install openssl`

# Install Anchor
1. Install Anchor using cargo cli here  `cargo install --git https://github.com/project-serum/anchor anchor-cli --locked`
2. Check if the anchor is installed by `anchor --version`
3. Create an anchor project `anchor init project-name --javascript` 
4. Generate a local keypair for solana network `solana-keygen new`
5. Get address of the solana `solana address`
6. Test if the init project is all fine `anchor test`
7. Write contract + testcase
8. Deploy on devnet `solana config set --url devnet`
9. Verify if the configuration is pointing to devnet by confirming the url to `https://api.devnet.solana.com`
10. Send solana faucet to the address `solana airdrop 2 ` and check the balance if the address has recived the faucet by `solana balance
`
11. Update `Anchor.toml` file by replacing `localnet` to `devnet`. Change `[programs.localnet]` to `[programs.devnet]` and then, 
change `cluster = "localnet"` to `cluster = "devnet"`
12. Now build the project `anchor build`
13. create a new build for us with programId by `solana address -k target/deploy/project-name-keypair.json`
14. Copy the address and replace in the `lib.rs` which we see in the top like :
`declare_id!("programID")`
15. Also replace `anchor.toml` with the programID `project-name="programID"`
16. Build the solana project to deplaoy to the devent by `anchor build` and `anchor deploy`
17. Confirm that everything is same after deployment by `anchor test`
18. When we build the anchor project it generates idl (similar to ABI in eth) find `target/idl/project-name.json` 
you'll see metadata and address, copy the address
19. Upload the idl to solana directly by `anchor idl init  -f target/idl/project-name.json `solana address -k target/deploy/project-name-keypair.json`
20. if you would like to update the contract repeate the same steps from 7-18 and if you would like to update the contract address 
then you can use `anchor idl upgrade` instead of `anchor idl init`


  
