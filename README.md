<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pabbicarang Lontara Makassar</title>
    <style>
        body { font-family: sans-serif; text-align: center; background: #fdfdfd; margin: 0; padding: 20px; }
        h1 { color: #b71c1c; margin-bottom: 5px; }
        .subtitle { color: #666; margin-bottom: 30px; }
        
        /* Kontrol Vokal */
        .vokal-control { margin-bottom: 30px; sticky; top: 10px; background: white; padding: 10px; border-radius: 50px; display: inline-block; box-shadow: 0 4px 10px rgba(0,0,0,0.1); }
        .vokal-btn { border: none; background: #eee; padding: 10px 20px; margin: 0 5px; border-radius: 25px; cursor: pointer; font-weight: bold; transition: 0.3s; }
        .vokal-btn.active { background: #b71c1c; color: white; }

        /* Grid Huruf */
        .grid-container { display: grid; grid-template-columns: repeat(auto-fill, minmax(110px, 1fr)); gap: 15px; max-width: 900px; margin: 0 auto; }
        .huruf-card { background: white; padding: 20px; border-radius: 15px; border: 1px solid #eee; transition: 0.3s; }
        .aksara { font-size: 50px; display: block; margin-bottom: 10px; color: #333; }
        .latin { font-size: 18px; color: #888; text-transform: capitalize; }
    </style>
</head>
<body>

    <h1>ᨒᨚᨈᨑ Lontara</h1>
    <p class="subtitle">Aplikasi Belajar Aksara Makassar</p>

    <div class="vokal-control">
        <button class="vokal-btn active" onclick="ubahVokal('', 'a')">a</button>
        <button class="vokal-btn" onclick="ubahVokal('ᨗ', 'i')">i</button>
        <button class="vokal-btn" onclick="ubahVokal('ᨘ', 'u')">u</button>
        <button class="vokal-btn" onclick="ubahVokal('ᨙ', 'e')">e</button>
        <button class="vokal-btn" onclick="ubahVokal('ᨚ', 'o')">o</button>
    </div>

    <div class="grid-container" id="lontaraGrid">
        </div>

    <script>
        // Data dasar Lontara
        const daftarHuruf = [
            {dasar: 'ᨀ', latin: 'ka'}, {dasar: 'ᨁ', latin: 'ga'}, {dasar: 'ᨂ', latin: 'nga'}, {dasar: 'ᨃ', latin: 'ngka'},
            {dasar: 'ᨄ', latin: 'pa'}, {dasar: 'ᨅ', latin: 'ba'}, {dasar: 'ᨆ', latin: 'ma'}, {dasar: 'ᨇ', latin: 'mpa'},
            {dasar: 'ᨈ', latin: 'ta'}, {dasar: 'ᨉ', latin: 'da'}, {dasar: 'ᨊ', latin: 'na'}, {dasar: 'ᨋ', latin: 'nra'},
            {dasar: 'ᨌ', latin: 'ca'}, {dasar: 'ᨍ', latin: 'ja'}, {dasar: 'ᨎ', latin: 'nya'}, {dasar: 'ᨏ', latin: 'nyca'}
        ];

        function ubahVokal(tanda, vokal) {
            const grid = document.getElementById('lontaraGrid');
            grid.innerHTML = ''; // Bersihkan layar

            daftarHuruf.forEach(item => {
                // Ganti huruf vokal di tulisan latin (misal: 'ka' jadi 'ki')
                let latinBaru = item.latin.replace('a', vokal);
                
                grid.innerHTML += `
                    <div class="huruf-card">
                        <span class="aksara">${item.dasar}${tanda}</span>
                        <span class="latin">${latinBaru}</span>
                    </div>
                `;
            });

            // Efek tombol aktif
            document.querySelectorAll('.vokal-btn').forEach(btn => {
                btn.classList.remove('active');
                if(btn.innerText === vokal) btn.classList.add('active');
            });
        }

        // Jalankan pertama kali
        ubahVokal('', 'a');
    </script>
</body>
</html>
