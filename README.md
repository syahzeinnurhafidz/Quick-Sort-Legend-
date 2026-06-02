<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Quick Sort Legend Game Group-2</title>

    <style>
      /* 📱 HP */
      @media (max-width: 600px) {
        #panel,
        #container,
        #controls,
        #advantagePanel {
          width: 96%;
        }

        #stepText {
          margin-bottom: 2px;
          padding: 6px 8px;
          font-size: 12px;
        }

        #container {
          margin-top: -10px; /* 🔥 jarak diperbaiki */
          height: 100px;
        }

        .bar {
          min-width: 10px;
          width: 4vw;
          font-size: 8px;
        }

        button {
          flex: 1 1 100%;
          font-size: 13px;
        }

        #panel h2 {
          font-size: 14px;
        }

        #stepText {
          font-size: 12px;
        }
      }

      /* 🔥 FIX BACKGROUND MOBILE */
      @media (max-width: 768px) {
        body::before {
          background-position: center center !important;
          background-size: cover !important;

          width: 100vw;
          height: 100vh;

          position: fixed;
        }
      }

      /* 💻 LAPTOP BESAR */
      @media (min-width: 1200px) {
        #panel,
        #container,
        #controls,
        #advantagePanel {
          max-width: 1400px;
        }

        .bar {
          width: 3vw;
          max-width: 45px;
        }

        #stepText {
          font-size: 14px;
        }

        button {
          font-size: 15px;
        }
      }
      #advantagePanel {
        width: 94%;
        max-width: 1200px;
        margin: 10px auto 25px;
        padding: 14px;
        background: #0f172a;
        border-radius: 12px;
        text-align: left;
      }

      #advantagePanel h2 {
        margin: 0 0 10px;
        font-size: 16px;
        color: #34d399;
      }

      #advantagePanel ul {
        margin: 0;
        padding-left: 18px;
        font-size: 12px;
        line-height: 1.6;
        opacity: 0.95;
      }

      #advantagePanel li {
        margin-bottom: 8px;
      }
      * {
        box-sizing: border-box;
        -webkit-tap-highlight-color: transparent;
      }

      .intro-text {
        font-size: 10px;
        line-height: 1.7;
        max-width: 900px;
        margin: 10px auto 15px auto;
        padding: 0 10px;

        color: #cbd5f5;

        text-shadow: 0 0 10px rgba(56, 189, 248, 0.25);
      }

      html,
      body {
        margin: 0;
        padding: 0;
        height: 100%;
      }

      body {
        font-family: helvetica, sans-serif;
        color: white;
        text-align: center;
        min-height: 100vh;
        overflow-x: hidden;
        background: transparent; /* penting */
        position: relative;
        z-index: 0;
      }

      /* 🎯 BACKGROUND FIX (TIDAK MENGGANGGU KONTEN) */
      body::before {
        content: "";
        position: fixed;

        inset: 0;

        width: 100vw;
        height: 100vh;

        background-image: url("https://as2.ftcdn.net/v2/jpg/06/63/35/29/1000_F_663352917_us0OvSTRvzTn759Ddx0rUMkxq3QLnZqS.jpg");

        background-size: cover;
        background-position: center center;
        background-repeat: no-repeat;

        transform: translateZ(0); /* 🔥 fix mobile repaint */
        will-change: transform;

        z-index: -2;
        pointer-events: none;
      }

      html,
      body {
        margin: 0;
        padding: 0;

        width: 100%;
        min-height: 100%;

        overflow-x: hidden;

        background: #000;
      }

      /* 🌑 overlay gelap */
      body::after {
        content: "";
        position: fixed;
        inset: 0;
        background: rgba(0, 0, 0, 0.5);

        z-index: -1;
        pointer-events: none;
      }

      /* 🌌 JUDUL HIDUP */
      .game-title {
        position: relative;
        width: 94%;
        max-width: 1200px;

        margin: 14px auto;
        padding: 18px;

        font-size: min(4vw, 16px);
        font-weight: bold;
        letter-spacing: 2px;

        color: #ffffff;
        text-align: center;

        border-radius: 20px;

        /* background kosmik */
        background: linear-gradient(
          135deg,
          rgba(15, 23, 42, 0.88),
          rgba(30, 41, 59, 0.75),
          rgba(56, 189, 248, 0.18)
        );

        backdrop-filter: blur(8px);

        border: 1px solid rgba(255, 255, 255, 0.15);

        /* glow */
        box-shadow:
          0 0 12px rgba(56, 189, 248, 0.4),
          0 0 30px rgba(168, 85, 247, 0.25),
          inset 0 0 20px rgba(255, 255, 255, 0.05);

        overflow: hidden;

        /* animasi hidup */
        animation:
          floatTitle 3s ease-in-out infinite,
          glowPulse 2.5s ease-in-out infinite;
      }

      /* ✨ efek cahaya bergerak */
      .game-title::before {
        content: "";

        position: absolute;
        top: -50%;
        left: -20%;

        width: 140%;
        height: 220%;

        background: linear-gradient(
          120deg,
          transparent,
          rgba(255, 255, 255, 0.18),
          transparent
        );

        transform: rotate(12deg);

        animation: shine 4s linear infinite;
      }

      /* 🌟 teks glow */
      .game-title {
        text-shadow:
          0 0 8px rgba(255, 255, 255, 0.8),
          0 0 16px rgba(56, 189, 248, 0.9),
          0 0 24px rgba(168, 85, 247, 0.7);
      }

      /* 🔥 animasi naik turun */
      @keyframes floatTitle {
        0% {
          transform: translateY(0px);
        }

        50% {
          transform: translateY(-6px);
        }

        100% {
          transform: translateY(0px);
        }
      }

      /* 💡 glow hidup */
      @keyframes glowPulse {
        0% {
          box-shadow:
            0 0 10px rgba(56, 189, 248, 0.3),
            0 0 20px rgba(168, 85, 247, 0.2);
        }

        50% {
          box-shadow:
            0 0 25px rgba(56, 189, 248, 0.7),
            0 0 50px rgba(168, 85, 247, 0.45);
        }

        100% {
          box-shadow:
            0 0 10px rgba(56, 189, 248, 0.3),
            0 0 20px rgba(168, 85, 247, 0.2);
        }
      }

      /* ✨ kilau bergerak */
      @keyframes shine {
        0% {
          transform: translateX(-120%) rotate(12deg);
        }

        100% {
          transform: translateX(120%) rotate(12deg);
        }
      }

      /* 📘 PANEL */
      #panel {
        width: 94%;
        max-width: 1200px;

        margin: 10px auto;

        padding: 18px;

        overflow: visible;

        background: rgba(10, 15, 28, 0.88);

        border-radius: 16px;

        border: 1px solid rgba(255, 255, 255, 0.06);

        text-align: left; /* 🔥 semua teks rata kiri */

        backdrop-filter: blur(6px);

        box-shadow: 0 0 20px rgba(0, 0, 0, 0.35);
      }

      #panel h2,
      #panel p {
        text-align: left;
      }

      #panel p {
        margin-left: 10px;
      }

      /* ✨ garis cahaya step */
      #stepText::before {
        content: "";

        position: absolute;

        top: 0;
        left: 0;

        width: 100%;
        height: 2px;

        background: linear-gradient(90deg, transparent, #38bdf8, transparent);

        border-radius: 20px;
      }

      #panel h2 {
        margin: 0;
        font-size: 16px;
        color: #38bdf8;
      }

      #panel p {
        font-size: 12px;
        line-height: 1.4;
        opacity: 0.9;
      }

      /* 🎨 LEGEND */
      #legend {
        display: flex;
        flex-wrap: wrap;
        gap: 6px;
        margin-top: 10px;
        font-size: 11px;
      }

      .legend-item {
        display: flex;
        align-items: center;
        gap: 6px;
        background: #1e293b;
        padding: 6px 8px;
        border-radius: 8px;
      }

      .color-box {
        width: 12px;
        height: 12px;
        border-radius: 3px;
      }

      /* COLORS */
      .c-normal {
        background: #38bdf8;
      }
      .c-pivot {
        background: #f59e0b;
      }
      .c-active {
        background: #ef4444;
      }
      .c-sorted {
        background: #22c55e;
      }

      #stepText {
        position: relative;

        margin-top: 12px;
        margin-bottom: -2px;

        padding: 10px 12px;

        background: rgba(8, 15, 30, 0.95);

        border-radius: 14px;

        border: 1px solid rgba(56, 189, 248, 0.25);

        font-size: 12px;
        color: #fbbf24;

        backdrop-filter: blur(8px);

        box-shadow:
          0 0 18px rgba(56, 189, 248, 0.18),
          inset 0 0 10px rgba(255, 255, 255, 0.03);

        z-index: 5;
      }

      /* 📊 CHART */
      #container {
        position: relative;
        width: 94%;
        max-width: 1200px;

        height: clamp(260px, 60vh, 500px);

        /* 🔥 jarak chart dinaikkan lebih dekat */
        margin: 0px auto 6px;

        touch-action: manipulation;
      }

      .bar {
        position: absolute;
        bottom: 0;
        width: 2.5vw;
        min-width: 14px;
        max-width: 40px;
        border-radius: 6px 6px 0 0;
        background: #38bdf8;
        display: flex;
        justify-content: center;
        align-items: flex-end;
        font-size: 10px;
        color: white;
        transition:
          transform 0.45s ease,
          background 0.2s ease;
        will-change: transform;
      }

      .compare {
        background: #94a3b8 !important;
        filter: brightness(1.2);
      }

      .pivot {
        background: #f59e0b !important;
      }
      .active {
        background: #ef4444 !important;
      }
      .sorted {
        background: #22c55e !important;
      }

      /* BUTTON */
      #controls {
        width: 94%;
        max-width: 1200px;
        margin: 6px auto 10px;
        display: flex;
        flex-wrap: wrap;
        gap: 8px;
        justify-content: center;
      }

      button {
        flex: 1 1 42%;
        min-width: 120px;
        padding: 12px;
        border: none;
        border-radius: 10px;
        background: #334155;
        color: white;
        font-weight: bold;
        font-size: 14px;
      }

      button:active {
        transform: scale(0.97);
      }

      /* 👥 PANEL ANGGOTA */
      #memberPanel {
        margin-bottom: 18px;

        padding: 14px;

        background: rgba(15, 23, 42, 0.9);

        border-radius: 14px;

        border: 1px solid rgba(255, 255, 255, 0.08);

        box-shadow:
          0 0 14px rgba(56, 189, 248, 0.15),
          inset 0 0 8px rgba(255, 255, 255, 0.03);
      }

      #memberPanel h2 {
        margin: 0 0 10px;

        font-size: 15px;

        color: #38bdf8;

        text-align: left;
      }

      #memberPanel ul {
        margin: 0;

        padding-left: 20px;

        font-size: 12px;

        line-height: 1.8;

        color: #e2e8f0;
      }

      #memberPanel li {
        margin-bottom: 6px;
      }

      /* © FOOTER */
      #footer {
        width: 94%;
        max-width: 1200px;

        margin: 10px auto 25px;

        padding: 16px 12px;

        text-align: center;

        background: rgba(15, 23, 42, 0.88);

        border-radius: 14px;

        border: 1px solid rgba(255, 255, 255, 0.08);

        backdrop-filter: blur(6px);

        box-shadow:
          0 0 14px rgba(56, 189, 248, 0.12),
          inset 0 0 8px rgba(255, 255, 255, 0.03);
      }

      #footer p {
        margin: 6px 0;

        font-size: 12px;

        color: #cbd5e1;

        letter-spacing: 0.5px;
      }

      #footer p:last-child {
        color: #38bdf8;

        font-weight: bold;

        text-shadow: 0 0 8px rgba(56, 189, 248, 0.4);
      }
    </style>
  </head>

  <body>
    <h1 class="game-title">🎮 QUICK SORT LEGEND GAME 🎮</h1>

    <p class="intro-text">
      Selamat datang di Quick Sort Legend Game! Di sini kamu bisa belajar
      algoritma quick sort dengan cara yang seru dan interaktif. Tekan tombol
      Shuffle untuk mengacak data, lalu gunakan Play untuk melihat proses
      pengurutan secara otomatis, atau gunakan Prev/Next untuk menjelajahi
      setiap langkahnya. Nikmati pengalaman belajar yang menyenangkan!
    </p>

    <!-- 📘 PANEL -->
    <div id="panel">
      <!-- 👥 ANGGOTA KELOMPOK -->
      <div id="memberPanel">
        <h2>👥 Anggota Kelompok 2</h2>

        <p>
          <b>1. Syahzeinnur Hafidz (310125023915)</b><br />
          <b>2. Muhammad Raffi Aditya (310125023919)</b><br />
          <b>3. Muhammad Taufik Rahman (310125023931)</b>
        </p>
      </div>
      <h2>Quick Sort</h2>

      <p>
        Quick sort adalah algoritma pengurutan data yang sangat cepat dan
        efisien dengan membagi data menjadi dua bagian (partisi) menggunakan
        elemen acuan yang disebut pivot. Algoritma ini menggunakan metode divide
        and conquer untuk mengurutkan data skala kecil hingga besar.
      </p>

      <p>
        <b>Cara Kerja Quick Sort:</b><br />
        1. Pemilihan Pivot : Pilih satu elemen dari dalam data sebagai pivot
        (bisa elemen pertama, tengah, atau akhir).<br />
        2. Partisi : Pindahkan semua elemen yang lebih kecil dari pivot ke
        sebelah kiri, dan elemen yang lebih besar ke sebelah kanan pivot.<br />
        3. Rekursif : Lakukan proses langkah 1 dan 2 secara berulang untuk
        bagian data di sebelah kiri dan kanan pivot hingga semua data
        terurut.<br />
      </p>

      <!-- 🎨 LEGEND -->
      <div id="legend">
        <div class="legend-item">
          <div class="color-box c-normal"></div>
          Data normal
        </div>
        <div class="legend-item">
          <div class="color-box c-pivot"></div>
          Pivot
        </div>
        <div class="legend-item">
          <div class="color-box c-active"></div>
          Swap
        </div>
        <div class="legend-item">
          <div class="color-box c-sorted"></div>
          Posisi final
        </div>
        <div class="legend-item">
          <div class="color-box" style="background: #94a3b8"></div>
          Sedang dibandingkan dengan pivot
        </div>
      </div>

      <div id="stepText">Tekan Shuffle untuk mulai ulang</div>
    </div>

    <!-- 📊 CHART -->
    <div id="container"></div>

    <!-- 🎮 CONTROLS -->
    <div id="controls">
      <button onclick="togglePlay()">▶ Play</button>
      <button onclick="stopPlay()">⛔ Stop</button>
      <button onclick="prevStep()">⏮ Prev</button>
      <button onclick="nextStep()">⏭ Next</button>
      <button onclick="shuffle()">🔀 Shuffle</button>
    </div>

    <!-- 📘 KELEBIHAN QUICK SORT -->
    <div id="advantagePanel">
      <h2>Kelebihan Quick Sort</h2>

      <ul>
        <li>
          ⚡ <b>Sangat Cepat</b> — rata-rata memiliki kompleksitas waktu O(n log
          n), sehingga lebih efisien dibanding banyak algoritma sorting lain.
        </li>

        <li>
          📦 <b>Efisien untuk Data Besar</b> — sangat cocok digunakan untuk
          dataset berukuran besar karena performanya stabil dalam praktik.
        </li>

        <li>
          🧠 <b>Metode Divide and Conquer</b> — membagi masalah menjadi bagian
          kecil sehingga lebih mudah diproses.
        </li>

        <li>
          🔄 <b>Sorting di Tempat (In-place)</b> — tidak membutuhkan banyak
          memori tambahan.
        </li>

        <li>
          🚀 <b>Praktis di Dunia Nyata</b> — sering digunakan dalam sistem
          database, engine pencarian, dan library standar pemrograman.
        </li>

        <li>
          🎯 <b>Performa Rata-rata Sangat Baik</b> — meskipun ada kasus
          terburuk, secara umum tetap lebih cepat dibanding Merge Sort atau
          Bubble Sort.
        </li>
      </ul>
    </div>
    <!-- © FOOTER -->
    <div id="footer">
      <p>© 2026 Quick Sort Legend Game — All Rights Reserved</p>
      <p>Created with ❤️ by Group-2</p>
    </div>
    <script>
      function stopPlay() {
        playing = false;

        if (intervalId) {
          clearInterval(intervalId);
          intervalId = null;
        }
      }
      let array = [];
      let steps = [];
      let stepIndex = 0;
      let playing = false;
      let intervalId = null; // ✅ FIX STOP BUTTON

      /* 🔄 INIT */
      function init() {
        // 🔥 buat pool angka unik
        let pool = Array.from({ length: 80 }, (_, i) => i + 10);
        // angka 10–89 (cukup besar & unik)

        // 🔀 shuffle pool dulu
        pool.sort(() => Math.random() - 0.5);

        // ambil 10 angka unik
        array = pool.slice(0, 10);

        steps = [];
        stepIndex = 0;

        quickSort([...array], 0, array.length - 1);

        draw(array);
      }

      /* 📊 DRAW */
      function draw(arr, hl = {}) {
        const c = document.getElementById("container");
        const w = c.clientWidth;
        const gap = w / arr.length;

        c.innerHTML = "";

        arr.forEach((v, i) => {
          let b = document.createElement("div");
          b.className = "bar";

          b.style.height = v * 2.8 + "px";
          b.style.width = gap - 4 + "px";
          b.style.transform = `translateX(${i * gap}px)`;
          b.textContent = v;

          if (hl.pivot === i) b.classList.add("pivot");
          if (hl.active?.includes(i)) b.classList.add("active");
          if (hl.sorted?.includes(i)) b.classList.add("sorted");
          if (hl.compare?.includes(i)) b.classList.add("compare");

          c.appendChild(b);
        });
      }

      /* 🧠 RECORD STEP */
      function record(arr, hl, text) {
        steps.push({ arr: [...arr], hl, text });
      }

      /* QUICK SORT */
      function quickSort(arr, l, r) {
        if (l < r) {
          let p = partition(arr, l, r);
          quickSort(arr, l, p - 1);
          quickSort(arr, p + 1, r);
        }
      }

      /* SAFE SWAP */
      function safeSwap(arr, i, j) {
        if (i === j) return false;
        if (arr[i] === arr[j]) return false;

        [arr[i], arr[j]] = [arr[j], arr[i]];
        return true;
      }

      /* PARTITION */
      function partition(arr, l, r) {
        let pivot = arr[r];
        let i = l - 1;

        record(arr, { pivot: r }, `Pivot = ${pivot}`);

        for (let j = l; j < r; j++) {
          record(
            arr,
            { pivot: r, compare: [j] },
            `Bandingkan ${arr[j]} dengan pivot ${pivot}`,
          );
          if (arr[j] < pivot) {
            i++;

            let swapped = safeSwap(arr, i, j);

            if (swapped) {
              record(
                arr,
                { pivot: r, active: [i, j] },
                `Swap ${arr[i]} ↔ ${arr[j]}`,
              );
            } else {
              record(arr, { pivot: r, active: [j] }, `Tidak swap (nilai sama)`);
            }
          }
        }

        safeSwap(arr, i + 1, r);

        record(
          arr,
          { sorted: [i + 1], pivot: i + 1 },
          `Pivot ${pivot} selesai`,
        );

        return i + 1;
      }

      /* SHOW STEP */
      function show() {
        if (!steps.length) return;

        let s = steps[stepIndex];

        document.getElementById("stepText").textContent = s.text;

        animate(s.arr, s.hl);
      }

      /* ANIMATE */
      function animate(arr, hl) {
        const c = document.getElementById("container");
        const bars = [...c.children];

        const w = c.clientWidth;
        const gap = w / arr.length;

        arr.forEach((v, i) => {
          let b = bars.find((x) => parseInt(x.textContent) == v);

          if (b) {
            b.style.transform = `translateX(${i * gap}px)`;

            b.className = "bar";

            if (hl.pivot === i) b.classList.add("pivot");
            if (hl.active?.includes(i)) b.classList.add("active");
            if (hl.sorted?.includes(i)) b.classList.add("sorted");
            if (hl.compare?.includes(i)) b.classList.add("compare");
          }
        });

        setTimeout(() => draw(arr, hl), 400);
      }

      function partition(arr, l, r) {
        let pivot = arr[r];
        let i = l - 1;

        // pivot hanya info
        record(arr, { pivot: r }, `Pivot dipilih = ${pivot}`);

        for (let j = l; j < r; j++) {
          // 🔥 COMPARE = HANYA TEKS (NO ACTIVE ANIMATION)
          record(
            arr,
            { pivot: r, compare: [j] },
            `Bandingkan ${arr[j]} dengan pivot ${pivot}`,
          );

          if (arr[j] < pivot) {
            i++;

            let swapped = safeSwap(arr, i, j);

            if (swapped) {
              // 🔥 SWAP = BARU ANIMASI
              record(
                arr,
                { pivot: r, active: [i, j] },
                `Swap ${arr[i]} ↔ ${arr[j]}`,
              );
            }
          }
        }

        safeSwap(arr, i + 1, r);

        record(
          arr,
          { sorted: [i + 1], pivot: i + 1 },
          `Pivot ${pivot} selesai`,
        );

        return i + 1;
      }

      /* ▶ CONTROLS */
      function nextStep() {
        if (stepIndex < steps.length - 1) {
          stepIndex++;
          show();
        }
      }

      function prevStep() {
        if (stepIndex > 0) {
          stepIndex--;
          show();
        }
      }

      function togglePlay() {
        if (playing) return;

        playing = true;

        intervalId = setInterval(() => {
          if (stepIndex < steps.length - 1) {
            nextStep();
          } else {
            clearInterval(intervalId);
            intervalId = null;
            playing = false;
          }
        }, 650);
      }

      /* 🔄 SHUFFLE FIX (RESET TOTAL) */
      function shuffle() {
        array = [];
        steps = [];
        stepIndex = 0;
        playing = false;

        init();

        document.getElementById("stepText").textContent =
          "Data diacak ulang. Tekan Play untuk mulai";
      }
    </script>
  </body>
</html>
