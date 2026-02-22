<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mega Sándwich - Pedidos</title>

<style>
*{box-sizing:border-box;font-family:Arial,Helvetica,sans-serif}
body{margin:0;background:#f8f9fc;color:#222}

header{
background:#0d1b2a;
color:white;
padding:15px;
text-align:center;
}

header img{
width:120px;
border-radius:50%;
border:4px solid white;
margin-bottom:10px;
}

section{padding:15px}

h2{text-align:center;color:#0d1b2a}

.menu{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(160px,1fr));
gap:10px;
}

.item{
background:white;
border-radius:12px;
padding:10px;
text-align:center;
box-shadow:0 0 8px rgba(0,0,0,.1)
}

.item img{
width:100%;
height:130px;
object-fit:cover;
border-radius:10px;
}

.precio{font-weight:bold;color:#ff7b00;font-size:18px}

button{
width:100%;
padding:10px;
margin-top:5px;
border-radius:10px;
border:none;
background:#25d366;
color:white;
font-weight:bold;
cursor:pointer;
}

button:hover{background:#1ebe5d}

.carrito{
background:white;
border-radius:12px;
padding:10px;
box-shadow:0 0 8px rgba(0,0,0,.1);
}

.total{
font-size:20px;
font-weight:bold;
text-align:center;
margin-top:10px;
}

input,select,textarea{
width:100%;
padding:10px;
margin-top:8px;
border-radius:10px;
border:1px solid #ccc;
}

.whatsapp{
position:fixed;
right:15px;
bottom:15px;
background:#25d366;
color:white;
padding:15px;
border-radius:50%;
font-size:22px;
text-decoration:none;
box-shadow:0 0 10px rgba(0,0,0,.4);
}
</style>
</head>

<body>

<header>
<img src="logo.png">
<h1>MEGA SÁNDWICH</h1>
<p>Pedidos Online</p>
</header>

<section>
<h2>🥪 Menú</h2>
<div class="menu">

<div class="item"><img src="JYQ.jpg"><h3>JYQ 1 doc</h3><p class="precio">$16000</p><button onclick="agregar('JYQ 1 doc',16000)">Agregar</button></div>
<div class="item"><img src="JYQ.jpg"><h3>JYQ 1/2 doc</h3><p class="precio">$8500</p><button onclick="agregar('JYQ 1/2 doc',8500)">Agregar</button></div>
<div class="item"><img src="Primavera.jpg"><h3>Pollo 1 doc</h3><p class="precio">$19000</p><button onclick="agregar('Pollo 1 doc',19000)">Agregar</button></div>
<div class="item"><img src="Primavera.jpg"><h3>Pollo 1/2 doc</h3><p class="precio">$10000</p><button onclick="agregar('Pollo 1/2 doc',10000)">Agregar</button></div>
<div class="item"><img src="Verdura.jpg"><h3>Verdura 1 doc</h3><p class="precio">$17000</p><button onclick="agregar('Verdura 1 doc',17000)">Agregar</button></div>
<div class="item"><img src="Verdura.jpg"><h3>Verdura 1/2 doc</h3><p class="precio">$9000</p><button onclick="agregar('Verdura 1/2 doc',9000)">Agregar</button></div>
<div class="item"><img src="Ternera.jpg"><h3>Ternera 1 doc</h3><p class="precio">$26000</p><button onclick="agregar('Ternera 1 doc',26000)">Agregar</button></div>
<div class="item"><img src="Ternera.jpg"><h3>Ternera 1/2 doc</h3><p class="precio">$13500</p><button onclick="agregar('Ternera 1/2 doc',13500)">Agregar</button></div>
<div class="item"><img src="JYQPanNegro.jpg"><h3>JYQ Pan Negro 1 doc</h3><p class="precio">$18000</p><button onclick="agregar('JYQ Pan Negro 1 doc',18000)">Agregar</button></div>
<div class="item"><img src="JYQPanNegro.jpg"><h3>JYQ Pan Negro 1/2 doc</h3><p class="precio">$9500</p><button onclick="agregar('JYQ Pan Negro 1/2 doc',9500)">Agregar</button></div>
<div class="item"><img src="Variados.jpg"><h3>Pebetes unidad</h3><p class="precio">$2000</p><button onclick="agregar('Pebetes',2000)">Agregar</button></div>

</div>
</section>

<section>
<h2>🛒 Tu Pedido</h2>

<div class="carrito" id="lista"></div>
<div class="total" id="total">Total: $0</div>

<h2>📋 Datos del Cliente</h2>

<input id="nombre" placeholder="Nombre y apellido">
<input id="telefono" placeholder="Número de teléfono">
<textarea id="direccion" placeholder="Dirección completa"></textarea>

<select id="pago">
<option value="">Forma de pago</option>
<option>Efectivo</option>
<option>Transferencia</option>
</select>

<button onclick="enviarPedido()">Enviar pedido por WhatsApp</button>
</section>

<a class="whatsapp" href="https://wa.me/5493537557501" target="_blank">💬</a>

<script>
let carrito=[];

function agregar(nombre,precio){
    carrito.push({nombre,precio});
    mostrarCarrito();
}

function mostrarCarrito(){
    let lista=document.getElementById("lista");
    let total=document.getElementById("total");
    lista.innerHTML="";
    let suma=0;

    carrito.forEach((item,i)=>{
        lista.innerHTML += (i+1)+". "+item.nombre+" - $"+item.precio+"<br>";
        suma += item.precio;
    });

    total.innerHTML="Total: $"+suma;
}

function enviarPedido(){
    if(carrito.length===0){
        alert("El carrito está vacío");
        return;
    }

    let nombre=document.getElementById("nombre").value;
    let telefono=document.getElementById("telefono").value;
    let direccion=document.getElementById("direccion").value;
    let pago=document.getElementById("pago").value;

    if(!nombre || !telefono || !direccion || !pago){
        alert("Completá todos los datos");
        return;
    }

    let mensaje="🛒 *Pedido Mega Sándwich* %0A%0A";
    mensaje+="👤 Nombre: "+nombre+"%0A";
    mensaje+="📞 Tel: "+telefono+"%0A";
    mensaje+="📍 Dirección: "+direccion+"%0A";
    mensaje+="💳 Pago: "+pago+"%0A%0A";
    mensaje+="📦 Pedido:%0A";

    let total=0;
    carrito.forEach((item,i)=>{
        mensaje+=(i+1)+". "+item.nombre+" - $"+item.precio+"%0A";
        total+=item.precio;
    });

    mensaje+="%0A💰 Total: $"+total;

    window.open("https://wa.me/5493537557501?text="+mensaje,"_blank");
}
</script>

</body>
</html>
