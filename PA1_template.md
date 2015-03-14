<!DOCTYPE html>
<!-- saved from url=(0014)about:internet -->
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
<meta http-equiv="x-ua-compatible" content="IE=9" >

<title>Loading and preprocessing the data</title>

<style type="text/css">
body, td {
   font-family: sans-serif;
   background-color: white;
   font-size: 12px;
   margin: 8px;
}

tt, code, pre {
   font-family: 'DejaVu Sans Mono', 'Droid Sans Mono', 'Lucida Console', Consolas, Monaco, monospace;
}

h1 { 
   font-size:2.2em; 
}

h2 { 
   font-size:1.8em; 
}

h3 { 
   font-size:1.4em; 
}

h4 { 
   font-size:1.0em; 
}

h5 { 
   font-size:0.9em; 
}

h6 { 
   font-size:0.8em; 
}

a:visited {
   color: rgb(50%, 0%, 50%);
}

pre {	
   margin-top: 0;
   max-width: 95%;
   border: 1px solid #ccc;
   white-space: pre-wrap;
}

pre code {
   display: block; padding: 0.5em;
}

code.r, code.cpp {
   background-color: #F8F8F8;
}

table, td, th {
  border: none;
}

blockquote {
   color:#666666;
   margin:0;
   padding-left: 1em;
   border-left: 0.5em #EEE solid;
}

hr {
   height: 0px;
   border-bottom: none;
   border-top-width: thin;
   border-top-style: dotted;
   border-top-color: #999999;
}

@media print {
   * { 
      background: transparent !important; 
      color: black !important; 
      filter:none !important; 
      -ms-filter: none !important; 
   }

   body { 
      font-size:12pt; 
      max-width:100%; 
   }
       
   a, a:visited { 
      text-decoration: underline; 
   }

   hr { 
      visibility: hidden;
      page-break-before: always;
   }

   pre, blockquote { 
      padding-right: 1em; 
      page-break-inside: avoid; 
   }

   tr, img { 
      page-break-inside: avoid; 
   }

   img { 
      max-width: 100% !important; 
   }

   @page :left { 
      margin: 15mm 20mm 15mm 10mm; 
   }
     
   @page :right { 
      margin: 15mm 10mm 15mm 20mm; 
   }

   p, h2, h3 { 
      orphans: 3; widows: 3; 
   }

   h2, h3 { 
      page-break-after: avoid; 
   }
}

</style>

<!-- Styles for R syntax highlighter -->
<style type="text/css">
   pre .operator,
   pre .paren {
     color: rgb(104, 118, 135)
   }

   pre .literal {
     color: rgb(88, 72, 246)
   }

   pre .number {
     color: rgb(0, 0, 205);
   }

   pre .comment {
     color: rgb(76, 136, 107);
   }

   pre .keyword {
     color: rgb(0, 0, 255);
   }

   pre .identifier {
     color: rgb(0, 0, 0);
   }

   pre .string {
     color: rgb(3, 106, 7);
   }
</style>

