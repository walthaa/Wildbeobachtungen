var C="wildbeobachtung-v1";
var SHELL=["./","index.html","https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.js","https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.css"];
self.addEventListener("install",function(e){
 e.waitUntil(caches.open(C).then(function(c){return Promise.all(SHELL.map(function(u){return c.add(u).catch(function(){})}))}));
 self.skipWaiting();
});
self.addEventListener("activate",function(e){
 e.waitUntil(caches.keys().then(function(k){return Promise.all(k.filter(function(n){return n!==C}).map(function(n){return caches.delete(n)}))}));
 self.clients.claim();
});
self.addEventListener("fetch",function(e){
 var r=e.request;if(r.method!=="GET")return;
 var same=new URL(r.url).origin===location.origin;
 e.respondWith(caches.open(C).then(function(c){
  var net=function(){return fetch(r).then(function(res){if(res&&(res.ok||res.type==="opaque"))c.put(r,res.clone());return res})};
  if(same)return net().catch(function(){return c.match(r)});
  return c.match(r).then(function(h){return h||net()});
 }));
});
