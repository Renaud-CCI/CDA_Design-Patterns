# Les Designs Patterns 🚀

Aujourd'hui, nous allons plonger dans le monde fascinant des **Design Patterns**, (patrons de conception en français). 🤖

**Les Design Patterns** représentent une collection de solutions éprouvées et élégantes à des problèmes récurrents dans la conception logicielle.
Ils sont le fruit de l'expérience et des meilleures pratiques accumulées par les développeurs au fil des années. 👨‍💻👩‍💻

**Les Design Patterns** sont souvent classifiés en trois catégories fondamentales : création, structure, et comportement. Chacune répond à une dimension différente de la problématique de conception logicielle :

1. **Création** 🏗️ : Ces patterns concernent le processus de création d'objets, en insistant sur le fait de les créer de manière adaptée à la situation.
2. **Structure** 🌉 : Ils s'attachent à composer des classes et objets pour former des structures de grande envergure.
3. **Comportement** 👀 : Ces patterns se focalisent sur la communication entre objets, en s'efforçant d'assurer que cette communication est bien organisée et adaptée aux besoins.

Le célèbre livre "Design Patterns: Elements of Reusable Object-Oriented Software", communément appelé le "Gang of Four" (GoF), a introduit 23 patterns fondamentaux qui sont devenus des références incontournables. ☝️📚

L'apprentissage des Design Patterns vous apportera de multiples avantages, tels que :

- **Amélioration de la maintenabilité et de l'évolutivité** 🛠️: en utilisant des solutions normalisées, vous pouvez bâtir des logiciels plus faciles à maintenir et à faire évoluer.
- **Meilleure communication** 💬: Les motifs fournis par les patterns facilitent la communication entre développeurs à travers un vocabulaire commun.
- **Optimisation du développement** ⏱️: En vous appuyant sur des solutions qui ont fait leurs preuves, vous évitez de réinventer la roue, ce qui optimise le temps de développement.

L'objectif de ce cours sera de vous familiariser avec ces concepts, de comprendre leur utilité, et surtout, de savoir comment et quand les appliquer efficacement dans vos projets.

Pour commencer notre parcours, nous examinerons quelques patterns individuellement, en découvrant leur structure et leur raison d'être à travers des exemples pratiques. Préparez-vous à découvrir tout un nouveau niveau de conception logicielle ! 🎓

**Prêts à démarrer ? Allons-y !** 👊💥

## Cours 📚️

### **[Les DesignPatterns](https://docs.google.com/presentation/d/1Ov-ZKnB1TjxrNv7Za1AJDNT6FGVweWv49WHOv2k-rO4)**