<!-- R syntax highlighter -->
<script type="text/javascript">
var hljs=new function(){function m(p){return p.replace(/&/gm,"&amp;").replace(/</gm,"&lt;")}function f(r,q,p){return RegExp(q,"m"+(r.cI?"i":"")+(p?"g":""))}function b(r){for(var p=0;p<r.childNodes.length;p++){var q=r.childNodes[p];if(q.nodeName=="CODE"){return q}if(!(q.nodeType==3&&q.nodeValue.match(/\s+/))){break}}}function h(t,s){var p="";for(var r=0;r<t.childNodes.length;r++){if(t.childNodes[r].nodeType==3){var q=t.childNodes[r].nodeValue;if(s){q=q.replace(/\n/g,"")}p+=q}else{if(t.childNodes[r].nodeName=="BR"){p+="\n"}else{p+=h(t.childNodes[r])}}}if(/MSIE [678]/.test(navigator.userAgent)){p=p.replace(/\r/g,"\n")}return p}function a(s){var r=s.className.split(/\s+/);r=r.concat(s.parentNode.className.split(/\s+/));for(var q=0;q<r.length;q++){var p=r[q].replace(/^language-/,"");if(e[p]){return p}}}function c(q){var p=[];(function(s,t){for(var r=0;r<s.childNodes.length;r++){if(s.childNodes[r].nodeType==3){t+=s.childNodes[r].nodeValue.length}else{if(s.childNodes[r].nodeName=="BR"){t+=1}else{if(s.childNodes[r].nodeType==1){p.push({event:"start",offset:t,node:s.childNodes[r]});t=arguments.callee(s.childNodes[r],t);p.push({event:"stop",offset:t,node:s.childNodes[r]})}}}}return t})(q,0);return p}function k(y,w,x){var q=0;var z="";var s=[];function u(){if(y.length&&w.length){if(y[0].offset!=w[0].offset){return(y[0].offset<w[0].offset)?y:w}else{return w[0].event=="start"?y:w}}else{return y.length?y:w}}function t(D){var A="<"+D.nodeName.toLowerCase();for(var B=0;B<D.attributes.length;B++){var C=D.attributes[B];A+=" "+C.nodeName.toLowerCase();if(C.value!==undefined&&C.value!==false&&C.value!==null){A+='="'+m(C.value)+'"'}}return A+">"}while(y.length||w.length){var v=u().splice(0,1)[0];z+=m(x.substr(q,v.offset-q));q=v.offset;if(v.event=="start"){z+=t(v.node);s.push(v.node)}else{if(v.event=="stop"){var p,r=s.length;do{r--;p=s[r];z+=("</"+p.nodeName.toLowerCase()+">")}while(p!=v.node);s.splice(r,1);while(r<s.length){z+=t(s[r]);r++}}}}return z+m(x.substr(q))}function j(){function q(x,y,v){if(x.compiled){return}var u;var s=[];if(x.k){x.lR=f(y,x.l||hljs.IR,true);for(var w in x.k){if(!x.k.hasOwnProperty(w)){continue}if(x.k[w] instanceof Object){u=x.k[w]}else{u=x.k;w="keyword"}for(var r in u){if(!u.hasOwnProperty(r)){continue}x.k[r]=[w,u[r]];s.push(r)}}}if(!v){if(x.bWK){x.b="\\b("+s.join("|")+")\\s"}x.bR=f(y,x.b?x.b:"\\B|\\b");if(!x.e&&!x.eW){x.e="\\B|\\b"}if(x.e){x.eR=f(y,x.e)}}if(x.i){x.iR=f(y,x.i)}if(x.r===undefined){x.r=1}if(!x.c){x.c=[]}x.compiled=true;for(var t=0;t<x.c.length;t++){if(x.c[t]=="self"){x.c[t]=x}q(x.c[t],y,false)}if(x.starts){q(x.starts,y,false)}}for(var p in e){if(!e.hasOwnProperty(p)){continue}q(e[p].dM,e[p],true)}}function d(B,C){if(!j.called){j();j.called=true}function q(r,M){for(var L=0;L<M.c.length;L++){if((M.c[L].bR.exec(r)||[null])[0]==r){return M.c[L]}}}function v(L,r){if(D[L].e&&D[L].eR.test(r)){return 1}if(D[L].eW){var M=v(L-1,r);return M?M+1:0}return 0}function w(r,L){return L.i&&L.iR.test(r)}function K(N,O){var M=[];for(var L=0;L<N.c.length;L++){M.push(N.c[L].b)}var r=D.length-1;do{if(D[r].e){M.push(D[r].e)}r--}while(D[r+1].eW);if(N.i){M.push(N.i)}return f(O,M.join("|"),true)}function p(M,L){var N=D[D.length-1];if(!N.t){N.t=K(N,E)}N.t.lastIndex=L;var r=N.t.exec(M);return r?[M.substr(L,r.index-L),r[0],false]:[M.substr(L),"",true]}function z(N,r){var L=E.cI?r[0].toLowerCase():r[0];var M=N.k[L];if(M&&M instanceof Array){return M}return false}function F(L,P){L=m(L);if(!P.k){return L}var r="";var O=0;P.lR.lastIndex=0;var M=P.lR.exec(L);while(M){r+=L.substr(O,M.index-O);var N=z(P,M);if(N){x+=N[1];r+='<span class="'+N[0]+'">'+M[0]+"</span>"}else{r+=M[0]}O=P.lR.lastIndex;M=P.lR.exec(L)}return r+L.substr(O,L.length-O)}function J(L,M){if(M.sL&&e[M.sL]){var r=d(M.sL,L);x+=r.keyword_count;return r.value}else{return F(L,M)}}function I(M,r){var L=M.cN?'<span class="'+M.cN+'">':"";if(M.rB){y+=L;M.buffer=""}else{if(M.eB){y+=m(r)+L;M.buffer=""}else{y+=L;M.buffer=r}}D.push(M);A+=M.r}function G(N,M,Q){var R=D[D.length-1];if(Q){y+=J(R.buffer+N,R);return false}var P=q(M,R);if(P){y+=J(R.buffer+N,R);I(P,M);return P.rB}var L=v(D.length-1,M);if(L){var O=R.cN?"</span>":"";if(R.rE){y+=J(R.buffer+N,R)+O}else{if(R.eE){y+=J(R.buffer+N,R)+O+m(M)}else{y+=J(R.buffer+N+M,R)+O}}while(L>1){O=D[D.length-2].cN?"</span>":"";y+=O;L--;D.length--}var r=D[D.length-1];D.length--;D[D.length-1].buffer="";if(r.starts){I(r.starts,"")}return R.rE}if(w(M,R)){throw"Illegal"}}var E=e[B];var D=[E.dM];var A=0;var x=0;var y="";try{var s,u=0;E.dM.buffer="";do{s=p(C,u);var t=G(s[0],s[1],s[2]);u+=s[0].length;if(!t){u+=s[1].length}}while(!s[2]);if(D.length>1){throw"Illegal"}return{r:A,keyword_count:x,value:y}}catch(H){if(H=="Illegal"){return{r:0,keyword_count:0,value:m(C)}}else{throw H}}}function g(t){var p={keyword_count:0,r:0,value:m(t)};var r=p;for(var q in e){if(!e.hasOwnProperty(q)){continue}var s=d(q,t);s.language=q;if(s.keyword_count+s.r>r.keyword_count+r.r){r=s}if(s.keyword_count+s.r>p.keyword_count+p.r){r=p;p=s}}if(r.language){p.second_best=r}return p}function i(r,q,p){if(q){r=r.replace(/^((<[^>]+>|\t)+)/gm,function(t,w,v,u){return w.replace(/\t/g,q)})}if(p){r=r.replace(/\n/g,"<br>")}return r}function n(t,w,r){var x=h(t,r);var v=a(t);var y,s;if(v){y=d(v,x)}else{return}var q=c(t);if(q.length){s=document.createElement("pre");s.innerHTML=y.value;y.value=k(q,c(s),x)}y.value=i(y.value,w,r);var u=t.className;if(!u.match("(\\s|^)(language-)?"+v+"(\\s|$)")){u=u?(u+" "+v):v}if(/MSIE [678]/.test(navigator.userAgent)&&t.tagName=="CODE"&&t.parentNode.tagName=="PRE"){s=t.parentNode;var p=document.createElement("div");p.innerHTML="<pre><code>"+y.value+"</code></pre>";t=p.firstChild.firstChild;p.firstChild.cN=s.cN;s.parentNode.replaceChild(p.firstChild,s)}else{t.innerHTML=y.value}t.className=u;t.result={language:v,kw:y.keyword_count,re:y.r};if(y.second_best){t.second_best={language:y.second_best.language,kw:y.second_best.keyword_count,re:y.second_best.r}}}function o(){if(o.called){return}o.called=true;var r=document.getElementsByTagName("pre");for(var p=0;p<r.length;p++){var q=b(r[p]);if(q){n(q,hljs.tabReplace)}}}function l(){if(window.addEventListener){window.addEventListener("DOMContentLoaded",o,false);window.addEventListener("load",o,false)}else{if(window.attachEvent){window.attachEvent("onload",o)}else{window.onload=o}}}var e={};this.LANGUAGES=e;this.highlight=d;this.highlightAuto=g;this.fixMarkup=i;this.highlightBlock=n;this.initHighlighting=o;this.initHighlightingOnLoad=l;this.IR="[a-zA-Z][a-zA-Z0-9_]*";this.UIR="[a-zA-Z_][a-zA-Z0-9_]*";this.NR="\\b\\d+(\\.\\d+)?";this.CNR="\\b(0[xX][a-fA-F0-9]+|(\\d+(\\.\\d*)?|\\.\\d+)([eE][-+]?\\d+)?)";this.BNR="\\b(0b[01]+)";this.RSR="!|!=|!==|%|%=|&|&&|&=|\\*|\\*=|\\+|\\+=|,|\\.|-|-=|/|/=|:|;|<|<<|<<=|<=|=|==|===|>|>=|>>|>>=|>>>|>>>=|\\?|\\[|\\{|\\(|\\^|\\^=|\\||\\|=|\\|\\||~";this.ER="(?![\\s\\S])";this.BE={b:"\\\\.",r:0};this.ASM={cN:"string",b:"'",e:"'",i:"\\n",c:[this.BE],r:0};this.QSM={cN:"string",b:'"',e:'"',i:"\\n",c:[this.BE],r:0};this.CLCM={cN:"comment",b:"//",e:"$"};this.CBLCLM={cN:"comment",b:"/\\*",e:"\\*/"};this.HCM={cN:"comment",b:"#",e:"$"};this.NM={cN:"number",b:this.NR,r:0};this.CNM={cN:"number",b:this.CNR,r:0};this.BNM={cN:"number",b:this.BNR,r:0};this.inherit=function(r,s){var p={};for(var q in r){p[q]=r[q]}if(s){for(var q in s){p[q]=s[q]}}return p}}();hljs.LANGUAGES.cpp=function(){var a={keyword:{"false":1,"int":1,"float":1,"while":1,"private":1,"char":1,"catch":1,"export":1,virtual:1,operator:2,sizeof:2,dynamic_cast:2,typedef:2,const_cast:2,"const":1,struct:1,"for":1,static_cast:2,union:1,namespace:1,unsigned:1,"long":1,"throw":1,"volatile":2,"static":1,"protected":1,bool:1,template:1,mutable:1,"if":1,"public":1,friend:2,"do":1,"return":1,"goto":1,auto:1,"void":2,"enum":1,"else":1,"break":1,"new":1,extern:1,using:1,"true":1,"class":1,asm:1,"case":1,typeid:1,"short":1,reinterpret_cast:2,"default":1,"double":1,register:1,explicit:1,signed:1,typename:1,"try":1,"this":1,"switch":1,"continue":1,wchar_t:1,inline:1,"delete":1,alignof:1,char16_t:1,char32_t:1,constexpr:1,decltype:1,noexcept:1,nullptr:1,static_assert:1,thread_local:1,restrict:1,_Bool:1,complex:1},built_in:{std:1,string:1,cin:1,cout:1,cerr:1,clog:1,stringstream:1,istringstream:1,ostringstream:1,auto_ptr:1,deque:1,list:1,queue:1,stack:1,vector:1,map:1,set:1,bitset:1,multiset:1,multimap:1,unordered_set:1,unordered_map:1,unordered_multiset:1,unordered_multimap:1,array:1,shared_ptr:1}};return{dM:{k:a,i:"</",c:[hljs.CLCM,hljs.CBLCLM,hljs.QSM,{cN:"string",b:"'\\\\?.",e:"'",i:"."},{cN:"number",b:"\\b(\\d+(\\.\\d*)?|\\.\\d+)(u|U|l|L|ul|UL|f|F)"},hljs.CNM,{cN:"preprocessor",b:"#",e:"$"},{cN:"stl_container",b:"\\b(deque|list|queue|stack|vector|map|set|bitset|multiset|multimap|unordered_map|unordered_set|unordered_multiset|unordered_multimap|array)\\s*<",e:">",k:a,r:10,c:["self"]}]}}}();hljs.LANGUAGES.r={dM:{c:[hljs.HCM,{cN:"number",b:"\\b0[xX][0-9a-fA-F]+[Li]?\\b",e:hljs.IMMEDIATE_RE,r:0},{cN:"number",b:"\\b\\d+(?:[eE][+\\-]?\\d*)?L\\b",e:hljs.IMMEDIATE_RE,r:0},{cN:"number",b:"\\b\\d+\\.(?!\\d)(?:i\\b)?",e:hljs.IMMEDIATE_RE,r:1},{cN:"number",b:"\\b\\d+(?:\\.\\d*)?(?:[eE][+\\-]?\\d*)?i?\\b",e:hljs.IMMEDIATE_RE,r:0},{cN:"number",b:"\\.\\d+(?:[eE][+\\-]?\\d*)?i?\\b",e:hljs.IMMEDIATE_RE,r:1},{cN:"keyword",b:"(?:tryCatch|library|setGeneric|setGroupGeneric)\\b",e:hljs.IMMEDIATE_RE,r:10},{cN:"keyword",b:"\\.\\.\\.",e:hljs.IMMEDIATE_RE,r:10},{cN:"keyword",b:"\\.\\.\\d+(?![\\w.])",e:hljs.IMMEDIATE_RE,r:10},{cN:"keyword",b:"\\b(?:function)",e:hljs.IMMEDIATE_RE,r:2},{cN:"keyword",b:"(?:if|in|break|next|repeat|else|for|return|switch|while|try|stop|warning|require|attach|detach|source|setMethod|setClass)\\b",e:hljs.IMMEDIATE_RE,r:1},{cN:"literal",b:"(?:NA|NA_integer_|NA_real_|NA_character_|NA_complex_)\\b",e:hljs.IMMEDIATE_RE,r:10},{cN:"literal",b:"(?:NULL|TRUE|FALSE|T|F|Inf|NaN)\\b",e:hljs.IMMEDIATE_RE,r:1},{cN:"identifier",b:"[a-zA-Z.][a-zA-Z0-9._]*\\b",e:hljs.IMMEDIATE_RE,r:0},{cN:"operator",b:"<\\-(?!\\s*\\d)",e:hljs.IMMEDIATE_RE,r:2},{cN:"operator",b:"\\->|<\\-",e:hljs.IMMEDIATE_RE,r:1},{cN:"operator",b:"%%|~",e:hljs.IMMEDIATE_RE},{cN:"operator",b:">=|<=|==|!=|\\|\\||&&|=|\\+|\\-|\\*|/|\\^|>|<|!|&|\\||\\$|:",e:hljs.IMMEDIATE_RE,r:0},{cN:"operator",b:"%",e:"%",i:"\\n",r:1},{cN:"identifier",b:"`",e:"`",r:0},{cN:"string",b:'"',e:'"',c:[hljs.BE],r:0},{cN:"string",b:"'",e:"'",c:[hljs.BE],r:0},{cN:"paren",b:"[[({\\])}]",e:hljs.IMMEDIATE_RE,r:0}]}};
hljs.initHighlightingOnLoad();
</script>




