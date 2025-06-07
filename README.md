<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Stock Price Tracker</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 min-h-screen flex items-center justify-center">
  <div class="bg-white p-6 rounded-lg shadow-lg w-full max-w-md">
    <h1 class="text-2xl font-bold mb-4 text-center">Stock Price Tracker</h1>
    <div class="mb-4">
      <input id="tickerInput" type="text" placeholder="Enter stock ticker (e.g., AAPL)" class="w-full p-2 border rounded">
      <button id="searchBtn" class="w-full mt-2 bg-blue-500 text-white p-2 rounded hover:bg-blue-600">Search</button>
    </div>
    <div id="stockInfo" class="text-center">
      <p class="text-gray-500">Enter a ticker symbol to see stock data</p>
    </div>
  </div>

  <script>
    // Simulated stock data (replace with real API call in production)
    const mockStockData = {
      'AAPL': { name: 'Apple Inc.', price: 175.25, change: 2.34 },
      'GOOGL': { name: 'Alphabet Inc.', price: 2800.45, change: -15.67 },
      'MSFT': { name: 'Microsoft Corp.', price: 305.12, change: 5.89 }
    };

    async function fetchStockData(ticker) {
      // Simulate API call with mock data
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve(mockStockData[ticker.toUpperCase()] || null);
        }, 500);
      });
    }

    document.getElementById('searchBtn').addEventListener('click', async () => {
      const ticker = document.getElementById('tickerInput').value.trim().toUpperCase();
      const stockInfo = document.getElementById('stockInfo');

      if (!ticker) {
        stockInfo.innerHTML = '<p class="text-red-500">Please enter a ticker symbol</p>';
        return;
      }

      const data = await fetchStockData(ticker);

      if (data) {
        const changeClass = data.change >= 0 ? 'text-green-500' : 'text-red-500';
        stockInfo.innerHTML = `
          <h2 class="text-xl font-semibold">${data.name}</h2>
          <p>Price: $${data.price.toFixed(2)}</p>
          <p class="${changeClass}">Change: ${data.change.toFixed(2)}</p>
        `;
      } else {
        stockInfo.innerHTML = '<p class="text-red-500">Stock not found</p>';
      }
    });
  </script>
</body>
</html>
