<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Три Кота: Кликер</title>
    <style>
        body { background: #5d4037; color: white; text-align: center; font-family: sans-serif; margin: 0; padding-bottom: 70px; }
        .header { background: #ff9900; padding: 15px; font-size: 26px; font-weight: bold; border-bottom: 4px solid #333; position: sticky; top: 0; }
        .tab { display: none; padding: 15px; }
        .active { display: block; }
        #target { 
            width: 180px; height: 180px; background: white; border: 8px solid #333; 
            border-radius: 50%; margin: 30px auto; display: flex; align-items: center; 
            justify-content: center; font-size: 80px; cursor: pointer; box-shadow: 0 8px 0 #222;
        }
        #target:active { transform: translateY(4px); box-shadow: 0 4px 0 #222; }
        .grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
        .card { background: #4e342e; border: 3px solid #333; border-radius: 12px; padding: 10px; }
        .rare { background: #2ecc71; } .epic { background: #9b59b6; } .leg { background: #f1c40f; }
        .btn { width: 100%; border: none; padding: 10px; border-radius: 8px; font-weight: bold; margin-top: 5px; cursor: pointer; background: #2196f3; color: white; }
        .owned { background: #ff9800; }
        .nav { position: fixed; bottom: 0; width: 100%; display: flex; background: #222; height: 65px; border-top: 3px solid #ff9900; }
        .n-btn { flex: 1; border: none; background: none; color: #aaa; font-weight: bold; }
        .n-btn.act { color: #fff200; font-size: 16px; }
    </style>
</head>
<body>
    <div class="header">💰 <span id="c">0</span></div>

    <div id="pg1" class="tab active">
        <h2 id="cn">Коржик</h2>
        <div id="target" onclick="h()">🐱</div>
        <p>КЛИК: +<span id="p">1</span></p>
        <div id="tm" style="color:#ff5252; font-weight:bold"></div>
    </div>

    <div id="pg2" class="tab">
        <h2 style="color:#fff200">БОЙЦЫ</h2>
        <div class="grid">
            <div class="card rare">🎀<br>Карамелька<button class="btn" id="b-🎀" onclick="buy('🎀','Карамелька',200)">200</button></div>
            <div class="card rare">🎩<br>Компот<button class="btn" id="b-🎩" onclick="buy('🎩','Компот',800)">800</button></div>
            <div class="card epic">🐈<br>Папа<button class="btn" id="b-🐈" onclick="buy('🐈','Папа',3000)">3к</button></div>
            <div class="card leg">🖤<br>Сажик<button class="btn" id="b-🖤" onclick="buy('🖤','Сажик',20000)">20к</button></div>
        </div>
    </div>

    <div id="pg3" class="tab">
        <h2 style="color:#ff9900">БАФФЫ</h2>
        <div class="card" style="margin-bottom:10px">🧺 Печенье (+1)<button class="btn" onclick="up()">50</button></div>
        <div class="card">🤖 Автоклик (5м)<button class="btn" onclick="auto()">5000</button></div>
    </div>

    <div class="nav">
        <button class="n-btn act" onclick="tab('pg1',this)">ИГРА</button>
        <button class="n-btn" onclick="tab('pg2',this)">ГЕРОИ</button>
        <button class="n-btn" onclick="tab('pg3',this)">БАФФЫ</button>
    </div>

    <script>
        let c = parseFloat(localStorage.getItem('c')) || 0;
        let p = parseInt(localStorage.getItem('p')) || 1;
        let owned = JSON.parse(localStorage.getItem('o')) || ['🐱'];
        let curI = localStorage.getItem('i') || '🐱', curN = localStorage.getItem('n') || 'Коржик';

        function h() { c += p; u(); }
        function tab(id, b) {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.n-btn').forEach(n => n.classList.remove('act'));
            document.getElementById(id).classList.add('active'); b.classList.add('act');
        }
        function buy(i, n, cost) {
            if(owned.includes(i)) { curI=i; curN=n; tab('pg1',document.querySelector('.n-btn')); }
            else if(c >= cost) { c-=cost; owned.push(i); curI=i; curN=n; } u();
        }
        function up() { if(c>=50) { c-=50; p++; u(); } }
        function auto() {
            if(c>=5000) { c-=5000; let t=300; 
                let iv=setInterval(()=>{ c+=p; t--; document.getElementById('tm').innerText="⚡ АВТО: "+t+"с"; u(); if(t<=0){clearInterval(iv); document.getElementById('tm').innerText=""}},1000);
            }
        }
        function u() {
            document.getElementById('c').innerText = Math.floor(c);
            document.getElementById('p').innerText = p;
            document.getElementById('target').innerText = curI;
            document.getElementById('cn').innerText = curN;
            owned.forEach(x => { let b=document.getElementById('b-'+x); if(b) { b.innerText="ВЫБРАТЬ"; b.classList.add('owned'); }});
            localStorage.setItem('c', c); localStorage.setItem('p', p);
            localStorage.setItem('o', JSON.stringify(owned));
            localStorage.setItem('i', curI); localStorage.setItem('n', curN);
        }
        u();
    </script>
</body>
</html>