</head>

<body>
<h2>Loading and preprocessing the data</h2>

<pre><code class="r">unzip(&quot;activity.zip&quot;)
act&lt;-read.csv(&quot;activity.csv&quot;, header=TRUE, na.strings=&quot;NA&quot;)

library (lubridate) 
act$date&lt;-ymd(act$date)
summary(act)
</code></pre>

<pre><code>##      steps             date               interval     
##  Min.   :  0.00   Min.   :2012-10-01   Min.   :   0.0  
##  1st Qu.:  0.00   1st Qu.:2012-10-16   1st Qu.: 588.8  
##  Median :  0.00   Median :2012-10-31   Median :1177.5  
##  Mean   : 37.38   Mean   :2012-10-31   Mean   :1177.5  
##  3rd Qu.: 12.00   3rd Qu.:2012-11-15   3rd Qu.:1766.2  
##  Max.   :806.00   Max.   :2012-11-30   Max.   :2355.0  
##  NA&#39;s   :2304
</code></pre>

<h2>What is mean total number of steps taken per day?</h2>

<pre><code class="r">library(dplyr)
</code></pre>

<pre><code>## 
## Attaching package: &#39;dplyr&#39;
## 
## The following objects are masked from &#39;package:lubridate&#39;:
## 
##     intersect, setdiff, union
## 
## The following object is masked from &#39;package:stats&#39;:
## 
##     filter
## 
## The following objects are masked from &#39;package:base&#39;:
## 
##     intersect, setdiff, setequal, union
</code></pre>

