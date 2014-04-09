验证汇总
=============

> 常用验证汇总表

## 贡献规则：

+ 保证添加内容可以，复制后直接运行
+ 尽量详细的添加一些实现原理说明

## 字符验证集合

### 检查是否checkbox|radio

```
var checkable = function(element) {
	return /radio|checkbox/i.test(element.type);
};
```


### 为空验证

```
function required(elem, value){
	if (elem.nodeName.toLowerCase() === 'select') {
	    var v = elem.value;
	    return v && v != 0 && v != '';
	}
	if (checkable(elem)) {
	    return getLength(value, elem) > 0;
	}
	return value.length > 0;
}
```

### 国内邮政编码

```
/^[1-9][0-9]{5}$/.test(value)
```

### 手机号验证

TODO: 手机号如果增加新的号段，需要手动更新

```
/^(13|15|18|14)\d{9}$/.test(value)
```

### 邮箱验证

```
/^((([a-z]|\d|[!#\$%&'\*\+\-\/=\?\^_`{\|}~]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])+(\.([a-z]|\d|[!#\$%&'\*\+\-\/=\?\^_`{\|}~]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])+)*)|((\x22)((((\x20|\x09)*(\x0d\x0a))?(\x20|\x09)+)?(([\x01-\x08\x0b\x0c\x0e-\x1f\x7f]|\x21|[\x23-\x5b]|[\x5d-\x7e]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(\\([\x01-\x09\x0b\x0c\x0d-\x7f]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF]))))*(((\x20|\x09)*(\x0d\x0a))?(\x20|\x09)+)?(\x22)))@((([a-z]|\d|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(([a-z]|\d|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])*([a-z]|\d|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])))\.)+(([a-z]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(([a-z]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])*([a-z]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])))$/i.test(value)
```

### url

```
/^(https?|s?ftp):\/\/(((([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(%[\da-f]{2})|[!\$&'\(\)\*\+,;=]|:)*@)?(((\d|[1-9]\d|1\d\d|2[0-4]\d|25[0-5])\.(\d|[1-9]\d|1\d\d|2[0-4]\d|25[0-5])\.(\d|[1-9]\d|1\d\d|2[0-4]\d|25[0-5])\.(\d|[1-9]\d|1\d\d|2[0-4]\d|25[0-5]))|((([a-z]|\d|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(([a-z]|\d|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])*([a-z]|\d|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])))\.)+(([a-z]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(([a-z]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])*([a-z]|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])))\.?)(:\d*)?)(\/((([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(%[\da-f]{2})|[!\$&'\(\)\*\+,;=]|:|@)+(\/(([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(%[\da-f]{2})|[!\$&'\(\)\*\+,;=]|:|@)*)*)?)?(\?((([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(%[\da-f]{2})|[!\$&'\(\)\*\+,;=]|:|@)|[\uE000-\uF8FF]|\/|\?)*)?(#((([a-z]|\d|-|\.|_|~|[\u00A0-\uD7FF\uF900-\uFDCF\uFDF0-\uFFEF])|(%[\da-f]{2})|[!\$&'\(\)\*\+,;=]|:|@)|\/|\?)*)?$/i.test(value)
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
/**
 * 获取年龄
 * @param id
 * @returns {number}  返回当前周岁(已过生日默认+1岁)
 */
function getAge(id){
	id = idCard15To18(id);
	var day = new Date();
		nowYear = day.getFullYear(),
		nowMonth = day.getMonth() + 1,
		nowDay = day.getDay(),
		idDay = id.substring(6, 14),
		idcardYear = idDay.substring(0, 4),
		idcardMonth = idDay.substring(4, 6),
		idcardDay = idDay.substring(6)

	var age = nowYear - idcardYear,
		M = nowMonth - parseInt(idcardMonth),
		D = nowDay - parseInt(idcardDay);

	return (M>0 || (M == 0 && D >= 0)) ? age+1 : age;
}
```

### 信用卡

```
function isCreditCard(number){
	function reverseString(source){
		var s=source;
		var ss="";
		for(var i=s.length-1;i>=0;i--){
			ss=ss+s.charAt(i);
		}
		return ss;
	}
	try{
		if(number.length==0 || number.length<12 || number.length>19){
			return false;
		}
	
		var exp = /[34569]/,
			objExp = new RegExp(exp);
	
		if(objExp.test(number.charAt(0)==false)) return false;
	
		var n = reverseString(number),
			s = 0,
			d = 0;
	
		for(var i=0;i<n.length;i++){
			//说明是基数，因为从0位开始
			if (i%2==0){
				s = s + n.charAt(i) * 1
			} else {
				var t = n.charAt(i) * 2;
				if(t > 9){
					d = d + (t/10|0) + t % 10;
				}else{
					d = d + t;
				}
			}
		}
	
		var sum = s + d;
	
		if(sum%10 == 0){
			return true;
		} else {
			return false
		}
	
	}catch (e){
		return false;
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
!isNaN(value)
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

```
/^((-?\d)\.\d+)?$/.test(value)
```


## 时间验证集合

### date

```
!/Invalid|NaN/.test(new Date(value).toString())
````


PS： 可以到[这里](https://github.com/Johnqing/QHPAY/blob/master/js/lib/base.js)查看一些实用的基础方法


