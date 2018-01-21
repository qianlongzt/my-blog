<div class="entry-content">

在类中定义的变量称之为属性，通常属性跟数据库中的字段有一定的关联，因此也可以称作“字段”。属性声明是由关键字 public，protected 或者 private 开头，后面跟一个普通的变量声明来组成。属性的变量可以设置初始化的默认值，默认值必须是常量。

访问控制的关键字代表的意义为：

public：公开的
protected：受保护的
private：私有的
<pre class="code">class Car {
    //定义公共属性
    public $name = '汽车';

    //定义受保护的属性
    protected $corlor = '白色';

    //定义私有属性
    private $price = '100000';
}</pre>
默认都为public，外部可以访问。一般通过-&gt;对象操作符来访问对象的属性或者方法，对于静态属性则使用::双冒号进行访问。当在类成员方法内部调用的时候，可以使用$this伪变量调用当前对象的属性。
<pre class="code">$car = new Car();
echo $car-&gt;name;   //调用对象的属性
echo $car-&gt;color;  //错误 受保护的属性不允许外部调用
echo $car-&gt;price;  //错误 私有属性不允许外部调用</pre>
受保护的属性与私有属性不允许外部调用，在类的成员方法内部是可以调用的。
<pre class="code">class Car{
    private $price = '1000';
    public function getPrice() {
        return $this-&gt;price; //内部访问私有属性
​    }
}</pre>
<pre>&lt;?php class Car{ //在这里定义一个共有属性name public $name='汽车'; protected $price='1000'; private $color='blue'; } $car = new Car(); //在这里输出$car对象的name属性 echo $car-&gt;name;</pre>
&nbsp;

静态属性与方法可以在不实例化类的情况下调用，直接使用<code class="marker">类名::方法名</code>的方式进行调用。静态属性<strong>不允许</strong>对象使用-&gt;操作符调用。
<pre class="code">class Car {
    private static $speed = 10;
    
    public static function getSpeed() {
        return self::$speed;
    }
}
echo Car::getSpeed();  //调用静态方法</pre>
静态方法也可以通过变量来进行动态调用
<pre class="code">$func = 'getSpeed';
$className = 'Car';
echo $className::$func();  //动态调用静态方法</pre>
静态方法中，$this伪变量不允许使用。可以使用self，parent，static在内部调用静态方法与属性。
<pre class="code">class Car {
    private static $speed = 10;
    
    public static function getSpeed() {
        return self::$speed;
    }
    
    public static function speedUp() {
        return self::$speed+=10;
    }
}
class BigCar extends Car {
    public static function start() {
        parent::speedUp();
    }
}

<strong>BigCar::start();</strong>
echo BigCar::getSpeed();</pre>
使用extend完成类的进程
<pre>&lt;?php class Car { public $speed = 0; //汽车的起始速度是0 public function speedUp() { $this-&gt;speed += 10;
        return $this-&gt;speed;
    }
}
//定义继承于Car的Truck类
class Truck extends Car{
    public function speedUp(){
        $this-&gt;speed=parent::speedUp()+50;
    }
}
$car = new Truck();
$car-&gt;speedUp();
echo $car-&gt;speed;</pre>
</div>
<footer class="entry-footer"><span class="posted-on"><span class="screen-reader-text">发布于 </span></span></footer>