<pre><code class="r">act1&lt;-act %&gt;%
  group_by(date) %&gt;%
  summarise(sum_steps=sum(steps, na.rm=TRUE))
mean_act1&lt;-mean(act1$sum_steps, na.rm=TRUE)  
median_act1&lt;-median(act1$sum_steps, na.rm=TRUE)  
hist(act1$sum_steps,
                main = &quot;Histogram of Total Steps Taken by Day&quot;,
                xlab = &quot;Total Steps per Day&quot;)
</code></pre>

<p><img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAfgAAAH4CAMAAACR9g9NAAAAkFBMVEUAAAAAADoAAGYAOjoAOmYAOpAAZpAAZrY6AAA6ADo6AGY6OgA6OmY6OpA6ZrY6kNtmAABmADpmAGZmOgBmOpBmZjpmZmZmtv+QOgCQOjqQOmaQkDqQtpCQ27aQ29uQ2/+2ZgC2Zjq2tma225C2/7a2/9u2///bkDrb/7bb/9vb////tmb/25D//7b//9v///8YJx1qAAAACXBIWXMAAAsSAAALEgHS3X78AAAQzUlEQVR4nO2dC5uiyBlG6d507N2kR2cvsWeyu202SbtpL/z/fxcKCsSxRETkLfjOeZ4ZL1hvVXGsAmyRJAWTJOoGgAbEGwXxRkG8URBvFMQbBfFGQbxREG8UxBsF8UZBvFEQbxTEGwXxRkG8URBvFMQbBfFGQbxREG8UxBsF8UZBvFEQb5Q4xO8Wj+9pun99fC/ulayWN4Run5OHt9TFJjmzYO6hwt0iSZ4+2tT6beJxo09ffbrU1ZVxS/duJDbxR0+vblozZelT8fXcSlrhYtam1t7EJ/NWPbkHsYnP72VjNXl8z1dvtm7XfgVljx//s3j62L8+/JKN5U32dDaiN8lfs+ff14fhU7w+L50P4NQN/vxebcks9eUrae412YP/1mpd5m36wzUm9Y0qW1wk1jKy1GWgVFo+cO3OntgUrotaN0n+jMuoLxyEGMUXw+Hpf4WClR9cua/vnt0KdEv/LF70sUlK/Hr2rw+Iry+Z+Uo+auLzt86+Xuu8HNzudUktsEisZ6xd6W9KFTNCFeFessq3PuXbLZtcyozawkGIRXzpzq0RPz6LSXf7nA+ph7ftc7au1vnIKedY92I3apwz9xL3XPX6+pSdJ54uKd5l1cD0b56i1qyAeyNmz85d85ZVo2qJtYx/P8/Tb0pt/NvER7gezMpp39e6LhpSdHoW2ibcjRjF549KBZvccraG8ju7Yqp/Kws58TM/1RbPVq8/Ef/tkqJ8bfu8Kqotas3xU3BWaF41qpZ4yHj4m4uslcrfY6V435f9azZPzXyHD+KLjNrCQYhF/Mk2PvEj85z4/DWV+MPboa34svzRjlk+3YfFV42qJR4yijfFcakT8en64Vc3MaT1qb7MqC0chCjFO1aVoNOp3q3+wsWp+LZTfVm+qnBd7tFXU72jmuqrRtUS6xnF/arUkXg/1VcHmPWduzKjtnAQYhRfDYLVmZ07t4I2SXjEV68/EV9fkszK8vWdu5Na/Z6ku1MtriXWM/KcQ6lj8X6/MLtX7Rkkfj+wzKgtHIQYxecO/HSej6vicC5bWeXhnFOcreS53wIcia9efyK+WpLn+vKHqf641lXpqjgWOyyuJ9Yz8mOxQ6mjqf6P8qOhw25p7nt56Edt4SDEIb41m0FHRRr+9KU766bPhhoX9s54xPtBMh+21l7FN4YNejA3JvHF1nDI2dDRp47ap4tXLrwDIxIPfYJ4oyDeKIg3CuKNgnijIN4oiDcK4o2CeKMg3iiINwrijYJ4oyDeKIg3CuKNgnijIN4oiDcK4o2CeKMg3iiINwrijYJ4oyDeKIg3CuKNgnijIN4oiDcK4o1iQXzSK+re9MRU+tFEr32cygqbSj+aQHyAqfSjCcQHmEo/mkB8gKn0ownEB5hKP5pAfICp9KMJxAeYSj+aQHyAqfSjCcQHmEo/mkB8gKn0ownEB5hKP5pAfICp9KMJxAeYSj+aQHyAqfSjCcQHmEo/mkB8gKn0ownEB5hKP5pAfICp9KMJxAeYSj+aQHyAqfSjCcQHmEo/mkB8gKn0ownEB5hKP5pAfICp9KMJxAeYSj+aQHyAqfSjCcQHmEo/mkB8gKn0ownEB5hKP5pAfICL/dj9+J7uFkny9DFEc+4C4gO0Ee/cp9tPQzTnLiA+QBvx25ePYuSPFMQHuCx+8fD7VzfiX0Y71yM+QIt+7F+TWbp5HO2AR3yIqfSjCcQH6NKPsf0OEOIDXO7H9jl5eAvu3I1lHSA+wMV+7F+X2b854u8RJqTVBzhpupoh/g5hQlqN+Iz1dz8gvvcwIZf7sVvM3c369HhuLOsA8QFu6cdY1gHiAyBeGSYE8cowIYhXhglBvDJMCOKVYUIQrwwTgnhlmBDEK8OEIF4ZJgTxyjAhiFeGCUG8MkwI4pVhQhCvDBOCeGWYEMQrw4QgXhkmBPHKMCGIV4YJQbwyTAjilWFCEK8ME4J4ZZgQxCvDhCBeGSYE8cowIYhXhglBvDJMCOKVYUIQrwwTgnhlmBDEK8OEIF4ZJgTxyjAhiFeGCUG8MkwI4pVhQhCvDBOCeGWYEMQrw4QgXhkmBPHKMCGIV4YJQbwyTAjilWFCEK8ME4J4ZZgQxCvDhCBeGSbkcj+2z/k15gJXmhzLOkB8gIv98BcjSjen1xEfyzpAfICL/SgvO8blx+4QJoQRrwwTcrkfuwXb+HuFCWGvXhkmpEs/uJr0BGh1OMfVpO8UJqTVzh1Xk75TmJCWh3NcTfouYULaHs5xNel7hAlpczg3dzdcTfoOYUI4nFOGCUG8MkwI4pVhQhCvDBOCeGWYEMQrw4QgXhkmBPHKMCGIV4YJQbwyTAjilWFCEK8ME4J4ZZgQxCvDhCBeGSYE8cowIYhXhglBvDJMCOKVYUIQrwwTgnhlmBDEK8OEIF4ZJgTxyjAhiFeGCUG8MkwI4pVhQhCvDBOCeGWYEMQrw4QgXhkmBPHKMCGIV4YJQbwyTAjilWFCEK8ME4J4ZZgQxCvDhCBeGSak6MduMetcNn4QH6DsxybJf6q4U9nYQXyAWj/2r0my7Fg2ahAfoOxH8ePkgV8qblE2dhAfoNzGn15xpm3Z+EF8APbqlWFCfD822dZ9fe3e3VjWAeID+Kn+s3O+Pf1J+hZl4wfxAYp+FFcjCFxarkXZ+EF8AN+P/OJygUvLtSkbPYgPcLEf7gjPvS0Cs8FY1gHiA7QRnx/dbz9dXzYSEB+g2qs/cxlRJ3778sF15+4SJqT8AOfsZ7W7xcPvX92If+Giwr2HCfHimz6q3b8ms3TDRYXvECbE92M17142ehAfoJzqz27jQ2W4qPD44bN6ZZgQxCvDhPh+ZDtwT39+Dv2Rxm8FQtuBsawDxAcoP6ufZ4dr4c/q3TXEm8rGD+IDVIdzmfgzB3W74EyQjmcdID5AfcSv+evcwGFCDtv44N9h2pSNHsQHYK9eGSYE8cowIV0+uTsuGz+ID1Dvx3revWzMID5AvR/XnU4xnnWA+AD1foT+9Nq2bMwgPsDRNv6qM+fGsw4QH4C9emWYEMQrw4QcTfVXHtCNZR0gPoDvx3pW/nd92ehBfID6ly05nBs6TEj117mUET98mJD6X+eu/QGksawDxAdgr14ZJgTxyjAhF79sebls9CA+wOUvW14qe3jYK3118LSdEYUJafFlywtlzz28DcTfmR6/bBnt+o22YUp6/LJltOs32oYp6XGvPtr1G23DlNQ/su1W9tzD20D8nfHb+C/X/nL1oey5h7eB+DvT47dso12/0TZMCdt4ZZgQxCvDhLh+dNu1Q/yoKcUHfs2sVdnzD28D8XcmWvGRfu6P+JQRP2py8Z2+Y4v4UcNevTJMCOKVYUIQrwwTgnhlmBDEK8OEIF4ZJgTxyjAhiFeGCUG8MkwI4pVhQhCvDBOCeGWYEMQrw4QgXhkmBPHKMCGX+7F9Pve3esSPmIv9KC4tH7y4POJHzMV+lF/BvXxR4WjXb7QNU8KIV4YJudyP86dXIX7EsFevDBPSpR9nvq8e7fqNtmFKGPHKMCGIV4YJuXw41/qiwtGu32gbpuRyP1pfVDja9Rttw5S06EfbiwpHu36jbZgStvHKMCGIV4YJQbwyTAjilWFCEK8ME4J4ZZgQxCvDhCBeGSYE8cowIYhXhglBvDJMCOKVYUIQrwwTgnhlmBDEK8OEIF4ZJgTxyjAhiFeGCUG8MkwI4pVhQhCvDBOCeGWYEMQrw4QgXhkmBPHKMCGIV4YJQbwyTAjilWFCEK8ME4J4ZZgQxCvDhCBeGSYE8cowIYhXhglBvDJMCOKVYUIQrwwTgnhlmBDEK8OEIF4ZJgTxyjAhiFeGCUG8MkwI4pVhQhB/bViv9NmyK/vRX1kj4qMNG65qxEcVNlzViI8qbLiqER9V2HBVIz6qsOGqRnxUYcNVjfiowoarGvFRhQ1XNeKjCuu5anfdeHfRwdOriCM+rrCeq87EO/fp9tOlstGukmgbFrv47ctHMfLLMlxNOsawnqveLR5+/+pG/MvJXI/4qMJ6r3r/mszSzek1hREfV9hwVSM+qrDhqkZ8VGHDVY34qMKGqxrxUYUNVzXiowobrmrERxU2XNWIjypsuKoRH1XYcFUjPqqw4apGfFRhw1WN+KjChqsa8VGFDVc14qMKG65qxEcVNlzViI8qbLiqER9V2HBVIz6qsOGqRnxUYcNVjfiowoarGvFRhQ1XNeKjChuuasRHFTZc1YiPKmy4qhEfVdhwVSM+qrDhqkZ8VGHDVY34qMKGqxrxUYUNVzXiowobrmrERxU2XNWIjypsuKoRH1XYcFUjPqqw4apGfFRhw1WN+JvDdFc9QLzRMMQbDUO80TDEGw1DvNEwxBsNQ7zRMMQbDUO80TDEGw1DvNEwxBsNQ7zRMMQbDUO80TDEGw1DvNEwxBsNQ7zRMMQbDUO80bDLr94+51/h5IKD0wq7+Or96zK/3ZxeThrxIw67+OryYsItLioMWvoV3zDiYcRcfpvsFvnbKbCNhxHT61YGxgPijYJ4oyDeKIg3CuKNgnijIN4oiDcK4o2CeKP0KF78tymQie8vir/H3z0M8UbDEG80DPFGwxBvNAzxRsMQbzSMD3CMgnijIN4oiDcK4o2CeKMg3iiINwrijYJ4o/QlfrdIbj2Pep3k5+T6pOOb69j+8P5tQPe4PKyftrkfF1n21TIf1rVlPYl3Z9GvZ7dlrJa1pOOb69i4NRHM6RCXh/XTtt3nt3T7/Vs/LfNhnVvWk3j3exn50OjO/stbLen45qqg1cOvWYlgzvVxRVg/bds4F6tlPy3zYZ1b1pP47ctH/h68gfwHGJZl0vHNta3JOh3M6RLnwvpr27kmdQ3r3LKexLsfSrlRvJu3svevTzq+uTYqcxXM6RKXv4v6atv+dd5fy1xY55bFM+JzVssoR3xfbdst5mlvLcvDOrcsnm18zpkt4JUp2/628Ufibw3bPrs9sZ5aVoR1bllve/XzW/fq3fy0//ruk45vrsR1OpjTJa7cbtzeNq+qn5b5sM4ti+s4/uGthwPvOx3H3962dX6+y7KflpVhXVvGJ3dGQbxREG8UxBsF8UZBvFEQbxTEGwXxRkG8URBvFMQbBfFGQbxREG8UxBsF8UZBvFEQbxTEG2WK4vev+RcRy68bHr5o7O+5s08eO3zP+rn4euM0mKL4ND2S+q343cKdZPr00ekL9nnhKTBp8dnQfnzP/yvOKS6eLQR+/q1amO5+/Gf+HeVNee3k8oli8fbvP7mnfemXD3+G8qo4ZW2kTFr8Kj9RzZ1a4s4p/uG9eHb/WmwE3KNVfubBbvH0sXnMT0ApzkPwT/jF/twF/2b6/ObTNln6XNXBm5myeCfSnUnmt+w/vpeT+yY/CcG/IbLn3fy9//J2ON2s9sShmH/bVOcl737++NftZwuqmLL4bXFme35/5Wbx2lZ9+717Pj/J+KEw7mbu53yCL351wJ2RViw+El8scmn7L7/9PNqZftLiDyPejeBqqs9/UsCdYVqcXZgWMv1I3uSbAf+EX3wkPnuBT0vX/5gr+tYPUxZ/2Mb7c9xre/V+E1C8YreYuRsn3YsvnjgEVJmldHdeuvs3WiYtvtgp378+vq+T5C8/LWvH8dmU7p7P7mb3dp9/yef4VbVX758oFpfiq+P4Is2dparr4a1MVPx1nPyIQLufKNh+uktrhgHxaVfx64cRz/SItwrijYJ4oyDeKIg3CuKNgnijIN4oiDcK4o2CeKMg3iiINwrijYJ4oyDeKP8H1+nPACz2TlkAAAAASUVORK5CYII=" alt="plot of chunk unnamed-chunk-2"/> </p>

