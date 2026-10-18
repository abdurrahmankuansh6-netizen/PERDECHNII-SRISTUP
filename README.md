  1  <!DOCTYPE html>
  2  <html lang="ru">
  3  <head>
  4  <meta charset="utf-8">
  5  <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
  6  <title>ПЕРДЕЦНЫЙ СРИСТУП — меню и заказ</title>
  7  <style>
  8  :root{--bg:#fff;--card:#fff;--text:#111;--muted:#555;--accent:#d90f1e;--line:#111;--head:#111;--headtext:#fff;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
  9  @media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#0b0b0b;--card:#161616;--text:#fff;--muted:#cfcfcf;--accent:#ff2a38;--line:#fff;--head:#d90f1e;--headtext:#fff}}
 10  :root[data-theme="dark"]{--bg:#0b0b0b;--card:#161616;--text:#fff;--muted:#cfcfcf;--accent:#ff2a38;--line:#fff;--head:#d90f1e;--headtext:#fff}
 11  *{box-sizing:border-box}
 12  body{margin:0;background:var(--bg);color:var(--text);font-family:Arial,Helvetica,sans-serif;font-size:20px}
 13  header{padding:36px 20px 28px;text-align:center;background:var(--head);color:var(--headtext);border-bottom:6px solid var(--accent)}
 14  h1{margin:0;font-size:clamp(34px,8vw,60px);letter-spacing:.04em;font-weight:900}
 15  header p{margin:10px 0 0;font-size:clamp(20px,4vw,26px)}
 16  nav{display:flex;gap:10px;overflow-x:auto;padding:16px;position:sticky;top:0;background:var(--bg);z-index:5;border-bottom:2px solid var(--line)}
 17  nav button{border:3px solid var(--line);background:var(--card);color:var(--text);padding:12px 22px;border-radius:30px;cursor:pointer;white-space:nowrap;font-size:20px;font-weight:700}
 18  nav button.on{background:var(--accent);color:#fff;border-color:var(--accent)}
 19  main{max-width:860px;margin:0 auto;padding:8px 16px 140px}
 20  .item{display:flex;justify-content:space-between;align-items:center;gap:16px;background:var(--card);border:3px solid var(--line);border-radius:18px;padding:18px 20px;margin:14px 0}
 21  .item h3{margin:0 0 6px;font-size:26px}
 22  .item small{color:var(--muted);font-size:19px;line-height:1.35;display:block}
 23  .price{font-weight:900;font-size:24px;margin-top:10px;color:var(--accent)}
 24  .ctl{display:flex;align-items:center;gap:12px;font-size:24px;font-weight:700}
 25  .ctl button{width:48px;height:48px;border-radius:50%;border:3px solid var(--accent);background:transparent;color:var(--accent);font-size:28px;font-weight:700;cursor:pointer}
 26  .ctl button.add{width:auto;border-radius:28px;padding:0 22px;font-size:20px;background:var(--accent);color:#fff;height:50px}
 27  @media (max-width:560px){.item{flex-direction:column;align-items:flex-start}}
 28  #bar{position:fixed;left:0;right:0;bottom:0;padding:14px 16px calc(14px + env(safe-area-inset-bottom,0px));background:var(--bg);border-top:3px solid var(--line);display:none;justify-content:center}
 29  #bar button{width:100%;max-width:828px;padding:18px;border:0;border-radius:16px;background:var(--accent);color:#fff;font-size:24px;font-weight:800;cursor:pointer}
 30  #modal{position:fixed;inset:0;background:rgba(0,0,0,.65);display:none;align-items:flex-end;justify-content:center;z-index:10}
 31  #modal .box{background:var(--bg);color:var(--text);width:100%;max-width:640px;max-height:92%;overflow:auto;border-radius:24px 24px 0 0;padding:24px;border-top:6px solid var(--accent)}
 32  .row{display:flex;justify-content:space-between;gap:12px;padding:10px 0;border-bottom:2px solid var(--line);font-size:22px}
 33  input,textarea{width:100%;margin:8px 0;padding:16px;border:3px solid var(--line);border-radius:12px;background:var(--card);color:var(--text);font-size:21px;font-family:inherit}
 34  .total{font-weight:900;font-size:28px;margin:16px 0;color:var(--accent)}
 35  .sec{border:0;background:none;color:var(--text);width:100%;padding:14px;cursor:pointer;font-size:20px;font-weight:700}
 36  .sec.main{background:var(--accent);color:#fff;border-radius:14px;font-size:24px}
 37  #done{display:none;text-align:center;padding:24px 0;font-size:22px}
 38  h2{font-size:32px;margin:0 0 12px}
 39  </style>
 40  </head>
 41  <body>
 42  <header>
 43  <h1>ПЕРДЕЦНЫЙ СРИСТУП</h1>
 44  <p>Выберите блюда и оформите заказ онлайн</p>
 45  </header>
 46  <nav id="tabs"></nav>
 47  <main id="list"></main>
 48  <div id="bar"><button id="open"></button></div>
 49  <div id="modal"><div class="box">
 50  <div id="form">
 51  <h2>Ваш заказ</h2>
 52  <div id="lines"></div>
 53  <div class="total" id="total"></div>
 54  <input id="nm" placeholder="Имя">
 55  <input id="ph" type="tel" placeholder="Телефон">
 56  <input id="ad" placeholder="Адрес доставки (или «самовывоз»)">
 57  <textarea id="cm" rows="2" placeholder="Комментарий"></textarea>
 58  <button class="sec main" id="send">Отправить заказ</button>
 59  <button class="sec" id="close">Назад к меню</button>
 60  </div>
 61  <div id="done"><h2>Спасибо!</h2><p>Заказ принят. Мы скоро свяжемся с вами.</p><button class="sec" id="fin">Закрыть</button></div>
 62  </div></div>
 63  <script>
 64  var MENU={
 65  "Завтраки":[["Омлет с сыром и зеленью",1100,"Три яйца, чеддер, свежая зелень, тост"],["Сырники со сметаной",1250,"Творожные сырники, сметана, ягодный соус"],["Овсяная каша с ягодами",950,"На молоке, мёд, свежие ягоды"],["Яйца бенедикт",1650,"Бекон, пашот, голландский соус, булочка бриошь"],["Круассан с ветчиной и сыром",1050,"Тёплый круассан, ветчина, моцарелла"]],
 66  "Закуски":[["Брускетта с томатами",950,"Хрустящий хлеб, томаты, базилик, оливковое масло"],["Сырная тарелка",2490,"Три вида сыра, мёд, орехи, виноград"],["Куриные крылья BBQ",1790,"Острый соус барбекю, сельдерей"],["Картофель фри с соусом",890,"Хрустящий картофель, сырный соус на выбор"],["Мясная нарезка",2990,"Ассорти из вяленых и копчёных деликатесов"],["Креветки в чесноке",2650,"Тигровые креветки, чеснок, белое вино, багет"]],
 67  "Салаты и супы":[["Салат цезарь с курицей",1590,"Романо, пармезан, гренки, соус цезарь"],["Греческий салат",1390,"Огурцы, томаты, фета, маслины"],["Салат с тунцом",1750,"Микс салата, тунец, яйцо, каперсы"],["Борщ со сметаной",1290,"Говядина, свёкла, чесночная пампушка"],["Крем-суп грибной",1190,"Шампиньоны, сливки, гренки"],["Том ям с креветками",2190,"Острый, кокосовое молоко, рис"]],
 68  "Горячее":[["Стейк рибай",5900,"Мраморная говядина, овощи гриль, перечный соус"],["Лосось на гриле",3490,"Овощи гриль, лимонное масло"],["Бефстроганов",2490,"Говядина в сливочном соусе, картофельное пюре"],["Куриная грудка с грибами",2190,"Сливочно-грибной соус, рис"],["Плов по-домашнему",1890,"Баранина, морковь, чеснок, зира"],["Бешбармак",2790,"Конина, лапша, лук-сорпа"],["Манты с мясом",1690,"Пять штук, сметана"]],
 69  "Паста и пицца":[["Паста карбонара",2090,"Бекон, желток, пармезан"],["Паста болоньезе",1990,"Мясной соус, пармезан"],["Паста с морепродуктами",2790,"Креветки, мидии, кальмары, томатный соус"],["Пицца Маргарита",2190,"Томаты, моцарелла, базилик"],["Пицца Пепперони",2590,"Пепперони, моцарелла, томатный соус"],["Пицца Четыре сыра",2690,"Моцарелла, горгонзола, пармезан, чеддер"]],
 70  "Бургеры":[["Бургер классический",1990,"Говяжья котлета, чеддер, салат, фри"],["Чизбургер двойной",2490,"Две котлеты, двойной сыр, соус"],["Бургер с курицей",1790,"Хрустящая курица, салат, соус"],["Острый бургер халапеньо",2190,"Говядина, халапеньо, острый соус, фри"]],
 71  "Десерты":[["Чизкейк Нью-Йорк",1290,"С ягодным соусом"],["Тирамису",1350,"Классический рецепт"],["Медовик",1090,"Нежные коржи, сметанный крем"],["Шоколадный фондан",1490,"Тёплый, с шариком мороженого"],["Мороженое три шарика",990,"Ваниль, шоколад, клубника"],["Блинчики с вареньем",1050,"Три блинчика, варенье или сгущёнка"]],
 72  "Кофе и чай":[["Эспрессо",650,"Двойная порция"],["Американо",750,"Чёрный кофе"],["Капучино",950,"Эспрессо и молочная пена"],["Латте",1050,"Нежный молочный кофе"],["Раф ванильный",1250,"Сливки, ванильный сироп"],["Чай чёрный в чайнике",850,"Классический, с лимоном"],["Чай зелёный в чайнике",850,"Жасминовый"],["Чай с облепихой",1150,"Облепиха, мёд, имбирь"],["Горячий шоколад",1100,"Густой, со взбитыми сливками"]],
 73  "Холодные напитки":[["Домашний лимонад",1250,"Лимон, мята, содовая"],["Морс ягодный",990,"Клюква, смородина"],["Свежевыжатый апельсин",1650,"Сок из свежих апельсинов"],["Айс латте",1250,"Холодный кофе с молоком и льдом"],["Молочный коктейль",1350,"Ваниль, шоколад или клубника"],["Кола, 0.33 л",650,"Классическая"],["Минеральная вода, 0.5 л",450,"Газированная или негазированная"],["Компот домашний",750,"Сухофрукты"]]
 74  };
 75  var cart={},cat=Object.keys(MENU)[0];
 76  function fmt(n){return n.toLocaleString("ru-RU")+" ₸"}
 77  function key(c,i){return c+"|"+i}
 78  function render(){
 79  var t=document.getElementById("tabs");t.innerHTML="";
 80  Object.keys(MENU).forEach(function(c){var b=document.createElement("button");b.textContent=c;if(c===cat)b.className="on";b.onclick=function(){cat=c;render();window.scrollTo(0,0)};t.appendChild(b)});
 81  var l=document.getElementById("list");l.innerHTML="";
 82  MENU[cat].forEach(function(it,i){
 83  var k=key(cat,i),q=cart[k]||0,d=document.createElement("div");d.className="item";
 84  d.innerHTML='<div><h3>'+it[0]+'</h3><small>'+it[2]+'</small><div class="price">'+fmt(it[1])+'</div></div><div class="ctl"></div>';
 85  var c=d.querySelector(".ctl");
 86  if(!q){var a=document.createElement("button");a.className="add";a.textContent="В корзину";a.onclick=function(){cart[k]=1;render()};c.appendChild(a)}
 87  else{var m=document.createElement("button");m.textContent="−";m.onclick=function(){cart[k]--;if(!cart[k])delete cart[k];render()};var s=document.createElement("span");s.textContent=q;var p=document.createElement("button");p.textContent="+";p.onclick=function(){cart[k]++;render()};c.append(m,s,p)}
 88  l.appendChild(d)});
 89  var n=0,sum=0;Object.keys(cart).forEach(function(k){var p=k.split("|"),it=MENU[p[0]][p[1]];n+=cart[k];sum+=cart[k]*it[1]});
 90  var bar=document.getElementById("bar");bar.style.display=n?"flex":"none";
 91  document.getElementById("open").textContent="Корзина · "+n+" · "+fmt(sum);
 92  window._sum=sum}
 93  document.getElementById("open").onclick=function(){
 94  var h="";Object.keys(cart).forEach(function(k){var p=k.split("|"),it=MENU[p[0]][p[1]];h+='<div class="row"><span>'+it[0]+' × '+cart[k]+'</span><span>'+fmt(it[1]*cart[k])+'</span></div>'});
 95  document.getElementById("lines").innerHTML=h;
 96  document.getElementById("total").textContent="Итого: "+fmt(window._sum);
 97  document.getElementById("form").style.display="block";document.getElementById("done").style.display="none";
 98  document.getElementById("modal").style.display="flex"};
 99  document.getElementById("close").onclick=function(){document.getElementById("modal").style.display="none"};
100  document.getElementById("send").onclick=function(){
101  if(!document.getElementById("nm").value||!document.getElementById("ph").value){alert("Укажите имя и телефон");return}
102  cart={};render();document.getElementById("form").style.display="none";document.getElementById("done").style.display="block"};
103  document.getElementById("fin").onclick=function(){document.getElementById("modal").style.display="none"};
104  render();
105  </script>
106  </body>
107  </html>
