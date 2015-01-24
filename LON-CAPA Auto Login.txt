// ==UserScript==
// @name        LON-CAPA Auto-Login
// @namespace   loncapa
// @include https://loncapa.physics.mcmaster.ca/adm/roles
// @include https://loncapa.physics.mcmaster.ca
// @description Auto-Login for LON-CAPA
// @version     1.0
// @grant       none
// ==/UserScript==

// See Tutorial Video for Usage Instructions

//Current System Time (Milliseconds)
var curSysMillis = Math.round((new Date().getTime())/1000)

//Set LON-CAPA Username
$('#uname').val('MacID');

//Cycle Through Potential Password Field IDs (Field ID Dynamically Changes Based on Server Time)
for (var timeDisc = curSysMillis+10; timeDisc > curSysMillis-30;timeDisc--){
    //Guess Password Field ID
    var passID = '#upass' + timeDisc;
    //Set LON-CAPA Password
    $(passID).val('Student Number');
}

//Click "Log in"
buttonClick('input', 'submit', true, 'Log in');

//Select "PHYSICS 1E03" after Estimated Load Time
setTimeout(function() {
    buttonClick('input', 'button', false, 'stmacphys3848821ce41a85498macphys1');
}, 300); //Increase if Red Error Message Appears

setTimeout(function() {
    //GOTO "Course Contents" Page
    window.location.href = 'https://loncapa.physics.mcmaster.ca/adm/navmaps'
}, 1000); //Decrease if "Practice Assignment" is Expanded
          //Increase if Other Errors Appear

//Clicks Paramaterized Button
function buttonClick(eleTagName, eleType, eleIf, eleValue){
    
    //Get Matching Page Elements
    var buttons = document.getElementsByTagName(eleTagName);

    //Cycle Through Potential Elements
    for(var i = 0; i < buttons.length; i++) {
        
       if (eleIf){ //Current Element is Correct (Based on Value)
          if(buttons[i].type == eleType && buttons[i].value == eleValue)
          {
              //Click button and exit
              buttons[i].click();
              break;
          }
       } else { //Current Element is Correct (Based on Name)
          if(buttons[i].type == eleType && buttons[i].name == eleValue)
          {
              //Click Button and Exit
              buttons[i].click();
              break;
          }           
       }       
    }
}