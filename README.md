<html>
 <head> 
  <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
  <style>
   body{
  background-color:#DFD7F3;
  margin:10px;
}
h1{
  border:2px solid black;
  width:200px;
  margin:10px;
}
h2{
  margin-left:20px;
}
header{
  text-align:center;
  font-size:200%;
  font-family: Times New Roman;
  border:2px solid black;
}
.img1{
 height:30px;
 width:40px;
}
.img2{
  display:flex;
  flex-wrap:wrap;
  width:100%;
  height:900px;
}
.card{
  display:flex;
  flex-wrap:wrap;
  border:2px solid black;
}
.details{
  display:flex;
  flex-wrap:wrap;
 justify-content: flex-start;
}
.totalC{
  font-size:150%;
  box-shadow:2px 2px 0px 2px grey;
  background-color:white;
  border-radius:5px;
  line-height:50px;
  margin:20px;
}
.sh
{
  border:2px solid black;
  border-radius:5px;
  background-color:white;
  box-shadow:2px 2px 2px 1px grey;
  font-size:200%;
  width:340px;
  margin:10px;
}
#blink{
color:red;
}
.state1
{
 
}
.sec{
 
  
 
}
#state{
 font-size:180%;
 box-shadow:2px 2px 2px 2px grey;
 border-radius:10px;
 width:350px;
 display:block;
 margin-left:auto;
 margin-right:auto;
}
.btn
{
 font-size:150%;
 box-shadow:2px 2px 2px 2px grey;
 border-radius:10px;
 display:inline;
 margin-left:30%;
 margin-top:20px;
}
.rbtn
{
 font-size:150%;
 box-shadow:2px 2px 2px 2px grey;
 border-radius:10px;
 display:inline;
 margin-left:25%;
 margin-top:20px;
 margin-bottom:10px;
}

 

.stateC
{
  margin-left:auto;
  margin-right:auto;
  font-size:130%;
  box-shadow:2px 2px 2px 2px grey;
  border-radius:10px;
  background-color:white;
  width:100%;
  text-align:center;
}
.simg{
  display:flex;
  flex-wrap:wrap;
  justify-content:space-around;
}
  footer{
   font-size:150%;
   text-align:center;
   border:2px solid black;
   border-radius:10px;
   margin:10px;
 }  
 </style> 
 </head> 
 <body> 
  <header> 
   <img class="img1" src="corona.jpeg" alt="corona">Covid-19 Tracker 
  </header> 
  <form> 
   <select id="state"></select>
  </form> 
  <blink id="blink"> 
   <i>Note: If you want to see another state details, please hit to default button.</i> 
  </blink> 
  <button id="btn" onclick="sta(this)">Submit</button> 
  <button id="rbtn" onclick="remove()">To default</button>
 <script>
    fetch('https://api.rootnet.in/covid19-in/stats/latest').then((response)=>
    {
      return response.json();
    }) 
    .then((datas) =>
      {
      // console.log(data);
   
   var body =document.body;
  
   var img2=document.createElement("img");
   img2.classList.add("img2");
   img2.setAttribute("src","covid.jpg");
   body.append(img2);
  
   var h1=document.createElement("h1");
   h1.textContent="In India";
   body.append(h1);
   var card=document.createElement("div");
   card.classList.add("card");
   body.append(card);
   
   var time=document.createElement("h2");
   time.textContent="Last updated: "+new Date();
   card.append(time);
   
   var details=document.createElement("div");
   details.classList.add("details");
   card.append(details);
   
   var totalC=document.createElement("p");
   totalC.textContent="Total Confirmed: "+datas.data.summary.total;
   totalC.classList.add("totalC");
   details.append(totalC);
   var totalD=document.createElement("p");
   totalD.textContent="Total Deaths: "+datas.data.summary.deaths;
   totalD.classList.add("totalC");
   details.append(totalD);
   var totalR=document.createElement("p");
   totalR.textContent="Total Recovered: "+datas.data.summary.discharged;
   totalR.classList.add("totalC");
   details.append(totalR);
   var cI=document.createElement("p");
   cI.textContent="Confirmed Indian Cases: "+datas.data.summary.confirmedCasesIndian;
   cI.classList.add("totalC");
   details.append(cI);
   var fC=document.createElement("p");
   fC.textContent="Confirmed Foreign Cases: "+datas.data.summary.confirmedCasesForeign;
   fC.classList.add("totalC");
   details.append(fC);
   
   var state=document.createElement("div");
   state.classList.add("state1");
   body.append(state);
   
   var sh=document.createElement("p");
   sh.textContent="For State Wise Details: ";
   sh.classList.add("sh");
   state.append(sh);
   
   var blink=document.getElementById("blink");
   state.append(blink);
  
   sec=document.createElement("div");
   sec.classList.add("sec");
   state.append(sec);
  
   (function() {
        drop = document.getElementById('state');
        df = document.createDocumentFragment();
    for (var j = 0; j<datas.data.regional.length; j++) {
        var option = document.createElement('option');
        option.value =datas.data.regional[j].loc;
        option.appendChild(document.createTextNode(option.value));
        df.appendChild(option);
    }
    drop.appendChild(df);
   }());
   sec.append(drop);
   
   btn=document.getElementById("btn");
  btn.classList.add("btn");
  sec.append(btn);
   
   rbtn=document.getElementById("rbtn");
   rbtn.classList.add("rbtn");
   sec.append(rbtn);
   
   stateC=document.createElement("div");
   stateC.classList.add("stateC");
   sec.append(stateC);
   
   simg=document.createElement("div");
   simg.classList.add("simg");
   stateC.append(simg);
  
  var footer = document.createElement("footer"); 
  footer.textContent="All copy rights reserved";
  body.append(footer);
  });
  
  function sta(b){

    fetch('https://api.rootnet.in/covid19-in/stats/latest').then((sresponse)=>
    {
      return sresponse.json();
    }) 
    .then((sdata) =>
      {
   //  console.log(sdata);
      var result=drop.options[drop.selectedIndex].value;
     
     for(var i=0;i<sdata.data.regional.length;i++)
      {
       res=sdata.data.regional[i].loc;
      if(result==res)
      {
      loc=document.createElement("p");
      loc.innerHTML+="State: "+sdata.data.regional[i].loc;
      stateC.append(loc);
      
      stC=document.createElement("p");
      stC.innerHTML+="Total Confirmed: "+sdata.data.regional[i].totalConfirmed;
      stateC.append(stC);
      
      stD=document.createElement("p");
      stD.innerHTML+="Total Deaths: "+sdata.data.regional[i].deaths;
      stateC.append(stD);
      
      stR=document.createElement("p");
      stR.innerHTML+="Recovered: "+sdata.data.regional[i].discharged;
      stateC.append(stR);
      
      sImg=document.createElement("img");
      sImg.setAttribute("src","state"+i+".jpeg");
      sImg.setAttribute("width","200px;");
      sImg.setAttribute("height","200px");
      sImg.setAttribute("alt",sdata.data.regional[i].loc);
      simg.append(sImg);
       }
     }
   });
   } 
 function remove()
  {
    stateC.removeChild(loc);
    stateC.removeChild(stC);
    stateC.removeChild(stD);
    stateC.removeChild(stR);
    simg.removeChild(sImg);
  }
  
 </script> 
 </body>
</html>
