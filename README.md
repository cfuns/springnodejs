springnodejs
============

���� : solq

blog : http://www.cnblogs.com/solq/p/3574640.html

1.ֻ��Ҫ���  ws Controller �ļ�����,�����Զ�ע�� Controller

2.path ·����������������Զ�ע��

3.���������ʽת��������չת������

4.���������ֶ��Զ�ע��

5.������ʼ��ִ��

6.aop ʵ�ַ�������

7.url ���طַ�

�����Ǿͷ�spring ����

git : https://github.com/solq360/springnodejs

 

д���ĵ��������ܲ����ף���ҽ���һ�°�

�����Դ��

�������� nodejs ���� ip ��ѯСӦ�õģ�����ʱ�����Űѻ���Ū������Ӧ�ã�û�뵽�������žͱ�� spring ��

���˸о��Լ��������Ķ�������ͦţ�ģ�����Ӧ��û��������

��JS д�� spring �������������Ҿ���ţ

 

����spring ��ʲô������������°�

��������򵥽���һ�¼������ĸ�������ұ���ˮƽҲ���ޣ����ڳ�������Ҳֻ������ˮƽ����û�ﵽ���Σ���ʲô���������¡�

IOC : ��ת����
--------------------

��ͳд���뷽ʽ �� ��
```
var a={
    b : {},
    c : {},
    d : {}
}

var d ={
    da : 'xxx',
    db : 'ccc',
}

//�����Ҫ��A���������ǲ����Ƚ� A ���������ȫ����ʼ�����ܹ���������

a.b = b.da;
a.c = b.db;
....
a.z = b.z
```
�����˼���������Ҫ���һ�����ܣ���Ҫ�߰˸�ģ�飬ÿ��ģ��ƽ��Ҫ�õ����������/�����࣬ÿ������/���� ����Ҫ�õ� ������ ����/���� �����ټ������ĸ�������Դ�������ÿ���඼��һ��ѵ�����Ҫ��ʼ����������Ŀ���ж���ʮģ�顣

�������ȥ����Ļ������������Щ���ó������������Ǽ���ô���ɵ��°�

˵������� ioc��ôʵ����Ҳ���˽����Ҳ���ѧJAVA �ģ���ֻ֪�����Ĵ������ٰ��Ҵ��������ϵ��¼���

�Ǻã�������ô�ó����������溣�������������أ� �뿴JS ��ʵ�� ioc
```
var ar=[];
//���� 1
var o1={
    id:'o1',
    o2:null
}
//���� 2
var o2={
    id:'o2',
    o1:null
}
ar.push(o1);
ar.push(o2)

var ioc={

}
//ע������
for(var i in ar){
    var obj=ar[i];
    ioc[obj.id]=obj;
}

//���� �����Զ�ע��
for(var i in ioc){
    var obj = ioc[i];

    for(var j in obj){
        if(j!='id'){
            obj[j]=ioc[j];
        }
    }
}

console.log(ioc,o1,o2)
```
û��������ô�򵥡�ÿ�����������Լ���ID ��ʶ��ֻҪ����������λ����ֹ���ǡ�

��������Ŀ�ĺ��Ĵ��� AppContext ��������������Ŀ���е�������

��ô���оͼ����������� : ����ID ������������ע������������һ����ͬ�������� �� ����Ĺ����뿴����ʵ�ְ�
```
AppContext={
        getKey : function(key){
            key = key.trim();
            key = key[0].toLowerCase() + key.substring(1,key.length);
            return key;
        },
        findContainer : function(key){
            key = this.getKey(key);
            return this.data[key];
        },
        addContainer : function(id,container){
            id = this.getKey(id);
            container.id= id;
            if(this.data[id]!=null ){
                _error(" injection key is has : " ,id);
                return;
            }
            this.data[id] = container;
        },
        findInjectionOfType : function(include,exclude,callBack){
            for(var i in this.data){
                var container = this.data[i];
                if(container.injectionType==null){
                    continue;
                }
                var injectionType = container.injectionType;
                
                if(include!=null && include.indexOf(injectionType)<0){
                    continue;
                }
                
                if(exclude!=null && exclude.indexOf(injectionType)>-1){
                    continue;
                }
                
                callBack(container);    
            }
        },
        data : {}
    }
```

������˵��ע������һЩ���̣�

1.scan ioc

2.auto  injection field

3.init run

1.����Ҫע����Щ�ǿ���ע��ģ���Щ��Ҫ���˵��ģ���Щ�����Ƿֱ���ʲô���͡�����Ļ��߷��񣬿��ƣ����߹��������������õȵ�

���ע���������ʲô���ȵ�һ�������Ҫ��������Ա�������࣬���������Щ��

2.ע����ɺ󣬽����������Զ�ע�����ԣ���������ʽ��ʶ��������Щ�ǿ���ע��ģ��뿴ʾ��
```
{
    auto_field1:null,
    auto_field3:null,
    auto_field4:null,
    auto_field5:null,
    auto_field6:null,
    auto_field20:null,
    postConstruct : function(){
    	debug('init=========================================');
    }
};
```
ͨ�� auto_(����ID)  ��ע��

3.ע�����ˣ�������������ʼ������Լ�׼������

������̿��Գ������������
```
_scan();
_auto_injection_field();
_init();
 ```

 

 

�Զ�ɨ�裬�����JQUERY ��֪���ɣ�$('CSSѡ����') ������ɨ�赽һ���DOM���� $('id') $('class')

���ܽ���һ��

������ʽ�����Щ����/�ļ� �����Ǳ�ɨ�赽��

�����뿴��Ŀ����ʵ��

ɨ������ 
```
var appConfig={
    /**auto scan config**/    
    scan :{
        './core' : {
            injectionType : 'core'
        },
        './config' : {
            injectionType : 'config'
        },
        './aop' : {
            injectionType : 'aop'
        },
        './service' : {
            injectionType : 'service'
        },
        './ws' : {
            filter : '\\ws', //url ���� ������
            injectionType : 'controller',
            //include : [],
            exclude : ['./ws/test/test1.js']
        }
    } 
};
 ```

��û��ע�⵽ injectionType ������ڣ�

��Ŀǰ�ǰ�Ŀ¼�������������͵ġ���Щ��ҿ�����������չ�Լ����������ͣ�ע����� ��ͨ�� AppContext.findInjectionOfType ɨ��

��������Ŀʵ�� ioc ����

```
var _injection = function(filePath,container){
    var id = container.id;
    if(id == null){
        id =_path.basename(filePath).replace('.js','');            
    }     
    container.filePath = filePath ;     
    AppContext.addContainer(id,container);     
    return container;
}

var _auto_injection_field = function(){
    for(var id in AppContext.data){
        if(id == 'appContext'){
            continue;
        }
        var container = AppContext.findContainer(id);
        
        for(var field in container){
            if(field.indexOf('auto_')==0){
            
                var checkFn = container[field];
                if(typeof checkFn == 'function'){
                    continue;
                }
                var injectionKey = field.replace('auto_','');
                
                if(AppContext.findContainer(injectionKey)==null){
                    _error('injection field not find id : ',field, id );
                }else{
                    container[field] = AppContext.findContainer(injectionKey);                
                    debug("injection field : ",injectionKey,id )
                }            
            }            
        }        
    }
}

var _init = function(){
    //Ϊʲô��������ʼ���׶���    
    //postConstruct ΪӦ�ò��ʼ����������������չ�Ļ�����Ҫ��Ӧ�ò��ʼ��֮ǰ׼���������������˰�
    for(var id in AppContext.data){
        var container =AppContext.findContainer(id);
        container.awake!=null && container.awake(AppContext);
    }
    
    for(var id in AppContext.data){
        var container = AppContext.findContainer(id);
        container.start!=null && container.start(AppContext);
    }
    
    for(var id in AppContext.data){
        var container = AppContext.findContainer(id);
        container.postConstruct!=null && container.postConstruct(AppContext);
    }
}

var _scan = function(){
    webHelper.scanProcess(appConfig.scan,'.js',function(filePath,target){
        var container=require(filePath); 
        
        //injectionType ���ҹ����õ�
        
        if(container.injectionType==null){
            var injectionType= target.injectionType;
            if(injectionType == null){
                injectionType = 'service';
            }
            container.injectionType = injectionType;
        }
        
        //add filter ������
        if(target.filter!=null){
            container.filter = target.filter;
        }
        
        var injectionType = container.injectionType ;
        var id=_injection(filePath,container).id;
        debug( "injection : ",'[',injectionType,']','[',id,']', filePath);
    });
}

_scan();
_auto_injection_field();
_init();
```
AOP ���� ����������
--------------------
��һ����˵���Ʒ��˰ɣ��Ǻ�Ҳ������

����������һ�£�
����д�Ĵ������ձ��
```
a();
b();
c();
d();
```
CPU�������¶�ȡִ�У���С��λ����Ϊ����
�����˼��һ�£��������Ǵ�������ִ�еģ����������Ŀ���ڣ�Ҫ���ĳЩ���ܣ�������������������ǲ��ǵ��޸�ԭ�����ļ������������ƻ�ԭ���Ĵ��룬���ܻ����δ֪��BUG�����ǳ���Ա������µ���
```
a();
e();
b();
c();
d();
```
���ϴ���������
```
a();
newFn =function(){
	e();
	b();
}
newFn();
c();
d();

or


newFn =function(){
	a();
	e();
}
newFn();
b();
c();
d();
```
�����ǲ��ǲ����ƻ�ԭ���Ĵ��밡�� 

��������������̣��ǵ�ûʲô����ģ��ҵ�ִ�еĹؼ��㣬�����Լ�������߼����������֮ǰִ�л���֮��ִ�У�������չ���쳣ִ�еȵ�
------------
�����AOP�ĺ���˼�룬�Ҳ��������е��鼮Ϊʲô����д���ģ���

��������window���� ���ӣ��ǲ��Ǿ����е����ࣿ��
����һ��Ӧ���Ǹı�ԭ��ִ�з������������/������� ������������ת��Ӧ�ú���������:
```
var a = function(int a,Date b){
	return int c;
}

newa=function(int a,string b){
	b = Date.str2date(b);
	var c=a(a,b);
	return c+'';
}

aop.filter( if(call a?) call newa; );
```

�ҿ���һЩ�鼮�����򲹶������������

��������Ŀaopʵ�ִ��� :

�ȿ�AOPӦ�� :
```
module.exports = {	
	before : {
		'TestService.testAop' : function(originalFuncton,callObj,args){
			console.log('aop this is testAop before ==================');
			console.log('aop test this value',this.testFiled);
			console.log('aop arguments : ',originalFuncton,args);
		}
	},
	after : {		
		'TestService.testAop' : function(){ //TestService ��Ҫ���ص������� testAop �����صķ���
			console.log('aop this is testAop after ==================');			
		}
	},
 
	'testFiled' :'testFiled',
	postConstruct : function(){
		console.log('aop postConstruct');
	},
	preDestroy  : function(){
		console.log('preDestroy');
	}
};

```

aop����JS
```
/**
 * @author solq
 * @deprecated blog: cnblogs.com/solq
 * */
var debug = require('../core/util/debug.js').debug,
	_error = require('../core/util/debug.js').error;

module.exports = {

	awake : function(AppContext){
		var $this=this;
		AppContext.findInjectionOfType(null,null,function(container){
			$this.register(container,AppContext);
		});
	},
	//public
	register : function(container,AppContext){
		for(var key in container.before){ 
			var filter = container.before[key];
			this._aop(key,'before',filter,container, AppContext); 
		}
		
		for(var key in container.after){
			var filter = container.after[key];
			this._aop(key,'after',filter,container,AppContext); 
		}
		
		for(var key in container.error){
			var filter = container.error[key];
			this._aop(key,'error',filter,container,AppContext); 
		}
	},
	
	//private
	_aop : function(key,aopType,filter,thisObj,AppContext){
		var sp = key.split('.'),
				id = sp[0],
				fnName = key.substring(key.indexOf('.')+1, key.length );
		var container=AppContext.findContainer(id);
		if(container==null){
			_error("aop not find container : ",key, " id :",id);
			return;
		}
		
		var originalFuncton =null;
		try{
			originalFuncton = eval('container.'+ fnName);
		}catch(e){
			_error(e);
			_error("aop not find originalFuncton: ",key, " id :",id );
			return;
		}	
 		
		if(originalFuncton==null){
			_error("aop not find originalFuncton: ",key, " id :",id );
			return;
		}
		
		if(typeof originalFuncton!= "function"){
			_error("aop originalFuncton is not function ",key, " id :",id );
			return;
		}		
		
		var newFuntion=null;
		switch(aopType){
			case 'error':
				newFuntion=function(){
					try{
						originalFuncton.apply(container,arguments);
					}catch(e){
						filter.apply(thisObj,arguments);
					}					
				}
			break;			
			case 'after':
				newFuntion=function(){
					var result=originalFuncton.apply(container,arguments);
					filter.apply(thisObj,arguments);
					return result;
				}
			break;
			case 'before':
				newFuntion=function(){
					//debug("originalFuncton : " , originalFuncton.toString());
					var isCallFlag=filter.call(thisObj,originalFuncton,container,arguments);
					
					if(!isCallFlag){
						return originalFuncton.apply(container,arguments);
					}										
				}
			break;
		}	
		
		container[fnName]=newFuntion;		
	}
};
```

���ˣ�Ŀǰ��д������