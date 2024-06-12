![image](https://github.com/SAYNANE/Text-to-handwritten-/assets/141496895/5593ec14-ba55-414d-bb33-19fe7eb05c8e)# Text-to-handwritten-
javascript
"#content-writing").on("paste", function (e) {    
e.preventDefault();    
var text = (e.originalEvent || e).clipboardData.getData("text/plain");    document.execCommand("insertHTML", false, text);});
let oldFont = "gloria-hallelujah";function changePageStyle(font, fontsize, textColor, wordSpacing, letterSpacing, lineHeight) 
{    
if (font != '') {       
changeFont(font);   
} 
else if (fontsize != '') {        
$("#content-writing").css("font-size", fontsize);        
$(".selected-size").text(fontsize);    } else if (textColor != ‘’) 
{        $("#content-writing").css("color", textColor);       
$(".select-color-box").css("background-color", textColor);    } 
else if (wordSpacing != '') {        
$("#content-writing").css("letter-spacing", wordSpacing);        
$(".selected-spacing").text(wordSpacing);    } 
else if (letterSpacing != '') {        
$("#content-writing").css("word-spacing", letterSpacing);        
$(".letter-spacing").text(letterSpacing);    } 
else if (lineHeight != '') {        
$("#content-writing").css("line-height", lineHeight);        
$(".line-height-selected").text(lineHeight);    }    
$(".handwriting-list").addClass("d-none");}
function changeFont(font) 
{   
 $("#content-writing").removeClass(oldFont);    
$("#content-writing").addClass(font);    
$(".selected-hand").removeClass(oldFont);    
$(".selected-hand").addClass(font);    oldFont = font;
}
function changePageImage(imageSrc) {    
$("#main-image").attr("src", imageSrc);    
$(".handwriting-list").addClass("d-none");}
$(document).ready(function () 
{    
var result2 = []; 
var charsPerPage = 850; 
{        if (result2.length !== 0) {           
var pagenum = pageNum - 1;            
pagenum = (pagenum < 0) ? (result2.length - 1) : pagenum;            $('.body').html(result2[pagenum]);            
$('.body').attr('data-page', pagenum);            
$('#currPage').text(pageNum);       
 }    }

function splitIntoPages(text) {        
var myRe = /\S[\s\S]{0,850}\S(?=\s|$)/g;        
var m;        
var pages = [];        
while ((m = myRe.exec(text)) !== null) {            
pages.push(m[0]);        }        
return pages;    }

 $("#nxtBtn").click(function () {        
var currentPage = +$('#currPage').text();        
var totalPages = +$('#totpages').text();        
var nextPage = (currentPage % totalPages) + 1;

 if (currentPage === totalPages) {            
result2=result2.concat(splitIntoPages($('#notes').val()));            
$('#totpages').text(result2.length);        }       
updateContent(nextPage);    });

 $("#prevBtn").click(function () {       
 var currentPage = +$('#currPage').text();        
var totalPages = +$('#totpages').text();        
var prevPage = ((currentPage - 2 + totalPages) % totalPages) + 1;
if (currentPage === 1) {            
updateContent(totalPages);        }
 else {            
updateContent(prevPage);        
}    });

 result2 = splitIntoPages($('#notes').val());    
$('#totpages').text(result2.length);    
 updateContent(1);});let arr = [];
$(".content-writing-div").keyup(function () {    
var maxHeight = $("#main-image").height();   
var page_end = $(".content-writing-div").height();    
var text = $(".content-writing-div").html();    
console.log(5/page_end * 100) 

if (page_end > maxHeight) {
var words = text.split(' ');        
var currentText = "";
for (var i = 1; i < words.length; i++) {
if (currentText.length + words[i].length <= page_end * (15/page_end * 100)) 
{                
currentText += words[i] + ' ';            
} else {
arr.push(currentText.trim
currentText = words[i] + ' ‘;  
}       
}
if (currentText.trim() !== "") {            
arr.push(currentText.trim());        } 
$(".content-writing-div").html("");   
}



