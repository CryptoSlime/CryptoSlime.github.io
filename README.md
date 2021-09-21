# CryptoSlime.github.io
CrytoSlime!

<html>
    <head>
        <title>Example HTML/JS Algorand SDK Clients</title>
<script src="scripts/algosdk.min.js"></script>

<script>

//recover address 
//put your mnemonic phrase to replace this
var mnemonic = "wood clump category carpet cabin cement joy cover this hour armor twist write trade term only label later lizard disease boil pelican dish ability this";
let account = algosdk.mnemonicToSecretKey(mnemonic);

window.onload = async () => {

    let url = 'https://api.testnet.algoexplorer.io/v2/transactions/params';
        let params= await (await fetch(url)).json();
        firstRound = params["last-round"];
        lastRound = params["last-round"] + 1000;
        genesisID = params["genesis-id"];
        genesisHash = params["genesis-hash"];
       params.fee= 1000;

    let getParams = {
        "flatFee": true,
        "fee": params.fee,
        "firstRound": firstRound,
        "lastRound": lastRound,
        "genesisID": genesisID,
        "genesisHash": genesisHash,

    };

amount = 1000000;
address = account.addr;

const receiver = "AXTW46L6EPL4V7XSJAR7X24ATUM4N43BA6HQT3IBG3RS6GZCOBJNR735NI";
let note = algosdk.encodeObj("payment for shirt");

let txn = algosdk.makePaymentTxnWithSuggestedParams(address, receiver, amount, undefined, note, getParams);        
let signedTxn = txn.signTxn(account.sk);



//console.log("Signed transaction with txID: %s", txId);


    var traxUrl = "https://api.testnet.algoexplorer.io/v2/transactions";


    fetch(traxUrl, {
        method: 'POST', // or 'PUT'
        headers: {
          'Content-Type': 'application/x-binary',
        },
        body: signedTxn,
      })
      .then(response => response.json())
      .then(data => {
        document.getElementById("examples").value = JSON.stringify(data);

      })
      .catch((error) => {
        console.error('Error:', error);
      });


    }




</script>

<style>
    .log {
        font-size: 18px;
        width:50%;
        padding:1%;
        height: 40%;
    }
</style>

</head>
<body>
    <p>Example output</p>
    <textarea id="examples" class="log"></textarea>


    </body>

</html>
