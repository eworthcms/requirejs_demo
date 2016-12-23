## requirejsѧϰ�ʼ�

author: lzj

�½Ӵ�requirejs, ���ż�ѡ��, ���˽ⶫ����¼����, �Ա��������

��ͳ��js���ط�ʽ��ʹ�ö��`script`��ǩ, ��js�ļ�������˳�����μ���, �����ļ��ط�ʽ����������������Դ�ļ���, ���һ�Ӱ�����������Ⱦ.

requirejsͨ��������ͬjs�ļ�֮���**������ϵ**,  ������**�첽����**��**�ص�ִ��**�ķ�ʽִ��js����, ��Ч�Ľ������������.
����requirejs��һ��ģ�黯��js���, ���������ģ�黯, ����ʹ�ýű�ʱ��moduleId�����URL��ַ. һ���ļ�ֻ����һ��ģ��.

### API
requirejs���õ���������������������
��������:
- define: define��һ��**ȫ�ֺ���**, ���ڴ���һ���µ�ģ��. 
�˷����ɽ���3������, define(name, deps, callback):
1. name: ��ѡ����, ģ������
2. deps: ��ѡ����, ����ģ������
3. call: ��ѡ, �ص�����, ������������ģ��, ��������ģ����Բ���(���ǳ���Ϊ**ģ�����**)����ʽ����˻ص�����, ���Ҳ�����˳����ģ�������˳��һ��.
- require: requireҲ��һ��**ȫ�ֺ���**, ���ڼ�������.
�˷����ɽ�����������, require(deps, callback):
1. ����, ��ʾ��������ģ��
2. �ص�����, ָ����ģ����غ�, �����ô˺���; ���ص�ģ����Բ�������ʽ����˻ص�����, ���Ҳ�����˳����ģ�������˳��һ��.
- config: ��������requirejs

����������:
- basrUrl: ����ģ��ĸ�·��
- paths: ӳ�䲻�ڸ�·���µ�ģ���·��
- shim: ���ڲ�����AMD�淶��jsģ��, ʹ�ô����ÿ�ʵ��requirejs����

### ���ڿ�ʼ��ʾ��

#### Ŀ¼�ṹ����Ҫ����

![Alt text](./1482149192649.png)

- appĿ¼, ��Ÿ�ҳ�湦�ܴ���
- moduleĿ¼, ����Զ���ģ�����
- libĿ¼, ��ſ��ļ�
- main.js, ������ڵ�, ��Ҫ����������, һ����������ģ�弰ģ����������ϵ, ���Ǽ��س�����ģ��.

index.html
```xml
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title></title>
		<script data-main="js/main.js" src="js/lib/require/require.js"></script>
	</head>
	<body>
		<div>Hello World</div>
	</body>
</html>
```
main.js
```javascript
require.config({
	baseUrl: "js/",
	paths: {
		"jquery": ["lib/jquery/jQuery.v1.11.1.min"]
	}
});

require(["jquery"], function(jq){
	alert(jq().jquery);
});
```
���������index.html
alert��ʾjQuery�汾��1.11.1, ҳ����ʾHello World, 
����js��ִ�в�û��Ӱ��ҳ�����Ⱦ.

> ʾ��������, ӳ���ϵ��keyֵ**jquery**���ܸı�, ������Ϊ�ڵ���`define`��������jqueryģ��ʱ, ʹ���˵�һ������, ����ģ������Ϊjquery, ��ô���ģ���ֻ����jquery, ֻ����jqueryȥ������, ���Ե�ʹ����������ȥ����ʱ, ����ʾ`undefined`.
> 
> ��, ������ģ��ʱû��ʹ�õ�һ������Ϊ������, ��ô��������ʱ�Ϳ���ʹ�����������, ʹ������������.

#### �������
index.html��, ͨ��`script`��ǩ������*requirejs.js*���ļ�
requirejsͨ��`data-main`����ȥ����һ���ű��ļ�(��ʾ���о���*main.js*), �˽ű��ļ�����ҪΪ���нű��ļ�����һ����·��, requirejsͨ�������·��ȥ������ص�ģ��.

main.js��, 
��������������ģ��ĸ�·��baseUrl, 
Ȼ��������paths����, ʾ����ֻӳ����jquery�Ŀ��ļ�

��Ҫע�����:
1. ���ļ�����Ҫ�ټ�`.js`��׺
2. ���baseUrl�����õĻ�, Ĭ��Ϊ**main.js**����·��, ������ģ����ļ�Ĭ����main.js��ͬһ��Ŀ¼(������Ŀ¼)

