# Lop-2019
Projeto lop ect ufrn 20191

var a = "";
var b = 0;
var x = 300;
var y = 500;
var xo = 0;
var yo = 0;
var velo=3;
var qntasteroides = 6;
var estadoDisparo = false;
var barreiradepontos = 30;

//escritas
var vida = 10;
var aux = 10;
var ax = 0;
var pontos = 0;
var dificuldade = 1;

//vetores 
var asteroides = [];
var astx = [];
var asty = [];


//telas
var tela = 1;
var tempo = 0

//carregar imagens
let imgFoguete;
let asteroide;
let fundo;
let bomba;
let explosao;
let iniciotela;
let gameover;
function preload(){
  imgFoguete = loadImage('nave.png');
  asteroide = loadImage('asteroide.png');
  fundo = loadImage('potw1148a.jpg');
  bomba = loadImage('bomba.png');
  explosao = loadImage('281626116048211.png');
  iniciotela = loadImage('4290270.jpg');
  gameover = loadImage('fimdejogo.png');

}

//quantidade de asteroides
  function setup() {
    for (i=0 ; i< qntasteroides ; i++){
    asteroides[i]=asteroide;
      astx[i]=random(30, 570);
      asty[i]=-random(30);      
    

//tela principal    
  createCanvas(600, 600);
}}

function draw() {
 if(tela == 1){  
    image(iniciotela, 0, 0);
    textSize(50);
    fill(255,255,255);
    text("GALAXY DESTROYER" ,40,300);
    textSize(25);
    fill(200,200,200);
    text("Aperte ENTER para começar", 140, 500);
    if(keyIsDown(ENTER)){
      tela = 2;
    }
}
if(tela==2){
    
//tela jogo
  image(fundo, 0, 0);

//texto jogo   
  fill (255,255,255);
  textSize(30);
  text("Vida: " +vida, 10, 30);
  text("Pontos: " +pontos, 240, 30);
  text ("Nível: " +dificuldade, 470, 30);
    
//comandos das setas  
  if (keyIsDown(LEFT_ARROW)){
    x = x - 10;
  }
  if (keyIsDown(RIGHT_ARROW)){
    x = x + 10;
  }
  if (keyIsDown(DOWN_ARROW)){
    y = y + 10;
  }
  if (keyIsDown(UP_ARROW)){
    y = y - 10;
  }
  fill (150);
  
//personagem principal
 imageMode (CENTER);
  image(imgFoguete,x,y,100,100);
  
//limitação de tela 
  if (x > width){
  x = 600;
  }
  if (x < 0){
  x = 0;
  }
  if ( y > width){
  y = 600;
  }
  if ( y < 0){
  y = 0;
  }
//disparo e bombas      
  if (keyIsDown(65)&& estadoDisparo == false ){
    xo = x;
    yo = y;
    estadoDisparo = true;
  }      
  if ( estadoDisparo ){
    image(bomba, xo, yo , 50, 50);
    yo = yo - 10 - velo;
    if (yo < 50 ) {
      estadoDisparo = false;
    }
    
  }  
  for(j=0; j < qntasteroides ; j++){
    image(asteroides[j] , astx[j], asty[j], 100, 100);
    asty[j]=asty[j]+5;
      if(asty[j]>600){
        astx[j] = random(30,570)
        asty[j]=-random(30,120);
      }

//incremento de pontos
    if (dist(xo, yo, astx[j] , asty[j]) < 30 && estadoDisparo == true){
      astx[j] = random(30,570)
      asty[j]=-random(30,120);
      ax = ax + 1
      pontos = int(ax)
      if(pontos > barreiradepontos){
        dificuldade++;
        barreiradepontos += 10;
        }
    }
    
//vidas
    if (dist(x, y, astx[j] , asty[j]) < 50){
      astx[j] = random(30,570)   
      asty[j]=-random(30,120);
      aux = aux -1;
      vida = int(aux) 
      }
  if(vida<=0){
      tela=3; 
    }
  if (tela == 3){
     image(gameover, 300, 300, 0, 0);
     fill (200,200,200);
     textSize(30);
     if(keyIsDown(ENTER)){
       tela = 1;
       vida = 5;
       aux = 5;
       pontos = 0;
       dificudade = 1;
       astx[j] = random(30,570)
       asty[j]=-random(30,120);
        }
      }
    }
  }
}