<pre><code class="r">mean_act1
</code></pre>

<pre><code>## [1] 9354.23
</code></pre>

<pre><code class="r">median_act1
</code></pre>

<pre><code>## [1] 10395
</code></pre>

<h2>What is the average daily activity pattern?</h2>

<pre><code class="r">act2&lt;-act %&gt;%
  group_by(interval) %&gt;%
  summarise(ave_interval_steps=mean(steps, na.rm=TRUE))

plot(act2$interval, act2$ave_interval_steps, type=&quot;l&quot;,
      main = &quot;Aveage Steps by Interval for All Days&quot;,
      xlab=&quot;Intervals&quot;,
      ylab = &quot;Average Steps&quot; )
</code></pre>

<p><img src="data:image/png;base64,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" alt="plot of chunk unnamed-chunk-3"/> </p>

<pre><code class="r">max_steps&lt;-act2[act2$ave_interval_steps==max(act2$ave_interval_steps), ]

max_steps
</code></pre>

<pre><code>## Source: local data frame [1 x 2]
## 
##   interval ave_interval_steps
## 1      835           206.1698
</code></pre>

<h2>Imputing missing values</h2>

<p>1.Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)</p>

<pre><code class="r">total_missing&lt;-length(is.na(act$steps))
total_missing
</code></pre>