**[Cours OpenClassroom](https://openclassrooms.com/fr/courses/7415611-ecrivez-du-php-maintenable-avec-les-principes-solid-et-les-design-patterns/7419805-quest-ce-quun-design-pattern)**

### Creationnal Pattern

- **[Singleton](https://docs.google.com/presentation/d/1Ha-KpwtNtXZNmPBJfEwv96dkKOzhpPDOAwswCUKotfk)**

- **[Builder](https://docs.google.com/presentation/d/10T4pWhrGmd4hTfCDSh2WcZhkWpCc1Ets5ggdOkrQd0A)**

- **[Factory](https://docs.google.com/presentation/d/1pxTjFeULbp52ldU4ibZkpD2Fqj0KsVS3r8-7QgAo4O4)**

### Structural Pattern

- **[Adapter](https://docs.google.com/presentation/d/1F3j_LFkyL-o4z7zmciCRoqJZHp0w9OndTKwsRjeGQ8g)**

## Livecodes 👨‍🏫

<details>
  <summary><b>Composition VS Héritage</b></summary>
  
  ```php
  <?php

  class A{
      public function test(){
          echo 'test';
      }
  }

  class C{
      public function test3(){
          echo 'test3';
      }
  }

  /*---------------------------------------*/
  /* HERITAGE */
  /*---------------------------------------*/

  class B extends A{
      public function test2(){
          echo 'test2';
      }
  }

  //B ne pourra avec l'héritage jamais contenir les fonctionnalités de A et de C

  /*---------------------------------------*/
  /* COMPOSITION */
  /*---------------------------------------*/


  class B{
      
      protected $a;
      protected $c;
      
      public function __construct($a, $c){
          $this->a = $a;
          $this->c = $c;
      }
      
      public function test(){
          echo $this->a->test()
      }
      
      public function test3(){
          echo $this->c->test()
      }

      public function test2(){
          echo 'test2';
      }
  }
  ```

</details>

<details>
  <summary><b>Factory</b></summary>

#### **<ins>Product Example</ins>**

<details style="margin-left:15px">
  <summary><b>Sans Factory</b></summary>

  ```php
  <?php

  class ConcreteProduct
  {
      protected $apiData;
      
      public function __construct($apiData){
          $this->apiData = $apiData;
      }
      
      public function useProduct()
      {
          echo "Inside ConcreteProduct:UseProduct()\n";
      }
  }


  class ConcreteProduct2
  {
      protected $apiData;
      
      public function __construct($apiData){
          $this->apiData = $apiData;
      }

      
      public function useProduct()
      {
          echo "Inside ConcreteProduct:UseProduct()\n";
      }
  }

  function apiCall(){
      //fetch data api
      return 'data';
  }

  $context = '1';

  function client(){
      $apiData = apiCall();
      if($context == '1')
          $product = new ConcreteProduct1($apiData);
      else
          $product = new ConcreteProduct2($apiData);
          
      //LOGIQUE DE NOTRE CODE
      $product->useProduct();
      
  }


  function client2(){
      $apiData = apiCall();
      if($context == '1')
          $product = new ConcreteProduct1($apiData);
      else
          $product = new ConcreteProduct2($apiData);
          
              
      //LOGIQUE DE NOTRE CODE
      $product->useProduct();
  }


  function client3(){
      if($context == '1')
          $product = new ConcreteProduct1();
      else
          $product = new ConcreteProduct2();
      
              
      //LOGIQUE DE NOTRE CODE
      $product->useProduct();
  }

  ?>

  ```

  </details>

  <details style="margin-left:15px">
  <summary><b>Factory Step 1</b></summary>

  ```php
  <?php

  interface IProduct{
      public function useProduct();
  }

  class ConcreteProduct implements IProduct
  {
      protected $apiData;
      
      public function __construct($apiData){
          $this->apiData = $apiData;
      }
      
      public function useProduct()
      {
          echo "Inside ConcreteProduct:UseProduct()\n";
      }
  }


  class ConcreteProduct2 implements IProduct
  {
      protected $apiData;
      
      public function __construct($apiData){
          $this->apiData = $apiData;
      }

      
      public function useProduct()
      {
          echo "Inside ConcreteProduct:UseProduct()\n";
      }
  }

  class ConcreteFactory{
      
      public function createProduct($context):IProduct
      {
          $apiData = apiCall();
          if($context == '1')
              $product = new ConcreteProduct1($apiData);
          else
              $product = new ConcreteProduct2($apiData);
          
          return $product;
      }
  }

  function apiCall(){
      //fetch data api
      return 'data';
  }

  $context = '2';

  function client(){
      $factory = new ConcreteFatory();
      $product = $factory->createProduct($context);
          
      //LOGIQUE DE NOTRE CODE
      $product->useProduct();
      
  }

  function client2(){
      $factory = new ConcreteFatory();
      $product = $factory->createProduct($context);
      
      //LOGIQUE DE NOTRE CODE
      $product->useProduct();
  }

  function client3(){
      $factory = new ConcreteFatory();
      $product = $factory->createProduct($context);
              
      //LOGIQUE DE NOTRE CODE
      $product->useProduct();
  }

  ?>
  ```

  </details>

  <details style="margin-left:15px">
  <summary><b>Complete Factory</b></summary>

  ```php
  <?php

  /*-- PRODUCT --*/


  interface IProduct{
      public function useProduct();
  }

  class ConcreteProduct implements IProduct
  {
      protected $apiData;
      
      public function __construct($apiData){
          $this->apiData = $apiData;
      }
      
      public function useProduct()
      {
          echo "Inside ConcreteProduct1:UseProduct()\n";
      }
  }


  class ConcreteProduct2 implements IProduct
  {
      protected $apiData;
      
      public function __construct($apiData){
          $this->apiData = $apiData;
      }

      
      public function useProduct()
      {
          echo "Inside ConcreteProduct2:UseProduct()\n";
      }
  }



  /*-- FACTORIES --*/



  interface IFactory{
      public function get($context);
  }

  class ConcreteFactory1 implements IFactory{

      protected function create(){
          $data = apiCall('https://qwant.fr');
          return new ConcreteProduct1($data);
          
      }
      
      public function get(){
          return $this->create();
      }
  }

  class ConcreteFactory2{

      protected function create(){
          $data = apiCall('https://google.com');
          return new ConcreteProduct2($data);
      }
      
      public function get(){
          return $this->create();
      }
  }


  /*-- DIRECTOR --*/


  class ProductFactoryDirector{
      
      public function createProduct($context):IProduct
      {
          if($context == '1'){
              $factory = new ConcreteFactory1();
          }
          else{
              $factory = new ConcreteFactory2();
              
          }
          
          return $factory->get();
      }
      
  }


  /*-- CODE --*/


  function apiCall($url){
      //fetch data api
      return 'data'.$url;
  }

  $context = '2';

  function client(){
      $factory = new ProductFactoryDirector();
      $product = $factory->createProduct($context);
          
      //LOGIQUE DE NOTRE CODE
      $product->useProduct();
      
  }


  function client2(){
      $factory = new ProductFactoryDirector();
      $product = $factory->createProduct($context);
      
      //LOGIQUE DE NOTRE CODE
      $product->useProduct();
  }


  function client3(){
      $factory = new ProductFactoryDirector();
      $product = $factory->createProduct($context);
      
              
      //LOGIQUE DE NOTRE CODE
      $product->useProduct();
  }
  ?>
  ```

  </details>

#### **<ins>Transporter Example</ins>**

  <details style="margin-left:15px">
  <summary><b>Transporter Factory Step 1</b></summary>

  ```php
  <?php
  interface ITransporter{
    public function useTransporter();
  }

  class Camion implements ITransporter
  {
      protected $speed = 0;
      protected $costs = 0;
      
      public function __construct($speed, $costs){
          $this->speed = $speed;
          $this->costs = $costs;
      }
      
    public function useTransporter()
    {
      echo "Je me déplace en Camion à la vitesse de : ".$this->speed." et au tarif de ".$this->costs."\n";
    }
  }


  class Avion implements ITransporter
  {
      protected $speed = 0;
      protected $costs = 0;
      
      public function __construct($speed, $costs){
          $this->speed = $speed;
          $this->costs = $costs;
      }

    public function useTransporter()
    {
      echo "Je me déplace en Avion à la vitesse de : ".$this->speed." et au tarif de ".$this->costs."\n";
    }
  }


  class TransporterFactory{
      public function createTransporter($transporter):ITransporter
      {
          if($transporter == 'Camion'){
              $speed = apiCallSpeed('Camion');
              $cost = apiCallCostsV2('Camion');
              $transporter = new Camion($speed, $cost);
          }else{
              $speed = apiCallSpeed('Avion');
              $cost = apiCallCostsV2('Avion');
              $transporter = new Avion($speed, $cost);
          }
          return $transporter;
      }
  }



  function apiCallSpeed($parameters){
      return rand();
  }

  function apiCallCostsV2($parameters){
      return rand();
  }



  $transporter = 'Camion';

  function client(){
      $transporterFactory = new TransporterFactory();
      $transporter = $transporterFactory->createTransporter($transporter);
      $transporter->useTransporter();
  }
  client();


  /* MAUVAIS */
  function client2(){
      if($transporter == 'Camion'){
          $speed = apiCallSpeed('Camion');
          $cost = apiCallCosts('Camion');
          $transporter = new Camion($speed, $cost);
      }else{
          $speed = apiCallSpeed('Avion');
          $cost = apiCallCosts('Avion');
          $transporter = new Avion($speed, $cost);
      }
      $transporter->useTransporter();
  }
  client2();


  function client3(){
      if($transporter == 'Camion'){
          $speed = apiCallSpeed('Camion');
          $cost = apiCallCostsV2('Camion');
          $transporter = new Camion($speed, $cost);
      }else{
          $speed = apiCallSpeed('Avion');
          $cost = apiCallCostsV2('Avion');
          $transporter = new Avion($speed, $cost);
      }
      $transporter->useTransporter();
  }
  client3();

  ?>
  ```

  </details>

  <details style="margin-left:15px">
  <summary><b>Transporter Factory Step 2</b></summary>

  ```php
  <?php

  interface ITransporter{
    public function useTransporter();
  }

  class Camion implements ITransporter
  {
      protected $speed = 0;
      protected $costs = 0;
      
      public function __construct($speed, $costs){
          $this->speed = $speed;
          $this->costs = $costs;
      }
      
    public function useTransporter()
    {
      echo "Je me déplace en Camion à la vitesse de : ".$this->speed." et au tarif de ".$this->costs."\n";
    }
  }


  class Avion implements ITransporter
  {
      protected $speed = 0;
      protected $costs = 0;
      
      public function __construct($speed, $costs){
          $this->speed = $speed;
          $this->costs = $costs;
      }

    public function useTransporter()
    {
      echo "Je me déplace en Avion à la vitesse de : ".$this->speed." et au tarif de ".$this->costs."\n";
    }
  }


  interface ITransporterFactory{
      public function getTransporter():ITransporter;
  }

  class CamionTransporterFactory implements ITransporterFactory
  {
      
      protected function create():ITransporter
      {
          $speed = apiCallSpeed('Camion');
          $cost = apiCallCostsV2('Camion');
          $transporter = new Camion($speed, $cost);
          return $transporter;
      }
      
      public function getTransporter():ITransporter
      {
          return $this->create();
      }
  }

  class AvionTransporterFactory implements ITransporterFactory
  {
      protected function create():ITransporter
      {
          $speed = apiCallSpeed('Avion');
          $cost = apiCallCostsV2('Avion');
          $transporter = new Avion($speed, $cost);
          return $transporter;
      }
      
      public function getTransporter():ITransporter
      {
          return $this->create();
      }
  }

  class TransporterFactoryDirector{
      public function createTransporter($transporter):ITransporter
      {
          if($transporter == 'Camion'){
              $factory = new CamionTransporterFactory();
          }else if($transporter == 'Avion'){
              $factory = new AvionTransporterFactory();
          }
          $transporter = $factory->getTransporter();
          return $transporter;
      }
  }



  function apiCallSpeed($parameters){
      return rand();
  }

  function apiCallCostsV2($parameters){
      return rand();
  }



  $transporter = 'Camion';

  function client(){
      $transporterFactoryDirector = new TransporterFactoryDirector();
      $transporter = $transporterFactoryDirector->createTransporter($transporter);
      $transporter->useTransporter();
  }
  client();

  function client2(){
      if($transporter == 'Camion'){
          $speed = apiCallSpeed('Camion');
          $cost = apiCallCosts('Camion');
          $transporter = new Camion($speed, $cost);
      }else{
          $speed = apiCallSpeed('Avion');
          $cost = apiCallCosts('Avion');
          $transporter = new Avion($speed, $cost);
      }
      $transporter->useTransporter();
  }
  client2();


  function client3(){
      if($transporter == 'Camion'){
          $speed = apiCallSpeed('Camion');
          $cost = apiCallCostsV2('Camion');
          $transporter = new Camion($speed, $cost);
      }else{
          $speed = apiCallSpeed('Avion');
          $cost = apiCallCostsV2('Avion');
          $transporter = new Avion($speed, $cost);
      }
      $transporter->useTransporter();
  }
  client3();



  ?>
  ```

  </details>

  <details style="margin-left:15px">
  <summary><b>Transporter Factory Step 3</b></summary>

  ```php
  <?php

  interface ITransporter{
    public function useTransporter();
  }

  class Camion implements ITransporter
  {
      protected $speed = 0;
      protected $costs = 0;
      
      public function __construct($speed, $costs){
          $this->speed = $speed;
          $this->costs = $costs;
      }
      
    public function useTransporter()
    {
      echo "Je me déplace en Camion à la vitesse de : ".$this->speed." et au tarif de ".$this->costs."\n";
    }
  }


  class Avion implements ITransporter
  {
      protected $speed = 0;
      protected $costs = 0;
      
      public function __construct($speed, $costs){
          $this->speed = $speed;
          $this->costs = $costs;
      }

    public function useTransporter()
    {
      echo "Je me déplace en Avion à la vitesse de : ".$this->speed." et au tarif de ".$this->costs."\n";
    }
  }


  interface ITransporterFactory{
      public function getTransporter():ITransporter;
  }

  class CamionTransporterFactory implements ITransporterFactory
  {
      
      protected function create():ITransporter
      {
          $speed = apiCallSpeed('Camion');
          $cost = apiCallCostsV2('Camion');
          $transporter = new Camion($speed, $cost);
          return $transporter;
      }
      
      public function getTransporter():ITransporter
      {
          return $this->create();
      }
  }

  class AvionTransporterFactory implements ITransporterFactory
  {
      protected function create():ITransporter
      {
          $speed = apiCallSpeed('Avion');
          $cost = apiCallCostsV2('Avion');
          $transporter = new Avion($speed, $cost);
          return $transporter;
      }
      
      public function getTransporter():ITransporter
      {
          return $this->create();
      }
  }

  class TransporterFactoryDirector{
      public function createTransporter($transporter):ITransporter
      {
          $factoryName = ucfirst(strotolower($transporter))."TransporterFactory";
          if(!class_exists($factoryName))
              throw new Exception('Factory Doesn\'t exists');
          $factory = new $factoryName();
          $transporter = $factory->getTransporter();
          return $transporter;
      }
  }



  function apiCallSpeed($parameters){
      return rand();
  }

  function apiCallCostsV2($parameters){
      return rand();
  }



  $transporter = 'Camion';

  function client(){
      $transporterFactoryDirector = new TransporterFactoryDirector();
      $transporter = $transporterFactoryDirector->createTransporter($transporter);
      $transporter->useTransporter();
  }
  client();



  /* MAUVAIS */

  function client2(){
      if($transporter == 'Camion'){
          $speed = apiCallSpeed('Camion');
          $cost = apiCallCosts('Camion');
          $transporter = new Camion($speed, $cost);
      }else{
          $speed = apiCallSpeed('Avion');
          $cost = apiCallCosts('Avion');
          $transporter = new Avion($speed, $cost);
      }
      $transporter->useTransporter();
  }
  client2();


  function client3(){
      if($transporter == 'Camion'){
          $speed = apiCallSpeed('Camion');
          $cost = apiCallCostsV2('Camion');
          $transporter = new Camion($speed, $cost);
      }else{
          $speed = apiCallSpeed('Avion');
          $cost = apiCallCostsV2('Avion');
          $transporter = new Avion($speed, $cost);
      }
      $transporter->useTransporter();
  }
  client3();



  ?>
  ```

  </details>
</details>

<details>
  <summary><b>Builder</b></summary>
  
  ```php
  <?php

  interface IHouse{
      public function setRoof($roof);

      public function setWalls($walls);
      
      public function setGarden($garden);
      
      public function setFloor($floor);
  }


  abstract class House implements IHouse
  {
      protected  $roof;
      protected  $walls;
      protected  $garden;
      protected  $floor;
      
      public function __construct(){}
      
      public function setRoof($roof){
          $this->roof = $roof;
      }

      public function setWalls($walls){
          $this->walls = $walls;
      }
      
      public function setGarden($garden){
          $this->garden = $garden;
      } 
      
      public function setFloor($floor){
          $this->floor = $floor;
      }    
      
      public function display() {
          var_dump(get_object_vars($this));
      }
  }

  class AmazingHouse extends House implements IHouse
  {

  }

  class NormalHouse extends House implements IHouse
  {
      
  }


  interface IHouseBuilder
  {
    public function create();
    public function buildRoof();
    public function buildWalls();
    public function buildGarden();
    public function buildFloor();
    public function getHouse():IHouse;
  }

  class AmazingHouseBuilder implements IHouseBuilder
  {
      protected $house;
      
    public function create(){
        $this->house = new AmazingHouse();
        return $this;
    }
    
    public function buildRoof(){
        $this->house->setRoof('gold');
        return $this;
    }
    
    public function buildWalls(){
        $this->house->setWalls(1000);
        return $this;
    }
    
    public function buildGarden(){
        $this->house->setGarden(true);
        return $this;
    }
    
    public function buildFloor(){
        $this->house->setFloor('fur');
        return $this;
    }
    
    public function getHouse():IHouse
    {
        return $this->house;
    }
  }

  class NormalHouseBuilder implements IHouseBuilder
  {
    protected $house;
      
    public function create(){
        $this->house = new NormalHouse();
        return $this;
    }
    
    public function buildRoof(){
        $this->house->setRoof('slate');
        return $this;
    }
    
    public function buildWalls(){
        $this->house->setWalls(4);
        return $this;
    }
    
    public function buildGarden(){
        $this->house->setGarden(false);
        return $this;
    }
    
    public function buildFloor(){
        $this->house->setFloor('wood');
        return $this;
    }

    public function getHouse():IHouse
    {
        return $this->house;
    }
  }


  class HouseDirector
  {
    private $builder;

    public function setBuilder(IHouseBuilder $obj)
    {
      $this->builder = $obj;
    }

    public function construct():IHouse
    {
      return $this->builder
                  ->create()
                  ->buildRoof()
                  ->buildWalls()
                  ->buildGarden()
                  ->buildFloor()
                  ->getHouse();
    }
  }


  class HouseStrategy{
      public function construct($houseType):IHouse
      {
          $director = new HouseDirector();
          if($houseType == 'amazing'){
              $houseBuilder = new AmazingHouseBuilder();
          }else{
              $houseBuilder = new NormalHouseBuilder();
          }
          $director->setBuilder($houseBuilder);
          $house = $director->construct();
          return $house;
      }
  }



  function client(){
      $houseStrategy = new HouseStrategy();
      $house = $houseStrategy->construct('normal');
      $house->display();
  }

  client();

  ?>
  ```

</details>

<details>
  <summary><b>Observer</b></summary>

  <details style="margin-left:15px">
    <summary><b>Example 1</b></summary>

  ```php

    <?php
    
    class Subject
    {
      private $observers = array();

      public function attach(Observer $obj)
      {
        array_push($this->observers, $obj);
      }

      public function detach(Observer $obj)
      {

      }

      public function notify()
      {
        for ($i = 0; $i < count($this->observers); ++$i)
          $this->observers[$i]->update();

      }
    }

    class ConcreteSubject extends Subject
    {
      private $state;

      public function setState($value)
      {
        $this->state = $value;
        $this->notify();
      }
      
      public function getState()
      {
        return $this->state;
      }
    }

    abstract class Observer
    {
      public abstract function update();
    }

    class ConcreteObserverA extends Observer
    {
      private $state;
      private $conSub;

      public function __construct(ConcreteSubject $obj)
      {
        $this->conSub = $obj;
        $this->conSub->attach($this);
      }

      public function update()
      {
        echo "Inside ConcreteObserverA::Update()\n";
        $this->state = $this->conSub->getState();
        echo "State = ", $this->state, "\n";
      }
    }

    class ConcreteObserverB extends Observer
    {
      private $state;
      private $conSub;

      public function __construct(ConcreteSubject $obj)
      {
        $this->conSub = $obj;
        $this->conSub->attach($this);
      }

      public function update()
      {
        echo "Inside ConcreteObserverB::Update()\n";
        $this->state = $this->conSub->getState();
        echo "State = ", $this->state, "\n";
      }
    }

    $conSubObj = new ConcreteSubject();
    $ObsObj1 = new ConcreteObserverA($conSubObj);
    $ObsObj2 = new ConcreteObserverB($conSubObj);
    $conSubObj->setState(1);

    ?>
  ```
  </details>

  <details style="margin-left:15px">
    <summary><b>Example 2 </b></summary>

  ```php
    <?php

    class RegistrationEvent{
        
        protected $observers = [];
        
        public function addObserver($observer){
            $this->observers[] = $observer;
        }
        
        public function notifyObserver($data){
            foreach($this->observers as $o){
                $o->notify($data);
            }
        }
        
    }

    interface IObserver{
        public function notify($data);
    }

    class DisplayRegistrationStatus implements IObserver
    {
        public function notify($data){
            echo "L'enregistrement a été un ".$data;
        }
    }


    class SendApiNotification implements IObserver
    {
        public function notify($data){
            //API CALL POUR RECUPERER DES INFOS
        }
    }

    function client(){
        $event = new RegistrationEvent();
        $event->addObserver(new DisplayRegistrationStatus);
        $event->addObserver(new SendApiNotification);
        
        $registration = false;
        /* Plein de code */
        if($registration == true){
            $event->notifyObserver('reussite');
        }else{
            $event->notifyObserver('echec');
        }
    }


    client();
  ```
  </details>
</details>

## Exercices 💥

**[Exercices Design Patterns](https://github.com/G404-CDA/Exercices-Design-Patterns)**

## Ressources 💼

 - ### **[La Bible 📖](https://refactoring.guru/)**
 - ### **[Généralité 📽️](https://www.youtube.com/watch?v=aXq05_mdCqE)**

### Cours Magistral ( assez complexe )

  - [**Part 1** - Design Patterns - Introduction](https://www.youtube.com/watch?v=atFLkqYefLQ&t=1611s)
  - [**Part 2** - Design Patterns - Pattern Strategy](https://www.youtube.com/watch?v=osI49NHcJm0)
  - [**Part 3** - Design Patterns - Pattern Strategy Implementation](https://www.youtube.com/watch?v=iM22mn8JeoI)
  - [**Part 4** - Design Patterns - Pattern Strategy Exercices Conception Implementation](https://www.youtube.com/watch?v=noO_da60E_4)
  - [**Part 5** - Design Patterns Observer Pattern](https://www.youtube.com/watch?v=jO4v4e4POuw)
  - [**Part 6** - Design Patterns Decorator Pattern](https://www.youtube.com/watch?v=rHmHp7hJG4o)
  - [**Part 7** - Design Patterns -Composite Pattern](https://www.youtube.com/watch?v=8MW48ljuNc8)
  - [**Part 8** - Design Patterns - Adapter Pattern](https://www.youtube.com/watch?v=PX9NPm2P618)
  - [**Part 9** - Design Patterns Proxy](https://www.youtube.com/watch?v=cDSAfBdfcJ4)
  - [**Part 10** - Design Patterns Template Method](https://www.youtube.com/watch?v=JbgfY1j3plc)

### Singleton :

  - [Singleton Pattern](https://www.youtube.com/watch?v=hUE_j6q0LTQ)
  - [POO PHP Singleton - Grafikart](https://www.youtube.com/watch?v=eCL_xXzsxeI)

### Facade :

  - [Facade Pattern](https://www.youtube.com/watch?v=K4FkHVO5iac)
  - [POO PHP Facade - Grafikart](https://www.youtube.com/watch?v=Wvfp3l2Um1s)
### Factory :

  - [Factory Pattern](https://www.youtube.com/watch?v=EcFVTgRHJLM)
  - [POO PHP Factory - Grafikart](https://www.youtube.com/watch?v=xzNd_LXLwc4)

### Abstract Factory :

  - [Abstract Factory Pattern](https://www.youtube.com/watch?v=v-GiuMmsXj4&t=1174s)

### Proxy :

  - [Proxy Pattern](https://www.youtube.com/watch?v=NwaabHqPHeM&t=1502s)

### Builder Pattern :

  - [Builder Pattern](https://www.youtube.com/watch?v=pLoNMD0rqjI)
  - [PHP Antwerp - Laravel Design Patterns by Bobby Bouwmann](https://www.youtube.com/watch?v=UAN4zqiwK5A) (min 16 → min 26)
  - [Design Patterns — A quick guide to Builder pattern. ](https://medium.com/@andreaspoyias/design-patterns-a-quick-guide-to-builder-pattern-a834d7cacead)
(Pas une vidéo mais bon ...)
  - [Design Patterns #2 - The Builder Pattern and the Telescoping...](https://medium.com/@modestofiguereo/design-patterns-2-the-builder-pattern-and-the-telescoping-constructor-anti-pattern-60a33de7522e) (Idem)

### Observer :

  - [Observer Pattern](https://www.youtube.com/watch?v=_BpmfnqjgzQ)
  - [Demo Observer Pattern](https://www.youtube.com/watch?v=DgbrQ6G7UGM)
  
### Adapter :

  - [Adapter Pattern](https://www.youtube.com/watch?v=2PKQtcJjYvc)
  - [POO PHP Adapter - Grafikart](https://www.youtube.com/watch?v=4ru7qqr5j-Q)
  - [Design Patterns: Adapter](https://betterprogramming.pub/design-patterns-adapter-efb73c5090e6)


## A connaitre PAR COEUR ⛑️

### **Les Indispensables**

<details>
  <summary>En Anglais</summary>

  ###
  **1. Singleton**

  The singleton pattern is used to keep creation of a class to only one object. This is useful when precisely one object is needed to coordinate actions across the system. There are several examples of where only a single instance of a class should exist, including caches, thread pools, and registries.

  It’s easy enough to initiate an object of a class — but how do we ensure that only one object ever gets created? The answer is to make the constructor ‘private’ to the class we intend to define as a singleton. That way, only the members of the class can access the private constructor and no one else. Hooray!
  
  ##
  **2. Factory Method**

  Just like a normal factory produces… well, products; a software factory produces objects. And not just that — it does so without specifying the exact class of the object to be created! Neat, right? To accomplish this, objects are created by calling a factory method instead of calling a constructor.

  ##
  **3. Strategy**

  The strategy pattern allows grouping related algorithms under an abstraction, which lets you then switch out one algorithm or policy for another without modifying the client. Instead of directly implementing a single algorithm, the code receives runtime instructions specifying which of the group of algorithms to run. Yay!

  ##
  **4. Observer**

  This pattern is a one-to-many dependency between objects so that when one object changes state, all its dependents are notified. This is typically done by calling one of their methods.

  A subject can have many observers. However, an observer is free to subscribe to updates from other subjects too. Score one for freedom!

  ##
  **5. Builder**

  A builder pattern is used to… build objects. Crazy, right? Sometimes, the objects you need to create are complex, made up of several sub-objects or require an elaborate construction process. The exercise of creating complex types can be simplified by using the builder pattern. A composite or an aggregate object is what a builder generally builds.

  ##
  **6. Adapter**

  This allows incompatible classes to work together by converting the interface of one class into another. Think of it as a sort of translator: when two heads of states who don’t speak a common language meet, usually an interpreter sits between the two and translates the conversation, thus enabling communication.

  ##
  **7. State**

  The state pattern encapsulates the various states a machine can be in, and allows an object to alter its behavior when its internal state changes. The machine can have actions taken on it that move it into different states. Without the use of the pattern, the code becomes inflexible and littered with if-else conditionals.

  ##
  **8. Bridge**

  A physical bridge provides connects two things, right? Well, the bridge pattern describes how to pull apart two software layers fused together in a single class hierarchy and change them into parallel class hierarchies connected by a bridge.

  ##
  **9. Visitor**

  The visitor pattern … *takes deep breath*…. lets you define an operation for a class or a class hierarchy without changing the classes of the elements on which the operation is performed. *inhales*

  ##
  **10. Abstract Factory**

  This is pretty similar to the Factory Builder, except the abstract factory pattern creates families of related products without specifying their class.

</details>

<details>
  <summary>En Français</summary>

  ####
  **1. Singleton**
  
  Le modèle **singleton** est utilisé pour limiter la création d'une classe à un seul objet. Ceci est utile lorsque précisément un objet est nécessaire pour coordonner les actions à travers le système.

  Il existe plusieurs exemples de cas où une seule instance d'une classe doit exister, notamment **des caches**, **des pools de threads** et **des registres**.

  Il est assez facile d'initier un objet d'une classe - mais comment garantir qu'un seul objet sera créé? La réponse est de rendre le constructeur **«privé»** de la classe que nous souhaitons définir comme singleton.

  De cette façon, seuls les membres de la classe peuvent accéder au constructeur privé et personne d'autre. Hourra!

  ##
  **2. Factory Method**

  Tout comme une usine normale produit… enfin, des produits; une fabrique de logiciels produit des objets. Et pas seulement cela - il le fait sans spécifier la classe exacte de l'objet à créer! Neat, non? Pour ce faire, les objets sont créés en appelant une méthode d'usine au lieu d'appeler un constructeur.
  ##
  **3. Strategy**

  Le modèle de **stratégie** permet de regrouper les algorithmes associés sous une abstraction, ce qui vous permet ensuite de désactiver un algorithme ou une stratégie pour un autre sans modifier le client. Au lieu d'implémenter directement un seul algorithme, le code reçoit des instructions d'exécution spécifiant lequel du groupe d'algorithmes exécuter. Yay!

  ##
  **4. Observer**

  Ce modèle est une dépendance **one-to-many** entre les objets de sorte que lorsqu'un objet change d'état, toutes ses dépendances sont notifiées.
  Cela se fait généralement en appelant l'une de leurs méthodes.

  Un sujet peut avoir de nombreux observateurs.
  Cependant, un observateur est également libre de s'abonner aux mises à jour d'autres sujets.

  Marquez un pour la liberté!

  ##
  **5. Builder**

  Un modèle de générateur est utilisé pour… créer des objets. Fou, non? Parfois, les objets que vous devez créer sont complexes, composés de plusieurs sous-objets ou nécessitent un processus de construction élaboré. L'exercice de création de types complexes peut être simplifié en utilisant le modèle de générateur. Un objet composite ou agrégé est ce qu'un constructeur construit généralement.

  ##
  **6. Adapter**

  Cela permet aux classes incompatibles de fonctionner ensemble en convertissant l'interface d'une classe en une autre. Considérez-le comme une sorte de traducteur: lorsque deux chefs d'État qui ne parlent pas une langue commune se rencontrent, généralement un interprète s'assoit entre les deux et traduit la conversation, permettant ainsi la communication.

  ##
  **7. State**

  Le modèle d'état encapsule les différents états dans lesquels une machine peut se trouver et permet à un objet de modifier son comportement lorsque son état interne change. La machine peut subir des actions qui la font passer dans différents états. Sans l'utilisation du modèle, le code devient inflexible et jonché de conditionnelles if-else.

  ##
  **8. Bridge**

  Un pont physique fournit relie deux choses, non? Eh bien, le modèle de pont décrit comment séparer deux couches logicielles fusionnées dans une hiérarchie de classes unique et les transformer en hiérarchies de classes parallèles reliées par un pont.

  ##
  **9. Visitor**

  Le schéma des visiteurs… (*prend une profonde inspiration*…). vous permet de définir une opération pour une classe ou une hiérarchie de classes sans changer les classes des éléments sur lesquels l'opération est effectuée. (*inhale*)

  ##
  **10. Abstract Factory**

  Ceci est assez similaire à **Factory Builder**, sauf que le modèle d'usine abstrait crée des familles de produits connexes sans spécifier leur classe.

</details>
