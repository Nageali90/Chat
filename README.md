<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" [content="width=device-width, initial-scale=1.0" />](https://johnDoe.github.io/chatcoin-wallet/)
  <title>Ethereum Hot Wallet</title>
  <script src="https://cdn.jsdelivr.net/npm/ethers@6.6.2/dist/ethers.umd.min.js"></script>
  <style>
    body { font-family: Arial, sans-serif; padding: 2rem; }
    button { margin-top: 1rem; padding: 0.5rem 1rem; }
    input { margin-top: 0.5rem; padding: 0.5rem; width: 100%; }
  </style>
</head>
<body>
  <h1>Ethereum Hot Wallet</h1>
  <button onclick="createWallet()">chat</button>
  <div id="wallet" style="margin-top: 1rem;"></div>  <h2>إرسال ETH</h2>
  <input type="text" id="toAddress" placeholder="عنوان المستقبل">
  <input type="text" id="amount" placeholder="المبلغ بـ ETH">
  <button onclick="sendTransaction()">إرسال</button>  <script>
    let wallet;
    let provider = new ethers.providers.JsonRpcProvider("https://mainnet.infura.io/v3/2a9b0faed1614cffbdb86503ff404bdb");

    async function createWallet() {
      wallet = ethers.Wallet.createRandom().connect(provider);
      const balance = await provider.getBalance(wallet.address);

      document.getElementById("wallet").innerHTML = `
        <p><strong>العنوان:</strong> ${wallet.address}</p>
        <p><strong>العبارة السرية:</strong> ${wallet.mnemonic.phrase}</p>
        <p><strong>الرصيد:</strong> ${ethers.formatEther(balance)} ETH</p>
      `;
    }

    async function sendTransaction() {
      const to = document.getElementById("toAddress").value;
      const amount = document.getElementById("amount").value;

      if (!wallet) {
        alert("أنشئ المحفظة أولاً");
        return;
      }

      const tx = await wallet.sendTransaction({
        to: to,
        value: ethers.parseEther(amount)
      });

      alert("تم إرسال المعاملة! Tx Hash: " + tx.hash);
    }
  </script></body>
</html>![1000017594](https://github.com/user-attachments/assets/31a0d84d-2777-4234-8644-185c7d22ae78)
 Chat
