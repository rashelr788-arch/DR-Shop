# DR-Shop
ওয়ার্ল্ড মার্কেটপ্লেস 
<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>DR SHOP</title>

<style>
*{box-sizing:border-box}
body{
 margin:0;
 font-family:Arial,sans-serif;
 background:#f4f2f0;
 color:#222;
}
header{
 background:#70251f;
 color:white;
 padding:16px;
}
.header{
 max-width:1100px;
 margin:auto;
 display:flex;
 justify-content:space-between;
 align-items:center;
 flex-wrap:wrap;
 gap:12px;
}
.logo{font-size:25px;font-weight:bold}
.tag{font-size:13px;margin-top:5px}
nav{display:flex;gap:6px;flex-wrap:wrap}
button{
 border:0;
 padding:10px 14px;
 border-radius:7px;
 background:#70251f;
 color:white;
 cursor:pointer;
}
nav button{background:#914139}
main{max-width:1100px;margin:20px auto;padding:0 12px}
.panel{
 background:white;
 padding:16px;
 border-radius:12px;
 margin-bottom:15px;
}
h2{color:#70251f}
input,textarea,select{
 width:100%;
 padding:11px;
 margin:6px 0 12px;
 border:1px solid #ccc;
 border-radius:7px;
}
.grid{
 display:grid;
 grid-template-columns:repeat(auto-fill,minmax(190px,1fr));
 gap:12px;
}
.product{
 background:white;
 border-radius:10px;
 overflow:hidden;
 border:1px solid #ddd;
}
.product img{
 width:100%;
 height:160px;
 object-fit:cover;
}
.product-info{padding:12px}
.price{font-weight:bold;color:#70251f}
.hidden{display:none!important}
table{width:100%;border-collapse:collapse;min-width:550px}
td,th{padding:10px;border-bottom:1px solid #ddd;text-align:left}
th{background:#f6eae5}
.table-wrap{overflow:auto}
.tabs{display:flex;gap:6px;flex-wrap:wrap}
.tabs button{background:#ddd;color:#222}
.tabs button.active{background:#70251f;color:white}
.stat{
 background:#fff6f1;
 padding:14px;
 border-radius:9px;
 border:1px solid #ead8cf;
}
.stat b{display:block;font-size:20px;color:#70251f;margin-top:7px}
.stats{
 display:grid;
 grid-template-columns:repeat(auto-fit,minmax(140px,1fr));
 gap:10px;
}
.green{background:#16794b}
.red{background:#b52d2d}
footer{text-align:center;padding:25px;color:#777}
</style>
</head>

<body>

<header>
 <div class="header">
  <div>
   <div class="logo">🛍️ DR SHOP</div>
   <div class="tag">বাংলাদেশের অনলাইন মার্কেটপ্লেস</div>
  </div>

  <nav>
   <button onclick="page('home')">হোম</button>
   <button onclick="page('cart')">কার্ট (<span id="count">0</span>)</button>
   <button onclick="page('seller')">Seller</button>
   <button onclick="page('admin')">Admin</button>
  </nav>
 </div>
</header>

<main>

<!-- HOME -->
<section id="home">
 <div class="panel">
  <h2>পণ্য খুঁজুন</h2>
  <input id="search" placeholder="পণ্যের নাম লিখুন..." oninput="showProducts()">
 </div>
 <div id="products" class="grid"></div>
</section>

<!-- CART -->
<section id="cart" class="hidden">
 <div class="panel">
  <h2>আমার কার্ট</h2>
  <div id="cartItems"></div>
  <h3 id="total"></h3>
 </div>

 <div class="panel">
  <h2>অর্ডার করুন</h2>
  <label>আপনার নাম</label>
  <input id="customer" placeholder="আপনার নাম">

  <label>মোবাইল নম্বর</label>
  <input id="phone" placeholder="01XXXXXXXXX">

  <label>সম্পূর্ণ ঠিকানা</label>
  <textarea id="address"></textarea>

  <label>ডেলিভারি</label>
  <select id="delivery">
   <option value="DR Shop">DR Shop Delivery</option>
   <option value="Seller">Seller Delivery</option>
  </select>

  <label>পেমেন্ট</label>
  <select id="payment">
   <option>Cash on Delivery</option>
   <option>Online Payment Demo</option>
  </select>

  <button class="green" onclick="checkout()">অর্ডার নিশ্চিত করুন</button>
 </div>
</section>

<!-- SELLER -->
<section id="seller" class="hidden">
 <div class="panel">
  <h2>Seller Panel</h2>

  <label>Seller নাম</label>
  <input id="sellerName" placeholder="দোকানের নাম">

  <label>পণ্যের নাম</label>
  <input id="productName" placeholder="পণ্যের নাম">

  <label>পণ্যের দাম</label>
  <input id="productPrice" type="number">

  <label>স্টক</label>
  <input id="productStock" type="number">

  <label>ছবির URL</label>
  <input id="productImage" placeholder="https://...">

  <label>বিবরণ</label>
  <textarea id="productDesc"></textarea>

  <button onclick="addProduct()">পণ্য যোগ করুন</button>
 </div>
</section>

<!-- ADMIN -->
<section id="admin" class="hidden">

 <div class="panel" id="login">
  <h2>Super Admin Login</h2>
  <input id="username" placeholder="Username" value="admin">
  <input id="password" type="password" placeholder="Password">
  <button onclick="login()">Login</button>
 </div>

 <div id="dashboard" class="hidden">

  <div class="panel">
   <h2>DR SHOP Super Admin</h2>
   <button onclick="logout()">Logout</button>
   <div class="stats" id="statistics"></div>
  </div>

  <div class="panel">
   <div class="tabs">
    <button class="active" onclick="tab('wallet',this)">Wallet</button>
    <button onclick="tab('orders',this)">Orders</button>
    <button onclick="tab('manage',this)">Products</button>
    <button onclick="tab('sellers',this)">Sellers</button>
    <button onclick="tab('settings',this)">Settings</button>
   </div>

   <!-- ADMIN WALLET -->
   <div id="wallet">
    <h2>Admin Wallet</h2>
    <div class="stats" id="walletStats"></div>

    <h3>টাকা উত্তোলন</h3>

    <label>পরিমাণ</label>
    <input id="withdrawAmount" type="number">

    <label>মাধ্যম</label>
    <select id="method" onchange="withdrawMethod()">
     <option>Bank</option>
     <option>bKash</option>
     <option>Nagad</option>
    </select>

    <div id="bankBox">
     <input id="bankName" placeholder="ব্যাংকের নাম">
     <input id="bankNumber" placeholder="ব্যাংক অ্যাকাউন্ট নম্বর">
    </div>

    <div id="mobileBox" class="hidden">
     <input id="mobileNumber" placeholder="01XXXXXXXXX">
    </div>

    <button class="green" onclick="withdraw()">সরাসরি টাকা উত্তোলন</button>

    <h3>উত্তোলনের ইতিহাস</h3>
    <div id="history"></div>
   </div>

   <!-- ORDERS -->
   <div id="orders" class="hidden">
    <h2>সব অর্ডার</h2>
    <div id="orderList"></div>
   </div>

   <!-- PRODUCTS -->
   <div id="manage" class="hidden">
    <h2>সব পণ্য</h2>
    <div id="productList"></div>
   </div>

   <!-- SELLERS -->
   <div id="sellers" class="hidden">
    <h2>Seller Management</h2>
    <div id="sellerList"></div>
   </div>

   <!-- SETTINGS -->
   <div id="settings" class="hidden">
    <h2>Marketplace Settings</h2>

    <label>Seller Commission (%)</label>
    <input id="commission" type="number" min="0" max="100">

    <label>Delivery Charge</label>
    <input id="deliveryCharge" type="number">

    <button onclick="saveSettings()">সেভ করুন</button>
   </div>

  </div>
 </div>
</section>

</main>

<footer>
 DR SHOP © 2026<br>
 বাংলাদেশের অনলাইন মার্কেটপ্লেস
</footer>

<script>
// DATABASE
function getData(){
 try{
  return JSON.parse(localStorage.getItem("DRSHOP_DB")) || null;
 }catch(e){return null}
}

let db=getData() || {
 products:[
  {id:1,name:"টি-শার্ট",price:450,stock:20,image:"https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?w=600",seller:"DR Shop",own:true},
  {id:2,name:"জুতা",price:1250,stock:12,image:"https://images.unsplash.com/photo-1542291026-7eec264c27ff?w=600",seller:"DR Shop",own:true},
  {id:3,name:"ঘড়ি",price:850,stock:15,image:"https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=600",seller:"DR Shop",own:true}
 ],
 orders:[],
 cart:[],
 withdrawals:[],
 rate:10,
 fee:60,
 nextId:4
};

function save(){
 localStorage.setItem("DRSHOP_DB",JSON.stringify(db));
}

function money(n){
 return "৳"+Number(n||0).toLocaleString("en-BD");
}

// PAGE NAVIGATION
function page(p){
 ["home","cart","seller","admin"].forEach(x=>{
  document.getElementById(x).classList.toggle("hidden",x!==p);
 });
 if(p==="cart")showCart();
 if(p==="admin")showAdmin();
 if(p==="seller")showSellerProducts();
}

// PRODUCTS
function showProducts(){
 let q=document.getElementById("search").value.toLowerCase();
 let list=db.products.filter(p=>p.active!==false && p.name.toLowerCase().includes(q));

 document.getElementById("products").innerHTML=list.map(p=>`
  <div class="product">
   <img src="${p.image}" onerror="this.src='https://placehold.co/500x300?text=DR+Shop'">
   <div class="product-info">
    <b>${p.name}</b>
    <p class="price">${money(p.price)}</p>
    <small>স্টক: ${p.stock}</small><br><br>
    <button onclick="addCart(${p.id})">কার্টে যোগ করুন</button>
   </div>
  </div>
 `).join("");
}

function addCart(id){
 let p=db.products.find(x=>x.id===id);
 if(!p||p.stock<1)return alert("স্টক নেই");
 let c=db.cart.find(x=>x.id===id);
 if(c)c.qty=Math.min(c.qty+1,p.stock);
 else db.cart.push({id,qty:1});
 save();
 updateCount();
 alert("কার্টে যোগ হয়েছে");
}

function updateCount(){
 document.getElementById("count").innerText=
 db.cart.reduce((s,x)=>s+x.qty,0);
}

// CART
function showCart(){
 let el=document.getElementById("cartItems");
 if(!db.cart.length){
  el.innerHTML="আপনার কার্ট খালি";
  document.getElementById("total").innerText="";
  return;
 }

 let total=0;
 el.innerHTML=db.cart.map(c=>{
  let p=db.products.find(x=>x.id===c.id);
  if(!p)return "";
  total+=p.price*c.qty;
  return `<p>${p.name} × ${c.qty} — ${money(p.price*c.qty)}
   <button onclick="qty(${p.id},-1)">−</button>
   <button onclick="qty(${p.id},1)">+</button>
   <button onclick="removeItem(${p.id})">বাদ</button>
  </p>`;
 }).join("");

 document.getElementById("total").innerText=
 "মোট: "+money(total+db.fee)+" (ডেলিভারি সহ)";
}

function qty(id,n){
 let c=db.cart.find(x=>x.id===id);
 let p=db.products.find(x=>x.id===id);
 if(!c||!p)return;
 c.qty=Math.max(1,Math.min(p.stock,c.qty+n));
 save();showCart();updateCount();
}

function removeItem(id){
 db.cart=db.cart.filter(x=>x.id!==id);
 save();showCart();updateCount();
}

// CHECKOUT
function checkout(){
 if(!db.cart.length)return alert("কার্ট খালি");

 let name=document.getElementById("customer").value.trim();
 let phone=document.getElementById("phone").value.trim();
 let address=document.getElementById("address").value.trim();

 if(!name||!/^01[0-9]{9}$/.test(phone)||!address)
  return alert("সঠিক নাম, ফোন ও ঠিকানা দিন");

 let items=[],total=0,commission=0,sellerDue=0;

 for(let c of db.cart){
  let p=db.products.find(x=>x.id===c.id);
  if(!p||p.stock<c.qty)return alert("স্টক পর্যাপ্ত নয়");
  let line=p.price*c.qty;
  let com=p.own?0:line*db.rate/100;
  items.push({id:p.id,name:p.name,qty:c.qty,price:p.price,
   seller:p.seller,own:!!p.own,line,commission:com});
  total+=line;commission+=com;sellerDue+=line-com;
  p.stock-=c.qty;
 }

 db.orders.unshift({
  id:"DR"+Date.now(),
  date:new Date().toLocaleString(),
  name,phone,address,items,total,
  grand:total+db.fee,
  commission,sellerDue,
  status:"নতুন",
  settled:false,
  delivery:document.getElementById("delivery").value,
  payment:document.getElementById("payment").value
 });

 db.cart=[];
 save();updateCount();showProducts();
 alert("অর্ডার সফল হয়েছে");
 page("home");
}

// SELLER
function addProduct(){
 let seller=document.getElementById("sellerName").value.trim();
 let name=document.getElementById("productName").value.trim();
 let price=Number(document.getElementById("productPrice").value);
 let stock=Number(document.getElementById("productStock").value);
 let image=document.getElementById("productImage").value.trim();

 if(!seller||!name||price<=0||stock<0)
  return alert("সব তথ্য সঠিকভাবে দিন");

 db.products.push({
  id:db.nextId++,name,price,stock,
  image:image||"https://placehold.co/500x300?text=DR+Shop",
  seller,own:false,active:true
 });

 save();showProducts();showSellerProducts();
 alert("পণ্য যোগ হয়েছে");
}

function showSellerProducts(){
 let seller=document.getElementById("sellerName").value.trim();
 let ps=db.products.filter(p=>!p.own&&(!seller||p.seller===seller));
 document.getElementById("sellerList").innerHTML=ps.map(p=>
  `<p>${p.name} — ${money(p.price)} — স্টক ${p.stock}</p>`
 ).join("")||"কোনো পণ্য নেই";
}

// ADMIN LOGIN
let adminLogged=false;

function login(){
 if(document.getElementById("username").value==="admin" &&
    document.getElementById("password").value==="DRshop@123"){
  adminLogged=true;
  showAdmin();
 }else alert("ভুল Username অথবা Password");
}

function logout(){
 adminLogged=false;
 document.getElementById("dashboard").classList.add("hidden");
 document.getElementById("login").classList.remove("hidden");
}

function showAdmin(){
 document.getElementById("login").classList.toggle("hidden",adminLogged);
 document.getElementById("dashboard").classList.toggle("hidden",!adminLogged);
 if(!adminLogged)return;

 document.getElementById("commission").value=db.rate;
 document.getElementById("deliveryCharge").value=db.fee;

 document.getElementById("statistics").innerHTML=
 stat("মোট অর্ডার",db.orders.length)+
 stat("মোট পণ্য",db.products.length)+
 stat("মোট বিক্রয়",money(db.orders.reduce((s,o)=>s+o.grand,0)));

 showWallet();showOrders();showAdminProducts();showAdminSellers();
}

function stat(name,value){
 return `<div class="stat">${name}<b>${value}</b></div>`;
}

function tab(id,btn){
 ["wallet","orders","manage","sellers","settings"].forEach(x=>
  document.getElementById(x).classList.toggle("hidden",x!==id)
 );
 document.querySelectorAll(".tabs button").forEach(x=>x.classList.remove("active"));
 btn.classList.add("active");
}

// ADMIN WALLET
function wallet(){
 let earned=db.orders.filter(o=>o.settled)
  .reduce((s,o)=>s+o.commission,0);
 let withdrawn=db.withdrawals.reduce((s,w)=>s+w.amount,0);
 return {earned,withdrawn,balance:Math.max(0,earned-withdrawn)};
}

function showWallet(){
 let w=wallet();
 document.getElementById("walletStats").innerHTML=
 stat("আদায়কৃত কমিশন",money(w.earned))+
 stat("উত্তোলিত টাকা",money(w.withdrawn))+
 stat("বর্তমান ব্যালেন্স",money(w.balance));

 document.getElementById("history").innerHTML=
 db.withdrawals.map(x=>
  `<p>${x.method} — ${money(x.amount)} — ${x.destination}</p>`
 ).join("")||"কোনো উত্তোলন নেই";
}

function withdrawMethod(){
 let m=document.getElementById("method").value;
 document.getElementById("bankBox").classList.toggle("hidden",m!=="Bank");
 document.getElementById("mobileBox").classList.toggle("hidden",m==="Bank");
}

function withdraw(){
 let amount=Number(document.getElementById("withdrawAmount").value);
 let method=document.getElementById("method").value;
 let destination="";

 if(method==="Bank"){
  let bank=document.getElementById("bankName").value.trim();
  let account=document.getElementById("bankNumber").value.trim();
  if(!bank||!account)return alert("ব্যাংকের তথ্য দিন");
  destination=bank+" / "+account;
 }else{
  destination=document.getElementById("mobileNumber").value.trim();
  if(!/^01[0-9]{9}$/.test(destination))
   return alert("সঠিক মোবাইল নম্বর দিন");
 }

 if(amount<=0||amount>wallet().balance)
  return alert("পর্যাপ্ত উত্তোলনযোগ্য ব্যালেন্স নেই");

 if(!confirm(money(amount)+" উত্তোলনের রেকর্ড তৈরি করবেন?"))return;

 db.withdrawals.unshift({
  date:new Date().toLocaleString(),
  amount,method,destination,
  status:"Demo"
 });

 save();showWallet();
 alert("ডেমো উত্তোলন রেকর্ড হয়েছে। বাস্তবে টাকা পাঠানো হয়নি।");
}

// ADMIN ORDERS
function showOrders(){
 document.getElementById("orderList").innerHTML=
 db.orders.map(o=>`
  <div class="panel">
   <b>${o.id}</b> — ${o.name}<br>
   ${o.phone}<br>${o.address}<br>
   মোট: ${money(o.grand)}<br>
   কমিশন: ${money(o.commission)}<br>
   অবস্থা: ${o.status}<br>
   পেমেন্ট: ${o.settled?"আদায় নিশ্চিত":"সেটেল হয়নি"}<br><br>
   <button onclick="orderStatus('${o.id}','ডেলিভারড')">ডেলিভারড</button>
   <button class="green" onclick="settle('${o.id}')">টাকা আদায় নিশ্চিত</button>
   <button class="red" onclick="cancelOrder('${o.id}')">বাতিল</button>
  </div>
 `).join("")||"কোনো অর্ডার নেই";
}

function orderStatus(id,status){
 let o=db.orders.find(x=>x.id===id);
 if(o){o.status=status;save();showOrders()}
}

function settle(id){
 let o=db.orders.find(x=>x.id===id);
 if(!o)return;
 if(!confirm("এই অর্ডারের টাকা সত্যিই সংগ্রহ হয়েছে?"))return;
 o.settled=true;o.status="পেমেন্ট আদায় নিশ্চিত";
 save();showWallet();showOrders();
}

function cancelOrder(id){
 let o=db.orders.find(x=>x.id===id);
 if(!o||!confirm("অর্ডার বাতিল করবেন?"))return;
 o.status="বাতিল";o.settled=false;
 o.items.forEach(i=>{
  let p=db.products.find(x=>x.id===i.id);
  if(p)p.stock+=i.qty;
 });
 save();showOrders();showProducts();
}

// ADMIN PRODUCT CONTROL
function showAdminProducts(){
 document.getElementById("productList").innerHTML=
 db.products.map(p=>`
  <div class="panel">
   <b>${p.name}</b> — ${money(p.price)}<br>
   Seller: ${p.seller}<br>
   স্টক: ${p.stock}<br>
   অবস্থা: ${p.active===false?"বন্ধ":"চালু"}<br><br>
   <button onclick="editProduct(${p.id})">সম্পাদনা</button>
   <button onclick="toggleProduct(${p.id})">চালু/বন্ধ</button>
   <button class="red" onclick="deleteProduct(${p.id})">মুছুন</button>
  </div>
 `).join("");
}

function editProduct(id){
 let p=db.products.find(x=>x.id===id);
 if(!p)return;
 let name=prompt("পণ্যের নাম",p.name);
 if(name===null)return;
 let price=Number(prompt("দাম",p.price));
 let stock=Number(prompt("স্টক",p.stock));
 if(!name.trim()||price<=0||stock<0)return alert("তথ্য সঠিক নয়");
 p.name=name;p.price=price;p.stock=stock;
 save();showAdminProducts();showProducts();
}

function toggleProduct(id){
 let p=db.products.find(x=>x.id===id);
 if(p){p.active=p.active===false;save();showAdminProducts();showProducts()}
}

function deleteProduct(id){
 if(!confirm("পণ্য মুছে ফেলবেন?"))return;
 db.products=db.products.filter(x=>x.id!==id);
 save();showAdminProducts();showProducts();
}

// SELLER CONTROL
function showAdminSellers(){
 let sellers=[...new Set(db.products.filter(p=>!p.own).map(p=>p.seller))];
 document.getElementById("sellerList").innerHTML=
 sellers.map(s=>`<p><b>${s}</b> — 
 <button onclick="toggleSeller('${s}')">চালু/বন্ধ</button></p>`).join("")
 ||"কোনো Seller নেই";
}

function toggleSeller(name){
 let products=db.products.filter(p=>p.seller===name);
 let active=products.some(p=>p.active===false);
 products.forEach(p=>p.active=active);
 save();showAdminSellers();showAdminProducts();showProducts();
}

// SETTINGS
function saveSettings(){
 let rate=Number(document.getElementById("commission").value);
 let fee=Number(document.getElementById("deliveryCharge").value);
 if(rate<0||rate>100||fee<0)return alert("সঠিক তথ্য দিন");
 db.rate=rate;db.fee=fee;save();
 alert("সেটিংস সংরক্ষিত হয়েছে");
}

// START
save();
showProducts();
updateCount();
withdrawMethod();
</script>

</body>
</html>

