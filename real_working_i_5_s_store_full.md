<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>i5s Store</title>

<style>

body{
margin:0;
background:#050505;
font-family:Arial;
color:white;
}

.login-page{
height:100vh;
display:flex;
justify-content:center;
align-items:center;
}

.login-box{
width:400px;
background:#111;
padding:40px;
border-radius:20px;
border:1px solid #333;
}

.logo{
font-size:55px;
font-weight:bold;
color:#ff2e2e;
margin-bottom:10px;
}

.sub{
color:#777;
margin-bottom:20px;
}

input{
width:100%;
height:55px;
background:#1a1a1a;
border:1px solid #333;
border-radius:10px;
padding:0 15px;
margin-bottom:15px;
color:white;
font-size:16px;
box-sizing:border-box;
}

button{
width:100%;
height:55px;
border:none;
border-radius:10px;
font-size:16px;
font-weight:bold;
cursor:pointer;
margin-bottom:10px;
}

.login-btn{
background:#ff2e2e;
color:white;
}

.register-btn{
background:#222;
color:white;
}

#store{
display:none;
padding:30px;
}

.navbar{
display:flex;
justify-content:space-between;
align-items:center;
margin-bottom:30px;
}

.balance{
background:#111;
padding:15px 20px;
border-radius:10px;
border:1px solid #333;
}

.logout{
background:#ff2e2e;
color:white;
padding:15px 20px;
border:none;
border-radius:10px;
cursor:pointer;
}

.card{
background:#111;
border:1px solid #333;
padding:25px;
border-radius:20px;
margin-bottom:20px;
}

.buy-btn{
background:#ff2e2e;
color:white;
margin-top:15px;
}

</style>
</head>

<body>

<div id="loginPage" class="login-page">

<div class="login-box">

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

</div>

<div id="store">

<div class="navbar">

<h1>
i5s Store
</h1>

<div style="display:flex;gap:10px;align-items:center;">

<div class="balance">
Balance: $<span id="balance">0</span>
</div>

<button class="logout" onclick="logout()">
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

</div>

<script>

let users = JSON.parse(localStorage.getItem("users")) || [];

let currentUser = JSON.parse(localStorage.getItem("currentUser")) || null;

if(currentUser){
openStore(currentUser);
}

function registerUser(){

const username = document.getElementById("username").value.trim();

const password = document.getElementById("password").value.trim();

if(username === "" || password === ""){
alert("Fill all fields");
return;
}

const exists = users.find(user => user.username === username);

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

localStorage.setItem("users", JSON.stringify(users));

alert("Account created successfully");

}

function login(){

const username = document.getElementById("username").value.trim();

const password = document.getElementById("password").value.trim();

const foundUser = users.find(user =>
user.username === username &&
user.password === password
);

if(!foundUser){
alert("Invalid login");
return;
}

localStorage.setItem("currentUser", JSON.stringify(foundUser));

openStore(foundUser);

}

function openStore(user){

document.getElementById("loginPage").style.display = "none";

document.getElementById("store").style.display = "block";

document.getElementById("welcomeText").innerText =
"Logged in as " + user.username;

document.getElementById("balance").innerText = user.balance;

}

function logout(){

localStorage.removeItem("currentUser");

location.reload();

}

function buyItem(price){

let user = JSON.parse(localStorage.getItem("currentUser"));

if(user.balance < price){
alert("Not enough balance");
return;
}

user.balance -= price;

document.getElementById("balance").innerText = user.balance;

localStorage.setItem("currentUser", JSON.stringify(user));

users = users.map(u => {

if(u.username === user.username){
return user;
}

return u;

});

localStorage.setItem("users", JSON.stringify(users));

alert("Purchased");

}

</script>

</body>
</html>
