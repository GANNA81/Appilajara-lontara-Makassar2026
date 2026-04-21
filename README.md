<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pabbicarang Lontara Pro</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; text-align: center; background: #fdfdfd; margin: 0; padding: 20px; }
        .container { max-width: 600px; margin: auto; background: white; padding: 25px; border-radius: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); }
        h1 { color: #b71c1c; margin-bottom: 5px; }
        input { width: 100%; padding: 15px; font-size: 18px; border: 2px solid #eee; border-radius: 12px; margin: 20px 0; box-sizing: border-box; outline: none; }
        input:focus { border-color: #b71c1c; }
        #hasilLontara { font-size: 70px; color: #b71c1c; margin: 20px 0; cursor: pointer; min-height: 80px; }
        .vokal-btn { border: none; background: #f0f0f0; padding: 12px 20px; margin: 5px; border-radius: 50px; cursor: pointer; font-weight: bold; }
        .vokal-btn.active { background: #b71c1c; color: white; }
        .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(90px, 1fr)); gap: 10px; margin-top: 30px; }
        .card { background: #fff; padding: 15px; border-radius: 15px; border: 1px solid #f0f0f0; cursor: pointer; transition: 0.2s; }
        .card:hover { transform: scale(1.05); background: #fff5f5; }
        .aksara { font-size: 35px; display: block; color: #333; }
        .latin { font-size: 14px; color: #999; text-transform: uppercase; }
        .info { font-size: 12px; color: #aaa; margin-top: 20px; }
    </style>
</head>
<body>

<div class="container">
    <h1>ᨒᨚᨈᨑ</h1>
    <p>Ketik & Klik untuk Mendengar Suara</p>
    
    <input type="text" id="inputLatin" placeholder="Ketik di sini..." oninput="transliterasi()">
    <div id="hasilLontara" onclick="bicaraLontara()"></div>

    <div id="vokalGroup">
        <button class="vokal-btn active" onclick="updateGrid('', 'a')">a</button>
        <button class="vokal-btn" onclick="updateGrid('ᨗ', 'i')">i</button>
        <button class="vokal-btn" onclick="updateGrid('ᨘ', 'u')">u</button>
        <button class="vokal-btn" onclick="updateGrid('ᨙ', 'e')">e</button>
        <button class="vokal-btn" onclick="updateGrid('ᨚ', 'o')">o</button>
    </div>

    <div class="grid" id="lontaraGrid"></div>
    
    <p class="info">Tips: Klik kartu huruf untuk mendengar suaranya.</p>
</div>

<script>
    const data = [
        {d: 'ᨀ', l: 'ka'}, {d: 'ᨁ', l: 'ga'}, {d: 'ᨂ', l: 'nga'}, {d: 'ᨃ', l: 'ngka'},
        {d: 'ᨄ', l: 'pa'}, {d: 'ᨅ', l: 'ba'}, {d: 'ᨆ', l: 'ma'}, {d: 'ᨇ', l: 'mpa'},
        {d: 'ᨈ', l: 'ta'}, {d: 'ᨉ', l: 'da'}, {d: 'ᨊ', l: 'na'}, {d: 'ᨋ', l: 'nra'},
        {d: 'ᨌ', l: 'ca'}, {d: 'ᨍ', l: 'ja'}, {d: 'ᨎ', l: 'nya'}, {d: 'ᨏ', l: 'nyca'},
        {d: 'ᨐ', l: 'ya'}, {d: 'ᨑ', l: 'ra'}, {d: 'ᨒ', l: 'la'}, {d: 'ᨓ', l: 'wa'}, 
        {d: 'ᨔ', l: 'sa'}, {d: 'ᨕ', l: 'a'}, {d: 'ᨖ', l: 'ha'}
    ];

    // FITUR SUARA
    function bicara(teks) {
        const suara = new SpeechSynthesisUtterance();
        suara.text = teks;
        suara.lang = 'id-ID'; // Menggunakan aksen Indonesia agar mirip
        window.speechSynthesis.speak(suara);
    }

    function bicaraLontara() {
        const teks = document.getElementById('inputLatin').value;
        if(teks) bicara(teks);
    }

    function transliterasi() {
        let teks = document.getElementById('inputLatin').value.toLowerCase();
        let hasil = "";
        let i = 0;
        while (i < teks.length) {
            let found = false;
            for (let len = 3; len >= 2; len--) {
                let sub = teks.substring(i, i + len);
                let match = data.find(item => item.l === sub);
                if (match) { hasil += match.d; i += len; found = true; break; }
            }
            if (!found) { 
                if(teks[i] === 'a') hasil += 'ᨕ';
                else hasil += teks[i]; 
                i++; 
            }
        }
        document.getElementById('hasilLontara').innerText = hasil;
    }

    function updateGrid(tanda, v) {
        const grid = document.getElementById('lontaraGrid');
        grid.innerHTML = data.map(item => {
            const bunyi = item.l.replace('a', v);
            return `
                <div class="card" onclick="bicara('${bunyi}')">
                    <span class="aksara">${item.d}${tanda}</span>
                    <span class="latin">${bunyi}</span>
                </div>
            `;
        }).join('');
        
        document.querySelectorAll('.vokal-btn').forEach(b => b.classList.remove('active'));
        if(event) event.target.classList.add('active');
    }

    updateGrid('', 'a');
</script>

</body>
</html>
