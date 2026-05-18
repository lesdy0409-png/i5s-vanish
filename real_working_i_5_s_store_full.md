<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>i5s Store</title>

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial;
}

body{
background:#050505;
color:white;
height:100vh;
display:flex;
justify-content:center;
align-items:center;
}

.container{
width:420px;
background:#111;
padding:35px;
border-radius:25px;
border:1px solid #333;
box-shadow:0 0 30px rgba(255,0,0,0.2);
}

.logo{
font-size:55px;
font-weight:bold;
color:#ff2e2e;
margin-bottom:10px;
}

.sub{
color:#888;
margin-bottom:25px;
}

input{
width:100%;
height:55px;
background:#1a1a1a;
border:1px solid #333;
border-radius:12px;
padding:0 15px;
color:white;
font-size:15px;
margin-bottom:15px;
outline:none;
}

button{
width:100%;
height:55px;
border:none;
border-radius:12px;
font-size:16px;
font-weight:bold;
cursor:pointer;
margin-bottom:12px;
}

.login-btn{
background:#ff2e2e;
color:white;
}

.register-btn{
background:#222;
color:white;
}

#storePage{
display:none;
width:100%;
height:100vh;
padding:40px;
}

.navbar{
display:flex;
justify-content:space-between;
align-items:center;
margin-bottom:30px;
}

.balance{
background:#111;
padding:14px 20px;
border-radius:12px;
border:1px solid #333;
}

.logout-btn{
background:#ff2e2e;
padding:14px 20px;
border-radius:12px;
border:none;
color:white;
font-weight:bold;
cursor:pointer;
}

.card{
background:#111;
border:1px solid #333;
padding:30px;
border-radius:20px;
margin-bottom:20px;
}

.card h2{
margin-bottom:15px;
}

.buy-btn{
background:#ff2e2e;
color:white;
height:50px;
margin-top:15px;
}

</style>
</head>

<body>

<div id="loginPage" class="container">

<div class="logo">
i5s
</div>

<div class="sub">
Secure Digital Store
</div>

<input type="text" id="username" placeholder="Username">

<input type="password" id="password" placeholder="Password">

<button class="login-btn" onclick="login()">
Login
</button>

<button class="register-btn" onclick="registerUser()">
Create Account
</button>

</div>

<div id="storePage">

<div class="navbar">

<h1>
i5s Store
</h1>

<div style="display:flex;gap:10px;align-items:center;">

<div class="balance">
Balance: $<span id="balance">0</span>
</div>

<button class="logout-btn" onclick="logout()">
Logout
</button>

</div>

</div>

<div class="card">

<h2>
Welcome
</h2>

<p id="welcomeText">
Logged in
</p>

</div>

<div class="card">

<h2>
1D Access
</h2>

<p>
Price: $10
</p>

<button class="buy-btn" onclick="buyItem(10)">
Purchase
</button>

</div>

<div class="card">

<h2>
3D Access
</h2>

<p>
Price: $25
</p>

<button class="buy-btn" onclick="buyItem(25)">
Purchase
</button>

</div>

</div>

<script>

let users = JSON.parse(
localStorage.getItem("users")
) || [];

let currentUser = JSON.parse(
localStorage.getItem("currentUser")
) || null;

if(currentUser){
openStore(currentUser);
}

function registerUser(){

const username = document
.getElementById("username")
.value
.trim();

const password = document
.getElementById("password")
.value
.trim();

if(username === "" || password === ""){
alert("Fill all fields");
return;
}

const exists = users.find(
user => user.username === username
);

if(exists){
alert("Username already exists");
return;
}

const newUser = {
username: username,
password: password,
balance: 0
};

users.push(newUser);

localStorage.setItem(
"users",
JSON.stringify(users)
);

alert("Account created successfully");

}

function login(){

const username = document
.getElementById("username")
.value
.trim();

const password = document
.getElementById("password")
.value
.trim();

const foundUser = users.find(
user =>
user.username === username &&
user.password === password
);

if(!foundUser){
alert("Invalid login");
return;
}

localStorage.setItem(
"currentUser",
JSON.stringify(foundUser)
);

openStore(foundUser);

}

function openStore(user){

document.getElementById("loginPage")
.style.display = "none";

document.getElementById("storePage")
.style.display = "block";

document.getElementById("welcomeText")
.innerText =
"Logged in as " + user.username;

document.getElementById("balance")
.innerText = user.balance;

}

function logout(){

localStorage.removeItem(
"currentUser"
);

location.reload();

}

function buyItem(price){

const savedUser = JSON.parse(
localStorage.getItem("currentUser")
);

if(savedUser.balance < price){
alert("Not enough balance");
return;
}

savedUser.balance -= price;

document.getElementById("balance")
.innerText = savedUser.balance;

localStorage.setItem(
"currentUser",
JSON.stringify(savedUser)
);

users = users.map(user => {

if(user.username === savedUser.username){
return savedUser;
}

return user;

});

localStorage.setItem(
"users",
JSON.stringify(users)
);

alert("Purchased");

}

</script>

</body>
</html>
