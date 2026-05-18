<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>i5s Store</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@700;800&family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Inter',sans-serif}
body{background:#050505;color:#fff;overflow-x:hidden}
body:before{content:'';position:fixed;width:600px;height:600px;background:rgba(255,0,0,.12);filter:blur(140px);left:-150px;top:-150px;z-index:-1}
body:after{content:'';position:fixed;width:500px;height:500px;background:rgba(255,0,0,.12);filter:blur(140px);right:-100px;bottom:-100px;z-index:-1}
.hidden{display:none!important}
.login-page{height:100vh;display:flex;justify-content:center;align-items:center;padding:20px}
.login-box{width:420px;background:#0d0d0d;border:1px solid #222;border-radius:28px;padding:45px;box-shadow:0 0 40px rgba(255,0,0,.12)}
.logo{font-family:'Orbitron',sans-serif;font-size:54px;font-weight:800;color:#ff3434;margin-bottom:10px}
.sub{color:#888;margin-bottom:30px}
.input{width:100%;height:58px;background:#111;border:1px solid #222;border-radius:16px;padding:0 18px;color:white;font-size:16px;margin-bottom:15px;outline:none}
.main-btn{width:100%;height:58px;border:none;border-radius:16px;background:#ff2e2e;color:white;font-size:17px;font-weight:800;cursor:pointer}
.second-btn{width:100%;height:58px;border:none;border-radius:16px;background:#1a1a1a;color:#aaa;font-size:16px;font-weight:700;cursor:pointer;margin-top:12px}
.navbar{height:80px;border-bottom:1px solid #1a1a1a;display:flex;justify-content:space-between;align-items:center;padding:0 30px;position:sticky;top:0;background:#070707ee;backdrop-filter:blur(10px);z-index:99}
.nav-right{display:flex;gap:12px;align-items:center;flex-wrap:wrap}
.balance,.nav-btn{padding:14px 20px;background:#111;border:1px solid #222;border-radius:14px;color:white}
.nav-btn{cursor:pointer}
.page{padding:35px}
.hero{background:linear-gradient(135deg,#090909,#170909);border:1px solid #221111;border-radius:32px;padding:60px;margin-bottom:40px;display:flex;justify-content:space-between;align-items:center;gap:20px}
.hero h1{font-size:70px;font-weight:900;margin-bottom:20px}
.hero p{color:#999;font-size:18px;line-height:1.7;max-width:700px}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:22px}
.card,.inventory-item,.request,.topup-box{background:#0d0d0d;border:1px solid #1d1d1d;border-radius:28px;padding:30px}
.card h2{font-size:34px;margin-bottom:15px}
.price{font-size:46px;font-weight:900;color:#ff3434;margin-bottom:20px}
.buy-btn{width:100%;height:58px;border:none;border-radius:16px;background:#ff2e2e;color:white;font-size:16px;font-weight:800;cursor:pointer}
.section-title{font-size:38px;font-weight:900;margin-bottom:25px}
.actions{display:flex;gap:10px;margin-top:15px}
.approve,.reject{padding:12px 18px;border:none;border-radius:12px;color:white;cursor:pointer}
.approve{background:#ff2e2e}.reject{background:#333}
@media(max-width:800px){.hero{flex-direction:column;text-align:center}.hero h1{font-size:48px}.navbar{height:auto;padding:20px;flex-direction:column;gap:20px}}
</style>
</head>
<body>
<div id="loginPage" class="login-page">
<div class="login-box">
<div class="logo">i5s</div>
<div class="sub">Secure Digital Store Login</div>
<input class="input" id="username" type="text" placeholder="Username">
<input class="input" id="password" type="password" placeholder="Password">
<button class="main-btn" onclick="login()">Login</button>
<button class="second-btn" onclick="register()">Create Account</button>
</div>
</div>
<div id="mainSite" class="hidden">
<div class="navbar">
<div class="logo" style="font-size:38px">i5s</div>
<div class="nav-right">
<div class="balance">Balance: $<span id="balance">0</span></div>
<button class="nav-btn" onclick="showPage('shop')">Purchase</button>
<button class="nav-btn" onclick="showPage('topup')">TopUp</button>
<button class="nav-btn" onclick="showPage('inventory')">Inventory</button>
<button id="adminBtn" class="nav-btn hidden" onclick="showPage('admin')">Admin</button>
<button class="nav-btn" onclick="logout()">Logout</button>
</div>
</div>
<div id="shop" class="page">
<div class="hero">
<div>
<h1>Premium Digital Store</h1>
<p>Purchase premium products instantly with your balance. Secure dashboard, auto login, inventory system and admin approval included.</p>
</div>
</div>
<div class="section-title">Products</div>
<div class="grid">
<div class="card"><h2>1D</h2><div class="price">$10</div><button class="buy-btn" onclick="buy(10,'1D Access')">Purchase</button></div>
<div class="card"><h2>3D</h2><div class="price">$25</div><button class="buy-btn" onclick="buy(25,'3D Access')">Purchase</button></div>
<div class="card"><h2>5D</h2><div class="price">$40</div><button class="buy-btn" onclick="buy(40,'5D Access')">Purchase</button></div>
<div class="card"><h2>7D</h2><div class="price">$60</div><button class="buy-btn" onclick="buy(60,'7D Access')">Purchase</button></div>
<div class="card"><h2>10D</h2><div class="price">$85</div><button class="buy-btn" onclick="buy(85,'10D Access')">Purchase</button></div>
<div class="card"><h2>Permanent</h2><div class="price">$150</div><button class="buy-btn" onclick="buy(150,'Permanent Access')">Purchase</button></div>
</div>
</div>
<div id="topup" class="page hidden">
<div class="section-title">Top Up</div>
<div class="topup-box">
<input class="input" id="amount" type="number" placeholder="Enter Amount">
<button class="main-btn" onclick="createRequest()">Create Payment Request</button>
</div>
</div>
<div id="inventory" class="page hidden">
<div class="section-title">Inventory</div>
<div id="inventoryList"></div>
</div>
<div id="admin" class="page hidden">
<div class="section-title">Admin Requests</div>
<div id="requestList"></div>
</div>
</div>
<script>
const ADMIN_USERNAME='woojun';
const ADMIN_PASSWORD='F1AX65DvCA45X';
let users=JSON.parse(localStorage.getItem('users'))||[];
let requests=JSON.parse(localStorage.getItem('requests'))||[];
let currentUser=JSON.parse(localStorage.getItem('currentUser'))||null;
if(!users.find(u=>u.username===ADMIN_USERNAME)){
users.push({username:ADMIN_USERNAME,password:ADMIN_PASSWORD,balance:0,inventory:[]});
localStorage.setItem('users',JSON.stringify(users));
}
window.onload=()=>{if(currentUser){showSite();}}
function register(){
const username=document.getElementById('username').value.trim();
const password=document.getElementById('password').value.trim();
if(username===''||password===''){alert('Fill all fields');return;}
if(users.find(u=>u.username===username)){alert('Username already exists');return;}
const user={username,password,balance:0,inventory:[]};
users.push(user);
localStorage.setItem('users',JSON.stringify(users));
alert('Account Created Successfully');
}
function login(){
const username=document.getElementById('username').value.trim();
const password=document.getElementById('password').value.trim();
const foundUser=users.find(u=>u.username===username&&u.password===password);
if(!foundUser){alert('Invalid Account');return;}
currentUser=foundUser;
localStorage.setItem('currentUser',JSON.stringify(currentUser));
showSite();
}
function showSite(){
document.getElementById('loginPage').classList.add('hidden');
document.getElementById('mainSite').classList.remove('hidden');
updateBalance();
renderInventory();
renderRequests();
if(currentUser.username===ADMIN_USERNAME&&currentUser.password===ADMIN_PASSWORD){
document.getElementById('adminBtn').classList.remove('hidden');
}
}
function logout(){localStorage.removeItem('currentUser');location.reload();}
function updateBalance(){document.getElementById('balance').innerText=currentUser.balance;}
function showPage(page){['shop','topup','inventory','admin'].forEach(id=>{document.getElementById(id).classList.add('hidden')});document.getElementById(page).classList.remove('hidden');}
function saveUser(){users=users.map(u=>u.username===currentUser.username?currentUser:u);localStorage.setItem('users',JSON.stringify(users));localStorage.setItem('currentUser',JSON.stringify(currentUser));}
function buy(price,name){if(currentUser.balance<price){alert('Not enough balance');return;}currentUser.balance-=price;currentUser.inventory.push(name);saveUser();updateBalance();renderInventory();alert('Purchased Successfully');}
function renderInventory(){const list=document.getElementById('inventoryList');list.innerHTML='';if(currentUser.inventory.length===0){list.innerHTML='<div class="inventory-item">No items purchased yet.</div>';return;}currentUser.inventory.forEach(item=>{list.innerHTML+=`<div class="inventory-item">${item}</div>`});}
function createRequest(){const amount=Number(document.getElementById('amount').value);if(!amount||amount<=0){alert('Invalid Amount');return;}requests.push({id:Date.now(),user:currentUser.username,amount});localStorage.setItem('requests',JSON.stringify(requests));document.getElementById('amount').value='';renderRequests();alert('Payment Request Sent');}
function renderRequests(){const list=document.getElementById('requestList');list.innerHTML='';requests.forEach(req=>{list.innerHTML+=`<div class="request"><div><b>${req.user}</b><br>$${req.amount}</div><div class="actions"><button class="approve" onclick="approve(${req.id})">Approve</button><button class="reject" onclick="rejectReq(${req.id})">Reject</button></div></div>`});}
function approve(id){const req=requests.find(r=>r.id===id);if(!req)return;const user=users.find(u=>u.username===req.user);if(user){user.balance+=req.amount;}if(currentUser.username===user.username){currentUser.balance=user.balance;updateBalance();}localStorage.setItem('users',JSON.stringify(users));requests=requests.filter(r=>r.id!==id);localStorage.setItem('requests',JSON.stringify(requests));renderRequests();alert('Approved');}
function rejectReq(id){requests=requests.filter(r=>r.id!==id);localStorage.setItem('requests',JSON.stringify(requests));renderRequests();alert('Rejected');}
</script>
</body>
</html>

