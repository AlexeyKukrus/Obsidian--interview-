```JS
//1. Что будет в консоли?
	ОТВЕТ: 0,1,2,3
for (var i = 0; i < 3; i++) { 
	console.log(i) 
} 
console.log(i)

//2. Что будет в консоли?
	ОТВЕТ: [0. 0]
var i = 10 
var arr = [] 
while(--i) { 
	arr.push(function () { 
		return i+i 
	})
} 
console.log([ 
	arr[0](), 
	arr[1](), 
])
```
