Void
============================================================

## Info
I made a simple webpage that checks whether the flag is correct... Wait, where are the flag-checking functions?    
* Chilly level: 1
* Price: 100
* Category: Reverse

## Connection
`https://c09-void.hkcert24.pwnable.hk/`

## Solution
The original source code:  
```
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Codeless</title>
  <link rel="stylesheet" href="style.css">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@300..700&family=Playfair+Display:ital,wght@0,400..900;1,400..900&display=swap" rel="stylesheet">
</head>

<body>
    <div class="container">
        <input type="text" id="flag" placeholder="What is the flag?" onkeydown="handleKeyPress(event)">
    </div>
</body>
<scipt>

with (ㅤ`` ) {
ㅤㅤㅤㅤㅤㅤㅤ
//This is the hiiden part

}
// https://x.com/aemkei/status/1843756978147078286
function \u3164(){return f="",p=[]  
,new Proxy({},{has:(t,n)=>(p.push(
n.length-1),2==p.length&&(p[0]||p[
1]||eval(f),f+=String.fromCharCode
(p[0]<<4|p[1]),p=[]),!0)})}//aem1k

</scipt>
</html>

```
In this case, we can see that the hidden part cannot be discover by normal technique  
[Explanation of technique that use to hide code](https://x.com/aemkei/status/1843756978147078286)  
Now we will modified the script, add `console.log` to log everything and find the flag  
```
function \u3164() {
  return f = "", p = [], 
  new Proxy({}, {
    has: (t, n) => (
      p.push(n.length - 1), 
      console.log("Current p array:", p),
      2 == p.length && (p[0] || p[1] || eval(f), 
      f += String.fromCharCode(p[0] << 4 | p[1]), 
      console.log("Current f:", f), 
      // Check for flag format
      f.startsWith("hkcert24{") && console.log("Flag found:", f),
      p = []), 
      !0)
  });
}

```
--> Run the source again and check the result in Development Tools on browser  

```
function check() {
    if (flag.value === 'hkcert24{j4v4scr1p7_1s_n0w_alm0s7_y3t_4n0th3r_wh173sp4c3_pr09r4mm1n9_l4ngu4g3}') {
        flag.disabled = true;
        flag.classList.add('correct');
    } else {
        flag.classList.add('wrong');
        setTimeout(() => flag.classList.remove('wrong'), 500);
    }
}
Flag.html:1 
```

**Flag: `hkcert24{j4v4scr1p7_1s_n0w_alm0s7_y3t_4n0th3r_wh173sp4c3_pr09r4mm1n9_l4ngu4g3}`**