<!DOCTYPE html>
<html>
<head>

<title>MY APPLICATION</title>
<link rel="stylesheet" href="css/html5demos.css">
<script src="js/h5utils.js"></script>

</head>

<body>

<center>

<div id="clockbox"></div>

<p id="demo"></p>

<script type="text/javascript" src="http://maps.google.com/maps/api/js?sensor=false"></script>

	<article>
      <p>Your current location is: <span id="status">checking...</span></p>
    </article>
	
<button type="button" onclick="alert('You Have Punched IN!')">IN</button>
	
<button type="button" onclick="alert('You Have Punched OUT!')">OUT</button>
	
<center>
	
</script>


<script type="text/javascript">

tday=new Array("Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday");
tmonth=new Array("January","February","March","April","May","June","July","August","September","October","November","December");

function GetClock(){
var d=new Date();
var nday=d.getDay(),nmonth=d.getMonth(),ndate=d.getDate(),nyear=d.getYear(),nhour=d.getHours(),nmin=d.getMinutes(),ap;
     if(nhour==0){ap=" AM";nhour=12;}
else if(nhour<12){ap=" AM";}
else if(nhour==12){ap=" PM";}
else if(nhour>12){ap=" PM";nhour-=12;}

if(nyear<1000) nyear+=1900;
if(nmin<=9) nmin="0"+nmin;

document.getElementById('clockbox').innerHTML=""+tday[nday]+", "+tmonth[nmonth]+" "+ndate+", "+nyear+" "+nhour+":"+nmin+ap+"";
}

window.onload=function(){
GetClock();
setInterval(GetClock,1000);
}


function success(position) {
  var s = document.querySelector('#status');
  
  if (s.className == 'success') {
    // not sure why we're hitting this twice in FF, I think it's to do with a cached result coming back    
    return;
  }
  
  s.innerHTML = "HERE!";
  s.className = 'success';
  
  var mapcanvas = document.createElement('div');
  mapcanvas.id = 'mapcanvas';
  mapcanvas.style.height = '400px';
  mapcanvas.style.width = '560px';
    
  document.querySelector('article').appendChild(mapcanvas);
  
  var latlng = new google.maps.LatLng(position.coords.latitude, position.coords.longitude);
  var myOptions = {
    zoom: 15,
    center: latlng,
    mapTypeControl: false,
    navigationControlOptions: {style: google.maps.NavigationControlStyle.SMALL},
    mapTypeId: google.maps.MapTypeId.ROADMAP
  };
  var map = new google.maps.Map(document.getElementById("mapcanvas"), myOptions);
  
  var marker = new google.maps.Marker({
      position: latlng, 
      map: map, 
      title:"You are here! (at least within a "+position.coords.accuracy+" meter radius)"
  });
}

function error(msg) {
  var s = document.querySelector('#status');
  s.innerHTML = typeof msg == 'string' ? msg : "failed";
  s.className = 'fail';
  
  // console.log(arguments);
}

if (navigator.geolocation) {
  navigator.geolocation.getCurrentPosition(success, error);
} else {
  error('not supported');
}


var gaJsHost = (("https:" == document.location.protocol) ? "https://ssl." : "http://www.");
document.write(unescape("%3Cscript src='" + gaJsHost + "google-analytics.com/ga.js' type='text/javascript'%3E%3C/script%3E"));


try {
var pageTracker = _gat._getTracker("UA-1656750-18");
pageTracker._trackPageview();
} catch(err) {} </script>

</body>

</html>
