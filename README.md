验证汇总
=============

> 常用验证汇总表

## 贡献规则：

+ 保证添加内容可以，复制后直接运行
+ 尽量详细的添加一些实现原理说明

## 字符验证集合

### 邮箱验证

```
/^((([a-z]|\d|[!#\$%&'\*\+\-\/=\?\^_`{\|}~]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])+(\.([a-z]|\d|[!#\$%&'\*\+\-\/=\?\^_`{\|}~]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])+)*)|((\x22)((((\x20|\x09)*(\x0d\x0a))?(\x20|\x09)+)?(([\x01-\x08\x0b\x0c\x0e-\x1f\x7f]|\x21|[\x23-\x5b]|[\x5d-\x7e]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(\\([\x01-\x09\x0b\x0c\x0d-\x7f]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF]))))*(((\x20|\x09)*(\x0d\x0a))?(\x20|\x09)+)?(\x22)))@((([a-z]|\d|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(([a-z]|\d|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])*([a-z]|\d|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])))\.)+(([a-z]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(([a-z]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])*([a-z]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])))$/i.test(value)
```

### url

```
/^(https?|s?ftp):\/\/(((([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(%[\da-f]{2})|[!\$&'\(\)\*\+,;=]|:)*@)?(((\d|[1-9]\d|1\d\d|2[0-4]\d|25[0-5])\.(\d|[1-9]\d|1\d\d|2[0-4]\d|25[0-5])\.(\d|[1-9]\d|1\d\d|2[0-4]\d|25[0-5])\.(\d|[1-9]\d|1\d\d|2[0-4]\d|25[0-5]))|((([a-z]|\d|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(([a-z]|\d|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])*([a-z]|\d|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])))\.)+(([a-z]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(([a-z]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])*([a-z]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])))\.?)(:\d*)?)(\/((([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(%[\da-f]{2})|[!\$&'\(\)\*\+,;=]|:|@)+(\/(([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(%[\da-f]{2})|[!\$&'\(\)\*\+,;=]|:|@)*)*)?)?(\?((([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(%[\da-f]{2})|[!\$&'\(\)\*\+,;=]|:|@)|[\uE000-\uF8FF]|\/|\?)*)?(#((([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(%[\da-f]{2})|[!\$&'\(\)\*\+,;=]|:|@)|\/|\?)*)?$/i.test(value)
```

### 信用卡

使用Luhn算法，总共有四步：

1. 从卡号的最后一个数字开市,并逆向将奇数位置的数字相加.

2. 将奇数位置的数字先*2,如果是两位数,就将这两位数相加,然后将结果放到总和中.

3. 将两个总和相加将结果与10取膜 ,如果整除,则为正确的MasterCard.

```
if ( /[^0-9 \-]+/.test(value) ) {
	return false;
}
var nCheck = 0,
	nDigit = 0,
	bEven = false;

value = value.replace(/\D/g, "");

for (var n = value.length - 1; n >= 0; n--) {
	var cDigit = value.charAt(n);
	nDigit = parseInt(cDigit, 10);
	if ( bEven ) {
		if ( (nDigit *= 2) > 9 ) {
			nDigit -= 9;
		}
	}
	nCheck += nDigit;
	bEven = !bEven;
}

return (nCheck % 10) === 0;
```

### HTML标签

```
/<(.*)>.*<\/>|<(.*) \/>/.test(value)
```

### 身份证

身份证15位编码规则：dddddd yymmdd xx p    
dddddd：地区码    
yymmdd: 出生年月日    
xx: 顺序类编码，无法确定    
p: 性别，奇数为男，偶数为女   
身份证18位编码规则：dddddd yyyymmdd xxx y    
dddddd：地区码    
yyyymmdd: 出生年月日    
xxx:顺序类编码，无法确定，奇数为男，偶数为女    
y: 校验码，该位数值可通过前17位计算获得   

11:"北京"
12:"天津"
13:"河北"
14:"山西"
15:"内蒙古"
21:"辽宁"
22:"吉林"
23:"黑龙江 "
31:"上海"
32:"江苏"
33:"浙江"
34:"安徽"
35:"福建"
36:"江西"
37:"山东"
41:"河南"
42:"湖北 "
43:"湖南"
44:"广东"
45:"广西"
46:"海南"
50:"重庆"
51:"四川"
52:"贵州"
53:"云南"
54:"西藏 "
61:"陕西"
62:"甘肃"
63:"青海"
64:"宁夏"
65:"新疆"
71:"台湾"
81:"香港"
82:"澳门"
91:"国外 "

```
function isIdCard(arrIdCard){  
	arrIdCard = arrIdCard.length == 15 ? idCard15To18(arrIdCard) : arrIdCard;
	var tag = false;      
	var sigma = 0;    
	var a = [7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2];    
	var w = ["1", "0", "X", "9", "8", "7", "6", "5", "4", "3", "2"];         
	for (var i = 0; i < 17; i++) {    
		var ai = parseInt(arrIdCard.substring(i, i + 1));    
		var wi = a[i];    
		sigma += ai * wi;             
	}     
	var number = sigma % 11;              
	var check_number = w[number];     
	if (arrIdCard.substring(17) != check_number) {    
		tag =  false;    
	} else {    
		tag = true;    
	}     
	return tag;  
}
function idCard15To18(id){  
	var W = [7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2, 1];  
	var A = ["1", "0", "X", "9", "8", "7", "6", "5", "4", "3", "2"];  
	var i, j, s = 0;  
	var newid;  
	newid = id;  
	newid = newid.substring(0, 6) + "19" + newid.substring(6, id.length);  
	for(i = 0; i < newid.length; i++ ){  
		j = parseInt(newid.substring(i,i+1))*W[i];  
		s = s + j;  
	}  
	s = s % 11;  
	newid = newid + A[s];   
	return newid;  
} 
//通过身份证号判断是男性还是女性
//男性返回M，女性返回F
function isFOrM(idCard){
	idCard = idCard.length == 15 ? idCard15To18(idCard) : idCard;
	if(idCard.substring(14,17)%2 == 0){
		return 'F';
	}else{
		return 'M';
	}
}
```

### 字节数验证

```
function byteRangeLength(value){
	var length = value.length;   
	for(var i = 0; i < value.length; i++){   
		if(value.charCodeAt(i) > 127){   
			length++;   
		}   
	}   
	if(param.length === 1) {param[1] = param[0]};
	return length >= param[0] && length <= param[1];  
}
```

### 汉字

```
/^[\u4e00-\u9fa5],{0,}$/.test(value)
```

### 固话

```
/^(\d{3,4}-)?\d{7,8}$/.test(value)
```

### 图片格式

```
/\.(jpe?g|gif|bmp|png)/i.test(value)
```

### qq号

```
/^\d{5,10}$/.test(value)
```

## 数字验证集合

### 数字

```
/^[0-9]*$/.test(value)
```

### 整数

```
/^\d+$/.test(value)
```

### 浮点数

```
/^(-?\d+)(\.\d+)?$/.test(value)
```

### 小数点

/^((-?\d)\.\d+)?$/.test(value)



## 时间验证集合

### date

```
!/Invalid|NaN/.test(new Date(value).toString())
````