<pre><code>## [1] 17568
</code></pre>

<p>2.use the mean for that 5-minute interval to fill in all of the missing values in the dataset. </p>

<pre><code class="r">library(dplyr)
act3&lt;-inner_join(act, act2)
</code></pre>

<pre><code>## Joining by: &quot;interval&quot;
</code></pre>

<pre><code class="r">act3$ave_interval_steps&lt;-round(act3$ave_interval_steps, digits=0)
act3$ave_interval_steps&lt;-as.integer(act3$ave_interval_steps)
act3$steps[is.na(act3$steps)==T] &lt;- act3$ave_interval_steps[is.na(act3$steps)==T]
</code></pre>

<p>3.Create a new dataset that is equal to the original dataset but with the missing data filled in.</p>

<pre><code class="r">act4&lt;-act3[, (1:3)]
</code></pre>

<p>4.Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?</p>

<pre><code class="r">library(dplyr)
act5&lt;-act4 %&gt;%
  group_by(date) %&gt;%
  summarise(sum_steps=sum(steps, na.rm=TRUE))
mean_act5&lt;-mean(act1$sum_steps, na.rm=TRUE)  
median_act5&lt;-median(act1$sum_steps, na.rm=TRUE)  
hist(act5$sum_steps,
                main = &quot;Histogram of Total Steps Taken by Day&quot;,
                xlab = &quot;Total Steps per Day&quot;)