require����������jqueryģ��, ������ģ�������Ϊ�������뵽�ص�������, 
���մ�ӡ��jquery�İ汾��Ϣ.


#### ����ʹ��define��������һ��������������ģ��, �������书��

��moduleĿ¼���½��ļ�`person.js`, ��������:
```javascript
define(function(){
	return function(){
		var persons = [{
			id: 1,
			name: '����',
			age: 23, 
			sex: '��'
		}, {
			id: 2,
			name: '����',
			age: 21, 
			sex: 'Ů'
		}, {
			id: 3,
			name: '����',
			age: 19, 
			sex: '��'
		}, {
			id: 4,
			name: '��һ',
			age: 23, 
			sex: '��'
		}];
		
		var list = function() {
			// ͨ���ӷ������˻�ȡ, ʾ�����þ�̬����
			return persons;
		};
		
		return {
			list: list
		};
		
	}();
});
```
�ļ��ж�����һ��ģ��, ��ģ�鲻�����κ�����ģ��, ������һ������, �����а���һ��list����.

`main.js`�ļ��޸�����:
```javascript
require.config({
	baseUrl: "js/",
	paths: {
		"jquery": ["lib/jquery/jQuery.v1.11.1.min"],
		"person": ["module/person"]
	}
});

require(["jquery", "person"], function($, person){
	var persons = person.list();
	for(var i=0; i<persons.length; i++) {
		$('body').append("<div>"+ persons[i].id + ".&nbsp;&nbsp;&nbsp;" + persons[i].name + "</div>");
	}
});
```
1. �����personģ���ӳ��
2. ������personģ��, ����������`list`����, ��ȡ��persons����, ������������չʾ��ҳ����.
����, �ص���������������**($��person)**�ֱ�Ϊ`jquery`��`person`����ģ���ģ�����.

��������Ч������:
![Alt text](./1482199391474.png)


#### ͨ���Զ������Խ�һ���ع�����

�����ʾ����, ��ģ��main.jsֱ�Ӽ�����`person`ģ��, �����䷵�����ݽ����˴���, ������ҳ���ʱ, ��������ģ�黯������, ����Ҳ��Խ��Խ������. ��ͨ���Զ������Խ�һ���ع�����.

�½�person.htmlҳ��, ��������:
```xml
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<script data-main="js/main.js" src="js/lib/require/require.js"></script>
	</head>
	<body my-js="js/app/showperson.js">
		<div>Hello Person</div>
	</body>
</html>
```
����, bodyԪ��������Զ�������my-js, ��ֵΪ��ҳ��Ĺ���js�ļ�·��.

��app·�����½��ļ�showperson.js, ��������:
```javascript
require(["jquery", "person"], function($, person){
	var persons = person.list();
	for(var i=0; i<persons.length; i++) {
		$('body').append("<div>"+ persons[i].id + ".&nbsp;&nbsp;&nbsp;<span>" 
		+ persons[i].name + "</span></div>");
	}
});
```
����ԭ��д��main.js�е�չʾ�����ƶ������ļ���.

�޸�main.js�ļ�,
```javascript
require.config({
	baseUrl: "js/",
	paths: {
		"jquery": ["lib/jquery/jQuery.v1.11.1.min"],
		"person": ["module/person"]
	}
});

require(["jquery"], function($){
	var jsurl=$('body').attr('my-js');
    require([jsurl], function () {
		
	});
});
```
��require�����Ļص�������, ������bodyԪ�ص�my-js���Ե�ֵ, ���ظ�ֵָ���ģ��, ��showperson.js, ģ�������ɺ������ִ�����еĴ���.

�����Ϳ��Ը���main.js, ����ͬģ��Ĺ��ܴ���ģ���з����ȥ, ����������չ.
��������Ч������:
![Alt text](./1482201540660.png)


#### ʹ��define��������һ����������ģ���ģ��

�����ʾ����, ʹ��define����������һ����������ģ��, �ֶ���һ����ģ��ʹ���������涨���ģ��.

��moduleĿ¼���½��ļ�account.js, ��������:
```javascript
define(["person"], function(person){
	var persons = person.list();
	
	var accounts = [];
	// ���Ǹ���persons����, ����һ��accounts����
	for(var i=0; i<persons.length; i++) {
		accounts.push({
			personId: persons[i].id,
			psersonName: persons[i].name,
			accountNo: (Math.random() * 1000000).toFixed()
		});
	}
	
	var list = function() {
		return accounts;
	}
	
	return  {
		list: list
	}
});
```
�¶����ģ��������`person`ģ��, ��ͨ���ص�����������personģ���еķ���.

