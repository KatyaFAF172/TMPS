# Laboratory work Nr.1

<h2>Creational patterns, structural pattern, behavioral pattern</h2>
===

<h3>_Members Group:_</h3>
1. Cretu Dumitru
2. Ejova Ecaterina
3. Galaju Elizabet
4. Scebec Mihai

<h4>Creational patterns:</h4>

1. Implementing Abstract Factory Pattern and Factory Method

To implement this pattern we first created the interface _Machine_, which has the method drive.
Then we created two interfaces which implement _Machine, Laptop and Smartphone_. Each those interfaces have
two classes that implement them, _LaptopDev, LaptopProd, SmartphoneDev, SmartphoneProd_. Those classes extend the
_ClonableMachines class_.

So the setup is done, because we want to isolate the classes _LaptopDev, LaptopProd, SmartphoneDev_,
_SmartphoneProd_, we will create the interface _AbstractFactory_, which will have the methods _createLaptop_
and _createSmartphone_. This interface will be implemented by the factory classes _ProductionFactory_ and
_DevelopFactory_.

To isolate these classes even more, the class _Factory Producer_ will be created. This class has the
method _getFactory_ which will take as parameter a string - _dev_ or _prod_ and will return an instance
of the factory class we demand.

To test if everything works, the following test will be executed:

```java
@Test
    void checkFactory() {
        //dev
        FactoryProducer factoryProducer = new FactoryProducer();
        AbstractFactory devFactory = factoryProducer.getFactory("dev");

        Laptop devLaptop = devFactory.createLaptop("Asus", "UX433FA");
        devLaptop.drive();

        System.out.println("------------------------------------------------------------------------------------------------------");

        //prod
        AbstractFactory prodFactory = factoryProducer.getFactory("prod");

        Smartphone prodSmartphone = prodFactory.createSmartphone("Asus", "UX433FA");
        prodSmartphone.drive();
    }
```

2. Implementing Builder Pattern

We implemented the builder pattern for the classes _LaptopDev, LaptopProd, SmartphoneDev, SmartphoneProd_, by
creating the classes _LaptopDevBuilder, LaptopProdBuilder, SmartphoneDevBuilder, SmartphoneProdBuilder_. Each class
has a constructor which takes the parameters name and model, getter and setters for the class fields:
_mName, mModel, mYear, mPrice, mDescription_; and the method that returns a new instance of the
class the builder is for.

To test if everything works, the following test will be executed:

```java
@Test
    void checkBuilder() {
        LaptopDev laptopDev1 = new LaptopDevBuilder("Asus", "UX433FA").setPrice(19000).setDescription("Intel Core i5, Windows 10, 8 GB / 512 GB").setYear(2019).createLaptop();
        laptopDev1.drive();

        SmartphoneProd smartphoneProd = new SmartphoneProdBuilder("Asus", "UX433FA").setPrice(19000).setDescription("Intel Core i5, Windows 10, 8 GB / 512 GB").setYear(2019).createSmartphone();
        smartphoneProd.drive();
        System.out.println("---------------------------------------------------------------------------------------------------");
    }
```
3. Implementing Prototype Pattern

We implemented the prototype pattern using an object pool, we created the class )_MachinePool_,
which has the field _defaultMachines_, the methods: _getMachine_ which has as parameter the index
of the machine we want, and returns a clone of the indicated machine, and the method _loadMachines_
which populates the HashMap _defaultMachines_ with four predetermined values.

To test if everything works, the following test will be executed:

```java
@Test
    void checkObjectPool() throws CloneNotSupportedException {
        MachinePool machinePool = new MachinePool();
        machinePool.loadDefaultLaptops();

        Assert.assertNotEquals(machinePool.getMachine(1).hashCode(),machinePool.getMachine(1).hashCode());

        machinePool.getMachine(1).drive();
        machinePool.getMachine(2).drive();
        machinePool.getMachine(3).drive();
        machinePool.getMachine(4).drive();
        System.out.println("-----------------------------------------------------------------------------------------------------");

    }
```

4. Implementing Singleton Pattern

We implemented this pattern by creating the class _ShopingCart_. If we are change the context of
out application to an internet store, it is logical that we only have one instance of a ShoppingCart
class. This class has the field _INSTANCE_ which contains an instance of the class, the field _mMachines_
which is a list of machines that the shopping cart contains, a constructor, the methods: _getInstance_
which returns the _INSTANCE_ field of the class, _getachines_ which returns the list of machines that are
in the cart, addachine which adds a machine to the list.

To test if everything works, the following test will be executed:

```java
@Test
    void checkSingleton() throws CloneNotSupportedException {
        MachinePool machinePool = new MachinePool();
        machinePool.loadDefaultLaptops();

        ShoppingCart shoppingCart = ShoppingCart.getInstance();

        shoppingCart.addMachine(machinePool.getMachine(1));
        shoppingCart.addMachine(machinePool.getMachine(3));

        ShoppingCart shoppingCart2 = ShoppingCart.getInstance();
        Assert.assertEquals(shoppingCart.hashCode(),shoppingCart2.hashCode());

        System.out.println(shoppingCart.getMachines().toString());


    }
```

<h4>Structural pattern:</h4>

5. Implementing Composite Pattern

Composite design patten allows you to have a tree structure and ask each node in the tree
structure to perform a task.You can take real life example of a organization.It have general managers
and under general managers, there can be managers and under managers there can be developers.Now
you can set a tree structure and ask each node to perform common operation like _getSalary()_.

As described by Gof:
”Compose objects into tree structure to represent part-whole hierarchies.Composite lets client
treat individual objects and compositions of objects uniformly”.

Composite design pattern treats each node in two ways-Composite or leaf.Composite means it
can have other objects below it.leaf means it has no objects below it.

To test if everything works, the following test will be executed:

```java
@Test
    void checkComposite() {
        LaptopConcurentsObj laptopConcurents = new LaptopConcurentsObj("Asus", "3");
        laptopConcurents.addMachine(new LaptopImpl("Dell ", "Inspiron Gaming 15 G3"));
        laptopConcurents.addMachine(new LaptopImpl("HP", "EliteBook 830"));

        System.out.println(laptopConcurents.toString());
        System.out.println("--------------------------------------------------------------------------------------------------------------");
    }
```

<h4>Behavioral Patterns:</h4>

6. Implementing Template Pattern

In Template pattern, an abstract class exposes defined way(s)/template(s) to execute its meth-
ods. Its sub-classes can override the method implementation as per need but the invocation is to be

in the same way as defined by an abstract class. This pattern comes under behavior pattern category.
To test if everything works, the following test will be executed:

```java
@Test
    void checkTemplate(){
        SmartphoneImpl smartphone = new SmartphoneImpl("Samsung Galaxy", "Xiaomi");
        smartphone.play();
        System.out.println("---------------------------------------------------------------------------------------------------------------");
    }
```

