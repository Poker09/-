# JavaScript Decorators
## decorators ��ʲô
decorators����ES7�еĸ�����԰�������һ������������Ŀ�꺯�������ϣ�Ȼ�������һϵ�в�������һ���µĺ������ࡣ
``` javascript
@something
function doing(){
	...
}
```
��������ʹ��װ������������doing�����ϣ��������ʽ��ʵ����������������
``` javascript
let doing = function (){
	...
}
doing = something(doing )
```
�������ǰ�doing����������something����Ȼ�󷵻�һ�µ�doing����������µ�doing��������something�Ĵ����Ѿ������һЩ�µ���Ϊ��

## ʹ�� decorators

### ����
��Ϊdecorators��ES7���﷨������Ҫʹ��babel�����
1. ��װ @babel/plugin-proposal-decorators
``` javascript
yarn add @babel/plugin-proposal-decorators
```
2. ����
``` javascript
// package.json
"babel": {
  "plugins": [
    [
	 "@babel/plugin-proposal-decorators", 
	 {
	   "legacy": true
	 }
    ]
  ]
}
```
�����Ϳ�������Ŀ��ʹ��װ������

### ����

#### �����ں���
���������ں����ϵ�װ������ʹ�õ���ES5��Object.defineProperty ������ͨ�����ƶ�����������������������
``` javascript
	Object.defineProperty(obj, prop, descriptor)
```
Object.defineProperty������������������
- Ŀ�����
- ������
- ���Ե�������

װ��������������ͨ�����������ı���������ǰ���ԡ�
``` javascript
	function something (obj,prop,descriptor){
		let _value = descriptor.value;
		descriptor.value = function () {
			... // ����һ
			_value()
			...// ������
		}
	}
	
	@something
	function doing(){
		...
	}
```
������doing�����ϼ���װ����something��������ԭ������֮ǰ�����˲���һ��֮�������˲��������γ���һ���µĺ���������Ҳ�����޸�����������������writabled�޸����Ŀɶ��ԣ��ȵȡ�

#### ��������
���������ϱȽϼ򵥾��Ǵ������౾������ͨ���޸����prototype�����������ࡣ
``` javascript
import Immutable from 'immutable'

function shouldComponentDecorators(target) {
   const compareEqual = function (objA, objB) {
        if (objA === objB || Immutable.is(objA, objB)) {
            return true
        }

        if (typeof objA !== 'object' || objA === null ||
            typeof objB !== 'object' || objB === null) {
            return false;
        }

        const keysA = Object.keys(objA);
        const keysB = Object.keys(objB);

        if (keysA.length !== keysB.length) {
            return false;
        }

        for (let i = 0; i < keysA.length; i++) {
            if (keysB.indexOf(keysA[i]) === -1) {
                return false;
            }
            if (!Immutable.is(objA[keysA[i]], objB[keysA[i]])) {
                return false
            }
        }
        return true
    };
	target.prototype.shouldComponentUpdate = function (nextProps, nextState, nextContext) {
		return !compareEqual(this.state, nextState) || !compareEqual(this.props, nextProps)
	}
}
```
�����ʵ����һ����react������shouldComponentUpdate�������ڷ�����װ��������ʹ����ֻ��Ҫ�ڴ���react��ǰ������
@shouldComponentDecorators�Ϳɸ�������ʮ�ַ��㡣
### ���Ӳ���
���ǿ�����Ҫͬһ��װ������ͬ����������������һЩ���ƻ�ֵ������ͨ�����ݲ���ʵ��
``` javascript
@something(true)

// ����
function something (value){
 return function(target, key, descriptor) {
	descriptor.value = function () {
		if(value) 	... // ����һ
		else ... // ������
		_value()
	}
  }
}

// ��
function something (value){
  return function(target) {
	target.prototype.value= value
  }
}
```

## ����
decorators ��ʹ�õĳ����ܶ����װ���ò�������װ�ظ����룬Ȩ�޿��ƣ�·�ɵȵȡ�
Ŀǰ�и� core-decorators ��https://github.com/jayphelps/core-decorators�����Ѿ�������ܶ����õ�װ������
�������ճ������п����ܽ���ȡ���Լ���װ�����⣬������Ч�������������顣

## �ܽ�
ES7�¼����װ�������Կ��������Ǽ򻯴��룬���Ӹ��ã����Ӵ���Ŀ�ά���ԡ�
