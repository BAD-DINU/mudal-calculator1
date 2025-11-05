<!DOCTYPE html>
<html lang="si">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>මුදල් එකතු කිරීම (Mobile)</title>
  <style>
    body {
      font-family: "Noto Sans Sinhala", sans-serif;
      margin: 0;
      padding: 15px;
      background: #f2f2f2;
    }
    .container {
      max-width: 100%;
      background: white;
      border-radius: 12px;
      padding: 15px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    h2 {
      text-align: center;
      color: #2e7d32;
      margin-bottom: 20px;
    }
    table {
      width: 100%;
      border-collapse: collapse;
    }
    th, td {
      border-bottom: 1px solid #ddd;
      padding: 10px;
      text-align: center;
      font-size: 18px;
    }
    th {
      background: #e8f5e9;
      color: #1b5e20;
    }
    input[type="number"], input[type="tel"] {
      width: 100%;
      padding: 12px;
      font-size: 18px;
      border: 1px solid #aaa;
      border-radius: 8px;
      text-align: center;
      box-sizing: border-box;
    }
    input[type="number"]:focus {
      border-color: #4CAF50;
      box-shadow: 0 0 5px rgba(76,175,80,0.5);
      outline: none;
    }
    .result {
      margin-top: 20px;
      text-align: center;
      font-size: 20px;
      font-weight: bold;
      color: #1b5e20;
      background: #dcedc8;
      padding: 15px;
      border-radius: 8px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>මුදල් එකතු කිරීම</h2>

    <table>
      <thead>
        <tr>
          <th>නෝට්ටුව</th>
          <th>ගණන</th>
          <th>එකතුව (රු)</th>
        </tr>
      </thead>
      <tbody id="moneyTable"></tbody>
    </table>

    <div class="result" id="grandTotal">මුළු එකතුව: රු. 0.00</div>
  </div>

  <script>
    const denominations = [20, 50, 100, 500, 1000, 5000];
    const tableBody = document.getElementById("moneyTable");

    denominations.forEach(value => {
      const row = document.createElement("tr");
      row.innerHTML = `
        <td>රු. ${value}</td>
        <td><input type="tel" id="note${value}" inputmode="numeric" pattern="[0-9]*" value="0"></td>
        <td id="total${value}">0</td>
      `;
      tableBody.appendChild(row);
    });

    function calculateTotal() {
      let grandTotal = 0;
      denominations.forEach(v => {
        const input = document.getElementById('note' + v);
        const count = parseInt(input.value) || 0;
        const subtotal = count * v;
        grandTotal += subtotal;
        document.getElementById('total' + v).innerText = subtotal.toLocaleString('si-LK');
      });
      document.getElementById('grandTotal').innerText = "මුළු එකතුව: රු. " + grandTotal.toLocaleString('si-LK');
    }

    tableBody.addEventListener('input', e => {
      if (e.target && e.target.type === 'tel') calculateTotal();
    });
  </script>
</body>
</html>
