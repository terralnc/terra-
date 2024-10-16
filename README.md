# terra-
terra happy
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Crypto Swap Interface</title>
  <link rel="stylesheet" href="styles.css">
  <script src="https://cdn.jsdelivr.net/gh/ethereum/web3.js/dist/web3.min.js"></script>
</head>
<body>
  <div class="swap-container">
    <h1>Swap</h1>

    <!-- Cüzdan Bağlantısı -->
    <div class="wallet-section">
      <button id="connect-wallet-btn" onclick="connectWallet()">Cüzdanı Bağla</button>
      <p>Cüzdan Adresi: <span id="wallet-address">Bağlanmamış</span></p>
    </div>

    <!-- Token Bilgileri -->
    <div class="token-container">
      <div class="token">
        <label for="token1">BNB</label>
        <input type="number" id="token1-amount" placeholder="0.03936 BNB">
        <p>Balance: <span id="bnb-balance">0.000000</span> BNB</p>
      </div>
      <div class="swap-arrow">⇅</div>
      <div class="token">
        <label for="token2">USDT</label>
        <input type="number" id="token2-amount" placeholder="10.7111 USDT">
        <p>Balance: <span id="usdt-balance">40</span></p>
      </div>
    </div>

    <!-- Swap Kontrolleri -->
    <div class="controls">
      <button id="max-btn">MAX</button>
      <button id="swap-btn">Swap</button>
    </div>

    <!-- Ek Bilgiler -->
    <div class="info">
      <p>Price: <span id="price">0.00367551 BNB per USDT</span></p>
      <p>Slippage Tolerance: <input type="number" id="slippage" value="0.5" step="0.1">%</p>
    </div>

    <!-- Risk Tarama Butonu -->
    <button id="scan-risk-btn">Scan Risk</button>
  </div>

  <script src="script.js"></script>
</body>
</html>

Adım 3: CSS Dosyası (styles.css)

Bu dosya, sitenizin görünümünü şekillendirir. Karanlık tema ve modern stil ile kullanıcı dostu bir arayüz oluşturur.

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #181818;
  font-family: Arial, sans-serif;
  color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.swap-container {
  background-color: #2C2C2C;
  padding: 20px;
  border-radius: 10px;
  width: 350px;
  text-align: center;
}

h1 {
  margin-bottom: 20px;
}

.token-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.token {
  width: 45%;
}

label {
  display: block;
  margin-bottom: 5px;
}

input[type="number"] {
  width: 100%;
  padding: 10px;
  border-radius: 5px;
  border: none;
  background-color: #404040;
  color: #fff;
  text-align: right;
}

.swap-arrow {
  font-size: 24px;
  color: #ff9900;
}

.controls {
  margin-bottom: 20px;
}

button {
  background-color: #ff9900;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  color: #fff;
  cursor: pointer;
}

button:hover {
  background-color: #ffcc33;
}

#max-btn {
  margin-right: 10px;
}

.info {
  margin-bottom: 20px;
}

input[type="number"]#slippage {
  width: 50px;
  padding: 5px;
}

#scan-risk-btn {
  background-color: #404040;
  padding: 10px;
}

#scan-risk-btn:hover {
  background-color: #555555;
}

.wallet-section {
  margin-bottom: 20px;
  text-align: center;
}

#connect-wallet-btn {
  background-color: #ff9900;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

#connect-wallet-btn:hover {
  background-color: #ffcc33;
}

#wallet-address {
  color: #ffcc33;
  font-weight: bold;
}

Adım 4: JavaScript Dosyası (script.js)

Bu dosya, cüzdan bağlantısı ve bakiyeleri yönetir. Ayrıca swap işlemlerini ve risk analizini gerçekleştirecek fonksiyonları içerir.

let web3;

async function connectWallet() {
  if (window.ethereum) {
    web3 = new Web3(window.ethereum);
    try {
      // MetaMask ile cüzdan bağlama
      const accounts = await ethereum.request({ method: 'eth_requestAccounts' });
      const account = accounts[0];
      document.getElementById('wallet-address').innerText = account;

      // Kullanıcının BNB bakiyesini al
      const bnbBalance = await web3.eth.getBalance(account);
      const bnbInEth = web3.utils.fromWei(bnbBalance, 'ether');
      document.getElementById('bnb-balance').innerText = parseFloat(bnbInEth).toFixed(6);

    } catch (error) {
      console.error("Cüzdan bağlanamadı:", error);
    }
  } else {
    alert("MetaMask tarayıcı eklentisini kurmanız gerekiyor.");
  }
}

document.getElementById('swap-btn').addEventListener('click', () => {
  const bnbAmount = parseFloat(document.getElementById('token1-amount').value);
  const usdtAmount = parseFloat(document.getElementById('token2-amount').value);
  if (bnbAmount && usdtAmount) {
    alert(Swapping ${bnbAmount} BNB for ${usdtAmount} USDT);
  } else {
    alert("Lütfen geçerli miktarlar girin.");
  }
});

document.getElementById('max-btn').addEventListener('click', () => {
  const bnbBalance = parseFloat(document.getElementById('bnb-balance').textContent);
  document.getElementById('token1-amount').value = bnbBalance;
});

document.getElementById('scan-risk-btn').addEventListener('click', () => {
  alert("Risk taraması yapılıyor...");
});
