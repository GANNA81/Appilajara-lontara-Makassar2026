<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lontara Makassar Digital</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; text-align: center; background: #f8f9fa; margin: 0; padding: 20px; color: #333; }
        .container { max-width: 800px; margin: auto; background: white; padding: 20px; border-radius: 20px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); }
        h1 { color: #b71c1c; margin-bottom: 10px; }
        
        /* Input Section */
        input { width: 90%; padding: 15px; font-size: 18px; border: 2px solid #ddd; border-radius: 10px; margin-bottom: 10px; outline: none; transition: 0.3s; }
        input:focus { border-color: #b71c1c; }
        #hasilLontara { font-size: 60px; color: #b71c1c; min-height: 80px; margin: 10px 0; word-wrap: break-word; }

        /* Vokal Control */
        .vokal-btn { border: none; background: #eee; padding: 10px 18px; margin: 5px; border-radius: 20px; cursor: pointer; font-weight: bold; }
        .vokal-btn.active { background: #b71c1c; color: white; }

        /* Grid */
        .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(100px, 1fr)); gap: 15px; margin-top: 30px; }
        .card { background: #fff; padding: 15px; border-radius: 12px; border: 1px solid #eee; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
        .aksara { font-size: 40px; display: block; color: #222; }
        .latin { font-size: 16px; color: #888; }
    </style>
</head>
<body>

<div class="container">
    <h1>ᨒᨚᨈᨑ ᨆᨀᨔᨑ</h1>
    <p>Ketik Latin ke Lontara:</p>
    
    <input type="text" id="inputLatin" placeholder="Contoh: makasara" oninput="transliterasi()">
    <div id="hasilLontara"></div>

    <hr>

    <p>Daftar Huruf & Vokal:</p>
    <div id="vokalGroup">
        <button class="vokal-btn active" onclick="updateGrid('', 'a')">a</button>
        <button class="vokal-btn" onclick="updateGrid('ᨗ', 'i')">i</button>
        <button class="vokal-btn" onclick="updateGrid('ᨘ', 'u')">u</button>
        <button class="vokal-btn" onclick="updateGrid('ᨙ', 'e')">e</button>
        <button class="vokal-btn" onclick="updateGrid('ᨚ', 'o')">o</button>
    </div>

    <div class="grid" id="lontaraGrid"></div>
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

    // Fungsi Ketik ke Lontara
    function transliterasi() {
        let teks = document.getElementById('inputLatin').value.toLowerCase();
        let hasil = "";
        let i = 0;
        while (i < teks.length) {
            let found = false;
            // Cek 3 atau 2 huruf (nga, ka, dll)
            for (let len = 3; len >= 2; len--) {
                let sub = teks.substring(i, i + len);
                let match = data.find(item => item.l === sub || (sub.length === 2 && item.l === sub));
                if (match) {
                    hasil += match.d; i += len; found = true; break;
                }
            }
            if (!found) { 
                if(teks[i] === 'a') hasil += 'ᨕ';
                else hasil += teks[i]; 
                i++; 
            }
        }
        document.getElementById('hasilLontara').innerText = hasil;
    }

    // Fungsi Update Tampilan Kartu
    function updateGrid(tanda, v) {
        const grid = document.getElementById('lontaraGrid');
        grid.innerHTML = data.map(item => `
            <div class="card">
                <span class="aksara">${item.d}${tanda}</span>
                <span class="latin">${item.l.replace('a', v)}</span>
            </div>
        `).join('');
        
        document.querySelectorAll('.vokal-btn').forEach(b => b.classList.remove('active'));
        event.target.classList.add('active');
    }

    updateGrid('', 'a'); // Inisialisasi awal
</script>

</body>
</html>
