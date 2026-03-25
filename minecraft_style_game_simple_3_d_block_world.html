<!DOCTYPE html>
<html>
<head>
  <title>Minecraft Lite EXTREME</title>
  <style>
    body { margin:0; overflow:hidden; font-family:sans-serif; }
    #crosshair { position:fixed; top:50%; left:50%; width:10px; height:10px; margin:-5px; background:white; }
    #hotbar { position:fixed; bottom:20px; left:50%; transform:translateX(-50%); display:flex; gap:6px; }
    .slot { width:40px; height:40px; border:2px solid white; display:flex; align-items:center; justify-content:center; background:rgba(0,0,0,0.5);} 
    .selected { border-color:yellow; }
    #stats { position:fixed; top:10px; left:10px; color:white; }
  </style>
</head>
<body>
<div id="crosshair"></div>
<div id="hotbar"></div>
<div id="stats"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/simplex-noise@2.4.0/simplex-noise.js"></script>
<script>
const scene=new THREE.Scene();
const camera=new THREE.PerspectiveCamera(75,innerWidth/innerHeight,0.1,1000);
const renderer=new THREE.WebGLRenderer();
renderer.setSize(innerWidth,innerHeight);
document.body.appendChild(renderer.domElement);

// lighting
let time=0;
const sun=new THREE.DirectionalLight(0xffffff,1);
scene.add(new THREE.AmbientLight(0x555555));
scene.add(sun);

// textures
const loader=new THREE.TextureLoader();
const tex={
 grass:loader.load('https://i.imgur.com/3dXn6Qx.png'),
 dirt:loader.load('https://i.imgur.com/8I3490M.png'),
 stone:loader.load('https://i.imgur.com/Uw6Qp6B.png'),
 wood:loader.load('https://i.imgur.com/9bK0nQp.png')
};

const mat={};
Object.keys(tex).forEach(k=>mat[k]=new THREE.MeshLambertMaterial({map:tex[k]}));

// inventory system
let inventory={grass:10,dirt:10,stone:10,wood:0};
let hotbarItems=['grass','dirt','stone','wood'];
let selected=0;

const hotbar=document.getElementById('hotbar');
function drawHotbar(){
 hotbar.innerHTML='';
 hotbarItems.forEach((item,i)=>{
  const d=document.createElement('div');
  d.className='slot'+(i===selected?' selected':'');
  d.textContent=item[0].toUpperCase()+"\n"+(inventory[item]||0);
  hotbar.appendChild(d);
 });
}
drawHotbar();

addEventListener('wheel',e=>{
 selected=(selected+(e.deltaY>0?1:-1)+hotbarItems.length)%hotbarItems.length;
 drawHotbar();
});

// stats
let health=100, hunger=100;
const stats=document.getElementById('stats');

function updateStats(){
 stats.innerHTML=`Health: ${health}<br>Hunger: ${hunger}`;
}
setInterval(()=>{
 hunger-=0.1;
 if(hunger<=0) health-=0.2;
 updateStats();
},100);

// world
const noise=new SimplexNoise();
const blocks=[];
const blockMap={};
function key(x,y,z){return x+','+y+','+z;}

function addBlock(x,y,z,type){
 const geo=new THREE.BoxGeometry(1,1,1);
 const cube=new THREE.Mesh(geo,mat[type]);
 cube.position.set(x,y,z);
 scene.add(cube);
 blocks.push(cube);
 blockMap[key(x,y,z)]=cube;
}

function removeBlock(obj){
 const p=obj.position;
 delete blockMap[key(p.x,p.y,p.z)];
 scene.remove(obj);
 blocks.splice(blocks.indexOf(obj),1);
}

// better terrain + trees
function generateTerrain(x,z){
 let h=Math.floor(noise.noise2D(x/30,z/30)*8);
 return h;
}

function maybeTree(x,y,z){
 if(Math.random()<0.05){
  for(let i=1;i<4;i++) addBlock(x,y+i,z,'wood');
 }
}

// chunks
const chunkSize=16,renderDist=2,chunks={};
function ckey(x,z){return x+','+z;}
function genChunk(cx,cz){
 const k=ckey(cx,cz); if(chunks[k]) return; chunks[k]=true;
 for(let x=0;x<chunkSize;x++){
  for(let z=0;z<chunkSize;z++){
   let wx=cx*chunkSize+x;
   let wz=cz*chunkSize+z;
   let h=generateTerrain(wx,wz);
   for(let y=0;y<=h;y++){
    let t='dirt'; if(y===h)t='grass'; if(y<h-3)t='stone';
    addBlock(wx,y,wz,t);
   }
   maybeTree(wx,h,wz);
  }
 }
}

