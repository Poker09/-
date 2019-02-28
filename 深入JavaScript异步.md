@(JavaScript)
# JavaScript�첽
## ʲô���첽��
�첽�򵥵�������һ�δ����߼���ִ��ʱ���Ǽ�ϵģ������������ġ�ͨ������ִ��һ����Ȼ���һ��ʱ����ִ��һ���֡�
## Ϊʲô��Ҫ�첽��
��ΪJavaScript�ǵ��̵߳ģ�����Ҫ�첽���ֻ����ô������Ч��ִ�С�����http�����ļ��������ֺ�ʱ�Ĳ���������첽ִ����ô��ʮ�ֵĿ��١�
## ���ʵ�֣�
ʵ�ֵķ�ʽĿǰ��Ҫ�����ֻص�������Promise��Generator �����лص������������ʵ�ַ�ʽ����ES6�м�����Promise��Generator��ʹ����һ�ָ�����Ϊ��ȡ�����첽�����ĸ��ӳ̶ȣ�������ƶ�Ƕ�׵�ʹ�ú����߾ͱȽϺã����ֻ��һ��ص��������ӵļ�����ˡ�
### �ص�����
�ص�������ʮ�ּ򵥷����һ���첽ִ�з�ʽ�����ǰѽ���Ҫִ�еĺ��������첽���ʱ�ܷ��ʵ����������в����á�
```javascript
function callback(){
	console.log()
}
post('interface/a',callback)
```
����callback���ǻص����������Լ������������룬���첽ִ�����֮����Է��ʵ���ִ�С�
���ǿ��Կ�����ֻ��һ��ص���ʱ�򣬻ص�������ʵ�ǳ������ֻ����JavaScript��򵥵�ԭ��û�н�������API�����ǵ�Ƕ��ʮ�ָ��ӵ�ʱ��ͻ���ֺܶ����⡣�磺
``` javascript
post('interface/a',function(){
	post('interface/b',function(){
		post('interface/c',function(){
			....
		})
	})
})
```
����Ƕ��ʮ�ָ��ӵĻص������ǳ�����ά��������������ֻ��д�˵�������ټ������е��߼�������δ���ͻ���ʮ�֡��Ӵ󡯣���������һ��һ���Ƕ�����������Ļ������ཻ�ڣ������ʮ��ǿ��������Ҫ�����е�ĳһ��ʱ��Ҫ�����ϼ�����¼����ⲻ��������Ҫ�ġ����Իص�������ֻ��һ���ʱ��ʹ����ѣ���������²��Ƽ�ʹ�á������Ŀ����ʹ��Promise�����ͳһһ�ַ�ʽ����Ϊ������ʽ��һ�����Ҳ�ܼ򵥣�������http�������ͳһ��ڣ�ȫ�ֶ��干�÷����������ڴ����쳣���ʱ���Ӱ�ȫ�ͷ��㡣
### Promise
Promise�Ƕ��첽ִ�е�һ�ֽⷽ����������Promise����
####ʹ��
Promise��ԭ��ʮ�ּ򵥣�����״̬�ĸı䣬���ڱ�ɲ�ͬ״̬��ʱ��ִ�в�ͬ�ĺ�����������״̬�ı�·��pending->fulfilled
��pending->rejected��һ��Promise����ֻ�ܸı�һ��״̬���ı�״̬�ķ�ʽҲ�ܼ򵥾���ִ��resolve��reject������
``` javascript
let promise = new Promise((resolve,reject) => {
	http.post('interface/a',function(){
		resolve('success') // pending->fulfilled
	},function(){
		reject('fail') // pending->rejected��
	})
})
```
�����е�resolve��reject �����õĲ�����
��״̬�ı�֮���ͨ��Promise.protoype.then��Promise.protoype.catch������ִ�ж�Ӧ״̬�ĺ�����
``` javascript
promise.then((data)=>{
	// pending->fulfilledִ��
}).catch(error =>{
	// pending->rejectedִ��
})
```
Promise�Ļ���ʹ��ʮ�ּ򵥣�������ʽ����ģʽҲʮ�ַ������Ǵ��������߼�˼·��������ͬʱ��Ҫ����첽����ʱ�������ֳ���������֮����
##### ��ʽʹ��
���Ǿ��������������첽����������������������ʹ�ûص������ͻ���ֻص����������⣬��Promise��ʮ��������ס�
``` javascript
// �ص�����
post('interface/a',function(){
	post('interface/b',function(){
		post('interface/c',function(){
			....
		})
	})
})
	// Promise
post('interface/a').then(data =>{
	return post('interface/b')
}).then(data => {
	return Post('interface/c'
}).then(data => {
	....
})
```
�Ա�֮�����ǿ������Եĸо���Promise���ӵļ�����ˣ���Ȼص�������Ƕ������Ҫ����������������⣺
1. �����Ļ��������ͨ����������������ϡ�
2. ��д������ף���ʽ�ṹ��
##### Promise.all
�ڴ���ĳ��������Ҫ����첽����ȫ�����ʱ��ִ�У�PromiseҲ�о��ѵĽ����ʽ��
``` javascript
 Promise.all([promise1,promise2,promise3]).then(data => {}).catch(e => {})
```
ֻ�е����е�Promiseȫ����Ϊfulfilled״̬ʱ�ͻ�ִ��then�еĺ�����������һ����Ϊrejected״̬�ͻ�ִ��catch�������ܺõĽ���������������

��ʹ��Promise.allʱ�����漸��ע���
1. Promise.all�е�ʵ������Լ�������then�ⲿ����ȡthen�ķ���ֵ�����û�з���ֵ����undefined��
2. Promise.all�е�ʵ������Լ�������catch �ⲿ�����Ჶ�����Ĵ��󣬳��ִ���ʱPromise.all��״̬Ҳ�����Ϊrejected��Promise.all��then�ж�Ӧ��ֵ��catch�ķ���ֵ��
3. Promise.all��ʵ���Լ������then��catch������ִ������ⲿ����������
``` javascript
let Pro1 = new Promise((resolve) => {
    setTimeout(() => {
        resolve('Pro1')
    }, 1000);
}).then(data => {
    console.log(data) // 'Pro1'
});
let Pro2 = new Promise((resolve) => {
    setTimeout(() => {
        resolve('Pro2')
    }, 2000);
});
let Pro3 = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject('Pro3 Error')
    }, 3000);
}).catch(e => {
    console.log(e); // Pro3 Error
    return `${e} catch`
});

Promise.all([Pro1, Pro2, Pro3]).then(data => {
    console.log(data) // [ undefined, 'Pro2', 'Pro3 Error catch' ]
});
```
#### �쳣����
Promise�ĵ��쳣����Ҳ��Щ������Promise����������˴���js��������ִֹ�С�
```  javascript
new Promise(() =>{
    console.log(x) // UnhandledPromiseRejectionWarning: ReferenceError: x is not defined
});
setTimeout(()=>{
    console.log(3) // 3
},3000);
```
����������Promise�����һ��������ֵxӦ��ͨ���ᱨ����ֹjs��ִ�е���Promise�л��ӡ�������Ǵ�������ִ�С����������дcatch,����ᱻcatch������
``` javascript
new Promise(() =>{
    throw 'err'
}).catch(e => {
	console.log(e) // 'err'
});
```
����catch�ز��񵽴�����������ƽʱ��ʹ��Promiseʱ���Ҫд��catch������
#### �ܽ�
Promise���ľ���״̬�ĸı䣬��ִ�в�ͬ�Ļص���������ص����������������һ��ȫ�µ�API���ڴ�����첽�����ʱ��ʮ�����ã��ڴ������д�ϣ���ʽ��Ҳ�Ȼص���������Ծʽ��������ף����Ƕ��صĴ�����ʽ��һЩAPI��Ҫ���������ʹ�úá�
### Generator�첽
#### Generator����
generator��ES6���¼����һ�����⺯������һ�㺯����ȫ��ͬ���ṩ��һ���µ��첽�������������˵��generator����ִ��֮�󷵻ص���һ��״̬����ͨ��yield����״̬��ͨ��next�������α���״̬������ִ��һ��next֮�����������ִ�п������Ϊ���������ͣ������������Ļ������ƽ��˿���Ȩ�����´�ִ��ʱ�ڽ�������Ļ�ÿ���Ȩ���ǲ��Ǹо����첽���񣬷���һ������ȴ�����һ��ʱ����ִ�лص���
``` javascript
function* generator() {
  yield 'ijijin';
  yield 'hello';
}
let a = generator() // ִ�з�����һ��״̬��
a.next() // { value: 'ijijin', done: false } 
a.next() // { value: 'hello', done: false }
a.next() // { value: 'undefined', done: true }
```
�����generator�﷨����ȥECMAScript 6 ������ѧϰ,����ֻ̽�������첽���֣�https://es6.ruanyifeng.com/#docs/generator
#### �첽ʹ��
generator����������ִͣ�в��Ҳ������������첽����Ҫ��
``` javascript
function* generator() {
  yield post('....');
  yield post('....');
}
```
����������post�����������ÿ��ִ�����֮���ټ���ִ����һ������ִ�е�ͬʱҲ�����������������ִ�У���������д������ȥҲ����ͬ�������ӣ��ǲ��Ǹо�������������ֻ��Ҫһ��������������Զ�ִ�еķ�������ÿ���첽���֮���Զ�ִ����һ��next()�ķ���������Ҫ��Promise��ϣ�������д��һ��ʵ�ַ�������ʵ�ֵķ�����ֹһ�֡�
``` javascript
// fn ��һ��generator����
function generator(fn){
	let a = fn()// ����״̬��
	function run(data){
		if(data.done) return
		data.value.then(data => {
			a.next(data)
		})}
	run(a.next())
}

function* async(){
	let a = post('.....') // ����A ����һ��promise
	// ��������A�Ľ��a
	let b = post('.....') // ����B ����һ��promise
	// ��������B�Ľ��b
	����������
}
generator(async)// ���� ����A������B�ͻ�˳��ִ�С�
```
����д�첽�Ͳ���Ҫ����̫��������򣬽����������ұ������������ͬ���߼���������ֻص������Ļص���������promise�ö��.then.catch�����ں�����ά���������ĵ��Ķ���ʮ���Ѻá�
### async/await