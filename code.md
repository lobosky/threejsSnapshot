/*** ADDING SCREENSHOTTING ABILITY ***/


//add a style to your css

<style> 

#imgBox {
	border :2px solid #ddd;
	border-radius: 15px;
	
	position: absolute;
	top:10px;
	left:10px;
	padding:6px;
	background-color:#026;
	text-align: center;
	z-index:1;
	font-color:#ddd;
	display:none;

}
#imgBox .img {
	width:95%;
	height:95%;
	margin-top:10px;

}
#imgBox a{
   color:#ddd;
   text-decoration: none;

</style>

//add a box to your html file. 

<div id="imgBox"></div>


/*Author Mauro Lobosky Donadello
 mauro.donadello@ifom.eu
 MIT License
 takeSnapshot(e)  -> e = event
 in my case is mapped to a click on icon, 
*/

function takeSnapshot(e){

    var imgData, imgNode;
    var boxId = 'imgBox';
    var downloadFileName = 'imaging_scene.png';
    var thisDebug = false;

    var keyClick = 80; // p key on the keyboard
	

	if(e.keyCode == keyClick){  
    	try {
	        imgData = renderer.domElement.toDataURL();      
	   		thisDebug && console.log("takeSnapshot imgData:" + imgData);
	    } 
	    catch(e) {
	        waitMessage("Browser does not support taking screenshot of 3d context");
	        return;
	    }

	}else{
		return ; 	
	}
  	//remove the contents of imgbox in already populated
  	if(box = document.getElementById(boxId)){
    	while(box.hasChildNodes()){
	 		box.removeChild(box.lastChild);
	  }
  	}
   //create the html juice to fill imgBox
   var link = document.createElement('a');
	link.innerHTML = 'click here to download';
	link.href = imgData;
    link.download = downloadFileName;

   imgNode = document.createElement("img");
   imgNode.src = imgData;
   //imgNode.height= window.innerHeight/10;
   //imgNode.width=window.innerWidth / 10;
   imgNode.alt=downloadFileName;
   imgNode.id="snapshot";
   box.appendChild(imgNode);
   box.appendChild(link);
   box.style.height = rendererHeight / 8 + 40 +  "px";
   box.style.width = rendererWidth /8 + 10 + "px";

    //box.style.width((window.innerWidth/16)+100);
    if(document.getElementById('snapshot')){       
       img = document.getElementById("snapshot");
       img.style.height =  rendererHeight /8   + "px";
       img.style.width = rendererWidth /8 + 10 +  "px";
	}

 box.style.display = 'block';

 //<a href="#" class="button" id="btn-download" download="my-file-name.png">Download</a>
}

//add an eventListener
window.addEventListener("keyup", takeSnapshot,false);


