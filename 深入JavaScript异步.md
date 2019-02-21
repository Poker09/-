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
����Ƕ��ʮ�ָ��ӵĻص������ǳ�����ά��������������ֻ��д�˵�������ټ������е��߼�������δ���ͻ���ʮ�֡��Ӵ󡯣���������һ��һ���Ƕ�����������Ļ������ཻ�ڣ������ʮ��ǿ��������Ҫ�����е�ĳһ��ʱ��Ҫ�����ϼ�����¼����ⲻ��������Ҫ�ġ����Իص�������ֻ��һ���ʱ��ʹ����ѣ���������²��Ƽ�ʹ�á�
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
Promise���ľ���״̬�ĸı䣬��ִ�в�ͬ�Ļص���������ص����������������һ��ȫ�µ�API���ڴ�����첽�����ʱ��ʮ�����ã��ڴ������д�ϣ���ʽ��Ҳ�Ȼص���������Ծʽ��������ף����Ƕ��صĴ������һЩAPI��Ҫ���������ʹ�úá�
### Generator�첽
### async/await