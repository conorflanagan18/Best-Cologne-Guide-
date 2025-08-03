<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="Honest, fast, and simple fragrance breakdowns — all killer, no filler." />
  <title>Best Cologne Guide</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f9f9f9;
      margin: 0;
      padding: 0;
    }
    header {
      background: #111;
      color: #fff;
      padding: 1rem;
      text-align: center;
    }
    .container {
      padding: 2rem;
      max-width: 1000px;
      margin: auto;
    }
    .search-bar {
      margin-bottom: 1.5rem;
      display: flex;
      justify-content: center;
    }
    .search-bar input {
      padding: 0.5rem;
      width: 300px;
      font-size: 1rem;
      border: 1px solid #ccc;
      border-radius: 6px;
    }
    .cards {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 1.5rem;
    }
    .card {
      background: #fff;
      border-radius: 12px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.05);
      padding: 1rem;
    }
    .card h3 {
      margin: 0 0 0.5rem;
      font-size: 1.2rem;
    }
    .card p {
      margin: 0.3rem 0;
    }
    footer {
      text-align: center;
      font-size: 0.9rem;
      color: #888;
      padding: 1rem;
      margin-top: 2rem;
    }
  </style>
</head>
<body>
  <header>
    <h1>Best Cologne Guide</h1>
    <p>Honest, fast, and simple fragrance breakdowns — all killer, no filler.</p>
  </header>
  <div class="container">
    <div class="search-bar">
      <input type="text" id="search" placeholder="Search by name or scent type..." />
    </div>
    <div class="cards" id="fragrance-list"></div>
  </div>
  <footer>
    &copy; 2025 Best Cologne Guide
  </footer>
  <script>
    async function loadFragrances() {
      const res = await fetch('fragrances.json');
      const data = await res.json();
      return data;
    }

    function renderFragrances(fragrances) {
      const list = document.getElementById('fragrance-list');
      list.innerHTML = '';
      fragrances.forEach(frag => {
        const card = document.createElement('div');
        card.className = 'card';
        card.innerHTML = `
          <h3>${frag["Product Name"]}</h3>
          <p><strong>Scent:</strong> ${frag["Scent Type"]}</p>
          <p><strong>Description:</strong> ${frag["Description"]}</p>
          <p><strong>Longevity:</strong> ${frag["Longevity"]}</p>
          <p><strong>Projection:</strong> ${frag["Projection"]}</p>
        `;
        list.appendChild(card);
      });
    }

    function setupSearch(data) {
      const input = document.getElementById('search');
      input.addEventListener('input', () => {
        const val = input.value.toLowerCase();
        const filtered = data.filter(frag =>
          frag["Product Name"].toLowerCase().includes(val) ||
          frag["Scent Type"].toLowerCase().includes(val)
        );
        renderFragrances(filtered);
      });
    }

    loadFragrances().then(data => {
      renderFragrances(data);
      setupSearch(data);
    });
  </script>
</body>
</html>

