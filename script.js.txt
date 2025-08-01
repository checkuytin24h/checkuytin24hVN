let gdvData = [];

fetch('data.json')
  .then(response => response.json())
  .then(data => {
    gdvData = data;
    renderTable();
  });

function renderTable() {
  const tbody = document.getElementById('gdvTable');
  gdvData.forEach(item => {
    const row = `<tr>
      <td>${item.name}</td>
      <td>${item.zalo}</td>
      <td><a href="${item.facebook}" target="_blank">Xem Facebook</a></td>
      <td>${item.amount.toLocaleString()} đ</td>
    </tr>`;
    tbody.innerHTML += row;
  });
}

function searchGDV() {
  const input = document.getElementById('searchInput').value.toLowerCase();
  const resultDiv = document.getElementById('result');
  const found = gdvData.find(item =>
    item.name.toLowerCase().includes(input) ||
    item.facebook.toLowerCase().includes(input)
  );

  if (found) {
    resultDiv.innerHTML = `<p style="color:green;">✔ ${found.name} đã cọc ${found.amount.toLocaleString()} đ</p>`;
  } else {
    resultDiv.innerHTML = `<p style="color:red;">❌ Không tìm thấy trong danh sách GDV</p>`;
  }
}