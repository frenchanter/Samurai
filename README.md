<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Для мамы ❤️</title>

<style>

body{
margin:0;
font-family:Arial;
overflow:hidden;
}

/* экран игры */

#game{
position:fixed;
top:0;
left:0;
width:100%;
height:100vh;

background:url("background.jpg");
background-size:cover;
background-position:center;

display:flex;
flex-direction:column;
align-items:center;
padding-top:40px;

color:white;
text-align:center;
}

/* затемнение */

#game::before{
content:"";
position:absolute;
top:0;
left:0;
width:100%;
height:100%;
background:rgba(0,0,0,0.35);
z-index:0;
}

#game h2,#counter{
position:relative;
z-index:2;
}

#counter{
font-size:22px;
margin-top:5px;
}

/* сердечки */

.heart{
position:absolute;
font-size:36px;
cursor:pointer;
animation:fall linear;
z-index:3;
}

@keyframes fall{
0%{transform:translateY(-100px) rotate(0deg);}
100%{transform:translateY(110vh) rotate(360deg);}
}

/* частицы */

.particle{
position:absolute;
font-size:18px;
animation:explode 0.7s forwards;
}

@keyframes explode{
0%{opacity:1;transform:scale(1);}
100%{opacity:0;transform:translateY(-40px) scale(2);}
}

/* поздравление */

#content{
display:none;
padding:30px;
background:#fff;
text-align:center;
}

#content h1{
color:#e91e63;
}

.gallery{
display:flex;
flex-wrap:wrap;
justify-content:center;
gap:10px;
margin-top:20px;
}

.gallery img{
width:45%;
border-radius:12px;
box-shadow:0 4px 10px rgba(0,0,0,0.2);
}

</style>
</head>

<body>

<audio id="music" loop>
<source src="music.mp3" type="audio/mpeg">
</audio>

<div id="game">

<h2>Поймай 8 сердечек 💖</h2>
<div id="counter">0 / 8</div>

</div>

<div id="content">

<h1>С 8 Марта, мамочка 🌸</h1>

<p>
Мамочка, поздравляю тебя с 8 Марта! 🌸
</p>

<p>
Спасибо тебе за твою заботу, любовь и доброту.  
Ты самый близкий и дорогой человек для меня.  
Я очень благодарен тебе за всё, что ты делаешь каждый день.
</p>

<p>
Желаю тебе крепкого здоровья, счастья, радости и всегда хорошего настроения.  
Пусть у тебя всё получается, а каждый день будет наполнен улыбками, теплом и приятными моментами.
</p>

<p>
Я тебя очень люблю! ❤️
</p>

<p><b>С любовью, твой Самурай!</b></p>

<div class="gallery">

<img src="photo1.jpg">
<img src="photo2.jpg">
<img src="photo3.jpg">
<img src="photo4.jpg">

</div>

</div>

<script>

let count=0
let gameActive=true

const hearts=["💖","💗","💓","💘","❤️"]

function particles(x,y){

for(let i=0;i<6;i++){

let p=document.createElement("div")
p.className="particle"
p.innerHTML="✨"

p.style.left=x+"px"
p.style.top=y+"px"

document.body.appendChild(p)

setTimeout(()=>p.remove(),700)

}

}

function createHeart(){

if(!gameActive) return

let heart=document.createElement("div")

heart.className="heart"
heart.innerHTML=hearts[Math.floor(Math.random()*hearts.length)]

heart.style.left=Math.random()*90+"%"
heart.style.animationDuration=(3+Math.random()*2)+"s"

heart.onclick=function(e){

count++

document.getElementById("counter").innerText=count+" / 8"

particles(e.clientX,e.clientY)

heart.remove()

if(count>=8){

gameActive=false

document.getElementById("music").play()

setTimeout(()=>{

document.getElementById("game").style.display="none"

document.body.style.overflow="auto"

document.getElementById("content").style.display="block"

},600)

}

}

heart.addEventListener("animationend",()=>heart.remove())

document.body.appendChild(heart)

}

setInterval(createHeart,700)

</script>

</body>
</html>