function updateChunks(){
 const cx=Math.floor(camera.position.x/chunkSize);
 const cz=Math.floor(camera.position.z/chunkSize);
 for(let x=-renderDist;x<=renderDist;x++){
  for(let z=-renderDist;z<=renderDist;z++) genChunk(cx+x,cz+z);
 }
}

// collision
function isSolid(x,y,z){return blockMap[key(Math.round(x),Math.round(y),Math.round(z))];}

// player
camera.position.set(0,10,5);
let velY=0,onGround=false;
const keys={};
addEventListener('keydown',e=>keys[e.key]=true);
addEventListener('keyup',e=>keys[e.key]=false);

function move(){
 let s=0.15;
 let nx=camera.position.x, nz=camera.position.z;
 if(keys['w']) nz-=s;
 if(keys['s']) nz+=s;
 if(keys['a']) nx-=s;
 if(keys['d']) nx+=s;

 if(!isSolid(nx,Math.floor(camera.position.y),camera.position.z)) camera.position.x=nx;
 if(!isSolid(camera.position.x,Math.floor(camera.position.y),nz)) camera.position.z=nz;

 velY-=0.01;
 let ny=camera.position.y+velY;
 if(isSolid(camera.position.x,Math.floor(ny),camera.position.z)){
  velY=0; onGround=true;
 } else camera.position.y=ny;

 if(keys[' ']&&onGround){velY=0.25; onGround=false;}
}

// mouse
let yaw=0,pitch=0;
document.body.onclick=()=>document.body.requestPointerLock();
addEventListener('mousemove',e=>{
 if(document.pointerLockElement===document.body){
  yaw-=e.movementX*0.002;
  pitch-=e.movementY*0.002;
  pitch=Math.max(-Math.PI/2,Math.min(Math.PI/2,pitch));
  camera.rotation.set(pitch,yaw,0);
 }
});

// raycast
const raycaster=new THREE.Raycaster();
const mouse=new THREE.Vector2(0,0);
function hit(){ raycaster.setFromCamera(mouse,camera); return raycaster.intersectObjects(blocks); }

// tools (speed)
const toolSpeed={hand:1, pickaxe:2};
let currentTool='hand';

// breaking
let breakTime=0,breaking=null;
addEventListener('mousedown',()=>{
 const h=hit();
 if(h.length){breaking=h[0].object; breakTime=0;}
});
addEventListener('mouseup',()=>breaking=null);

// placing
addEventListener('contextmenu',e=>{
 e.preventDefault();
 const h=hit();
 if(h.length){
  const p=h[0].point.clone().add(h[0].face.normal);
  const type=hotbarItems[selected];
  if(inventory[type]>0){
    addBlock(Math.round(p.x),Math.round(p.y),Math.round(p.z),type);
    inventory[type]--;
    drawHotbar();
  }
 }
});

// save/load
function saveWorld(){
 localStorage.setItem('world',JSON.stringify(Object.keys(blockMap)));
 localStorage.setItem('inv',JSON.stringify(inventory));
}

function loadWorld(){
 const data=JSON.parse(localStorage.getItem('world')||"[]");
 data.forEach(k=>{
  const [x,y,z]=k.split(',').map(Number);
  addBlock(x,y,z,'dirt');
 });
 inventory=JSON.parse(localStorage.getItem('inv')||"{}");
 drawHotbar();
}

setInterval(saveWorld,5000);
loadWorld();

// loop
function animate(){
 requestAnimationFrame(animate);
 move();
 updateChunks();

 if(breaking){
  breakTime+=0.02*toolSpeed[currentTool];
  if(breakTime>1){
    removeBlock(breaking);
    inventory.dirt++;
    drawHotbar();
    breaking=null;
  }
 }

 time+=0.001;
 sun.position.set(Math.sin(time)*100,Math.cos(time)*100,0);

 renderer.render(scene,camera);
}
animate();

addEventListener('resize',()=>{
 camera.aspect=innerWidth/innerHeight;
 camera.updateProjectionMatrix();
 renderer.setSize(innerWidth,innerHeight);
});
</script>
</body>
</html>