</code></pre>

<p><img src="data:image/png;base64,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" alt="plot of chunk unnamed-chunk-7"/> </p>

<pre><code class="r">mean_act5
</code></pre>

<pre><code>## [1] 9354.23
</code></pre>

<pre><code class="r">median_act5
</code></pre>

<pre><code>## [1] 10395
</code></pre>

<h2>Are there differences in activity patterns between weekdays and weekends?</h2>

<p>1.Create a new factor variable in the dataset with two levels - &ldquo;weekday&rdquo; and &ldquo;weekend&rdquo; indicating whether a given date is a weekday or weekend day.</p>

<pre><code class="r">act6&lt;-act4 %&gt;%
  mutate(day=weekdays(date)) 

act6$weekdayend[act6$day==&quot;Saturday&quot;|act6$day==&quot;Sunday&quot;]&lt;-&quot;Weekend&quot; 
act6$weekdayend[is.na(act6$weekdayend)==T]&lt;-&quot;Weekday&quot; 
act6$weekdayend&lt;-factor(act6$weekdayend)
</code></pre>

<p>2.Make a panel plot containing a time series plot (i.e. type = &ldquo;l&rdquo;) of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). See the README file in the GitHub repository to see an example of what this plot should look like using simulated data.</p>

<pre><code class="r">require(ggplot2)
</code></pre>

<pre><code>## Loading required package: ggplot2
</code></pre>

<pre><code class="r">ggplot(act6, aes(interval, steps))+
  geom_line()+
  facet_wrap(~weekdayend, nrow=2)+
  facet_wrap(~weekdayend, ncol=1)+
  xlab(&quot;Interval&quot;)+
  ylab(&quot;Number of steps&quot;)
</code></pre>

<p><img src="data:image/png;base64,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" alt="plot of chunk unnamed-chunk-9"/> </p>

</body>

</html>