appĿ¼���½��ļ�showaccount.js, ��������:
```javascript
require(["jquery", "account"], function($, account){
	var accounts = account.list();
	for(var i=0; i<accounts.length; i++) {
		$('body').append("<div>"+ accounts[i].personId + ".&nbsp;&nbsp;&nbsp;" 
		+ accounts[i].psersonName + "&nbsp;&nbsp;&nbsp;" + accounts[i].accountNo +"</div>");
	}
});
```

�½�account.html,
```xml
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<script data-main="js/main.js" src="js/lib/require/require.js"></script>
	</head>
	<body my-js="js/app/showaccount.js">
		<div>Hello Account</div>
	</body>
</html>
```

����Ч������ͼ:
![Alt text](./1482214650461.png)



#### �����AMD�淶��ģ��

moduleĿ¼���½��ļ�noamd.js
һ���, ���Ǳ�дjs�������js��������¼�����ʽ:
```javascript
// ��һ��:
var noamd = (function(){
	
	var hi = function(name) {
		var str = '��Һ�, ����' + name;
		alert(str);
	}
	var say = function() {
		alert('Hello');
	}
	
	return {
		hi: hi,
		say: say
	}
	
})();
// �ڶ���:
var noamd = {};
noamd.hi= function(name) {
	var str = '��Һ�, ����' + name;
	alert(str);
}
noamd.say = function() {
	alert('Hello');
}
// ������:
(function(){
	
	var hi= function(name) {
		var str = '��Һ�, ����' + name;
		alert(str);
	}
	var say = function() {
		alert('Hello');
	}
	
	window.noamd = {
		hi: hi,
		say: say
	}
	
})(window);
```

main.js��, config�����ĵ����޸�Ϊ:
```javascript
require.config({
	baseUrl: "js/",
	paths: {
		"jquery": ["lib/jquery/jQuery.v1.11.1.min"],
		"person": ["module/person"],
		"account": ["module/account"],
		"mynoamd": ["module/noamd"]
	},
	shim: {
		"mynoamd": {
			deps: [],
			exports: "noamd"
		}
	}
});
```
1. paths�������noamdģ���ӳ��
2. ����`shim`����,  
- **mynoamd**Ϊpathsӳ���key
- deps, ����, ��ʾ��ģ��Ҫ����������ģ��
- exports��ֵ, ��**noamd**, ������<span style="color: red">module/noamd.js�ļ��б�¶��ȥ��ȫ�ֱ�������һ��</span> 

�޸���showperson.js�ļ�
```javascript
require(["jquery", "person", "mynoamd"], function($, person, _){
	var persons = person.list();
	for(var i=0; i<persons.length; i++) {
		$('body').append("<div>"+ persons[i].id 
		+ ".&nbsp;&nbsp;&nbsp;<span>" + persons[i].name + "</span></div>");
	}
	
	$('span').click(function(){
		_.hi($(this).text());
	})
});
```
�ļ��������¶���ķ�AMDģ��`mynoamd`, ����`_`��Ϊ��ģ�������ص�������.
�ص�������, Ϊÿ��spanע����`click`�¼�, ������`_`�����`hi`����.
��������Ч������, �������ʱalert��ʾ: ��Һ�, ����xxx


#### ��¶���ȫ�ֱ����ķ�AMDģ��

���һ���ļ�ģ�鱩¶�˶��ȫ�ֱ���, ��ô�Ͳ���ʹ��shim��, ��ʹ��`init`����, �����������ļ�(multi.js):
```javascript
function xixi() {
	alert("xixi...");
}

function haha() {
	alert("haha...");
}
```
������ȫ�ֱ���, ���Ҷ���Ҫ, ��ômain.jsд������:
```javascript
require.config({
	baseUrl: "js/",
	paths: {
		"jquery": ["lib/jquery/jQuery.v1.11.1.min"],
		"person": ["module/person"],
		"account": ["module/account"],
		"mynoamd": ["module/noamd"],
		"mymulti": ["module/multi"]
	},
	shim: {
		"mynoamd": {
			deps: [],
			exports: "noamd"
		},
		"mymulti": {
			deps: [],
			init: function() {
				return {
					myxixi: xixi,
					myhaha: haha
				}
			}
		}
	}
});
```
��AMDģ��`mymulti`ͨ��`init`����, ���Ⱪ¶һ���ӿڶ���, ����ԭ��������ȫ�ֺ���ӳ��Ϊ�ӿڶ���������ֲ�����, �����Ϳ��������AMD�淶��ģ��һ��ʹ����.
��exports��initͬʱ���ڵ�ʱ, exports��������.

