<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>เกมจับคู่สิ่งของในห้องน้ำ</title>
  <style>
    body { 
      font-family: sans-serif; 
      text-align: center; 
      background: #f1f3f5; 
    }
    h1 { 
      margin: 20px; 
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(3, 200px); /* 3 ใบต่อแถว */
      grid-gap: 20px;
      justify-content: center;
    }
    .card {
      width: 200px; 
      height: 200px;
      display: flex; 
      align-items: center; 
      justify-content: center;
      font-size: 2rem; 
      cursor: pointer;
      background: #74c0fc; 
      color: transparent;
      border-radius: 16px;
      text-align: center; 
      padding: 10px;
      box-shadow: 2px 2px 8px rgba(0,0,0,0.2);
      transition: transform 0.2s;
    }
    .card:hover {
      transform: scale(1.05);
    }
    .flipped {
      background: #fff; 
      color: black;
      border: 2px solid #74c0fc;
    }
  </style>
</head>
<body>
  <h1>🛁 เกมจับคู่สิ่งของในห้องน้ำ 🧼</h1>
  <div class="grid" id="grid"></div>

  <script>
    const pairs = [
      {img:"🚽", word:"Toilet"},
      {img:"🚿", word:"Shower"},
      {img:"🪥", word:"Toothbrush"},
      {img:"🧴", word:"Shampoo"},
      {img:"🪞", word:"Mirror"},
      {img:"🧻", word:"Tissue"},
    ];

    // สร้างไพ่ (ภาพ + คำ)
    let cards = [];
    pairs.forEach(p => {
      cards.push({content:p.img, type:"img", key:p.word});
      cards.push({content:p.word, type:"word", key:p.word});
    });

    // สับไพ่
    cards = cards.sort(() => 0.5 - Math.random());
    const grid = document.getElementById("grid");

    let first = null, second = null, lock = false;

    cards.forEach(c => {
      const card = document.createElement("div");
      card.className = "card";
      card.textContent = c.content;
      card.dataset.type = c.type;
      card.dataset.key = c.key;
      card.addEventListener("click", () => flip(card));
      grid.appendChild(card);
    });

    function flip(card) {
      if (lock || card.classList.contains("flipped")) return;
      card.classList.add("flipped");
      if (!first) {
        first = card;
      } else {
        second = card;
        lock = true;
        if (first.dataset.key === second.dataset.key && first.dataset.type !== second.dataset.type) {
          first = second = null;
          lock = false;
        } else {
          setTimeout(() => {
            first.classList.remove("flipped");
            second.classList.remove("flipped");
            first = second = null;
            lock = false;
          }, 1000);
        }
      }
    }
  </script>
</body>
</html>

