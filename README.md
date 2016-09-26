# prototype
```
function Person(name){
    this.name=name;
    this.color=['red','blue'];
}
Person.prototype.say=function(){
    console.log(this.name+'in func');
}
function Worker(name){
    Person.call(this,name);
    this.age=20;
}
Worker.prototype=new Person();  //重写原型对象
console.log(Worker.prototype.construtor);
Worker.prototype.construtor=Worker;
console.log(Worker.prototype.construtor);
var worker1=new Worker('小明');
var worker2=new Worker('小刚');
worker1.color.push('black');
console.log(worker1.color);
console.log(worker2.color);
worker1.say();
worker2.say();
```
组合继承：`有时候也叫做伪经典继承，其主要思路是：使用原型链继承原型上的属性和方法，通过借用构造函数实现对实例属性的继承。`
 可以看到_worker1_和_worker2_既继承了私有的引用值属性，也继承了原型上的共享方法，这种组合式继承避免了原型链(实例引用值共享)和借用构造函数（无法继承原型上的属性方法）的缺点，融合了它们的优点，成为javascript中最常用的继承模式。
    但是这种方法仍然是有缺点的：在继承的工程中调用了两次父类构造函数，第一次是在给子类的原型复制父类构造函数实例化的时候（Worker.prototype=new Person()），第二次是在子类构造函数中调用了一次（ Person.call(this,name)）。这就会带来一个问题：其实在第一次调用的时候，子类的原型上其实已经有父类构造函数的属性了，只不过我们只是早构造函数中将相同的属性给覆盖掉了，这就是这种方法的小小的一个问题，下次将介绍另一种更好的方法解决这个问题，敬请期待。
