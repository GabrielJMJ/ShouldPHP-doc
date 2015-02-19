ShouldPHP documentation
=======================

## Index
* [Basic requirements](https://github.com/GabrielJMJ/ShouldPHP-doc#basic-requirements)
* [Instalation](https://github.com/GabrielJMJ/ShouldPHP-doc#instalation)
* [How it works?](https://github.com/GabrielJMJ/ShouldPHP-doc#how-it-works)
 * [Creating an ambient](https://github.com/GabrielJMJ/ShouldPHP-doc#creating-an-ambient)
 * [Creating an assertion](https://github.com/GabrielJMJ/ShouldPHP-doc#creating-an-assertion)
* [Assertions](https://github.com/GabrielJMJ/ShouldPHP-doc#assertions)
 * [Assertions for classes and objects](https://github.com/GabrielJMJ/ShouldPHP-doc#assertions-for-classes-and-objects)
 * [Assertions for methods](https://github.com/GabrielJMJ/ShouldPHP-doc#assertions-for-methods)
 * [Assertions for properties](https://github.com/GabrielJMJ/ShouldPHP-doc#assertions-for-properties)
 * [Assertions for methods parameters](https://github.com/GabrielJMJ/ShouldPHP-doc#assertions-for-methods-parameters)
* [Options](https://github.com/GabrielJMJ/ShouldPHP-doc#options)
 * [Visibility](https://github.com/GabrielJMJ/ShouldPHP-doc#visibility)
 * [Type Hinting](https://github.com/GabrielJMJ/ShouldPHP-doc#type-hinting)
* [Executing tests](https://github.com/GabrielJMJ/ShouldPHP-doc#executing-tests)
 * [should.json](https://github.com/GabrielJMJ/ShouldPHP-doc#shouldjson)
 * [Explaining by the example](https://github.com/GabrielJMJ/ShouldPHP-doc#explaining-by-the-example)
 * [Saving the report logs](https://github.com/GabrielJMJ/ShouldPHP-doc#saving-the-report-logs)
 * [Showing the report with console colors](https://github.com/GabrielJMJ/ShouldPHP-doc#showing-the-report-with-console-colors)

## Basic requirements
To use **ShouldPHP** you must have this requirements:
* PHP >= 5.5

## Instalation
You can install **ShouldPHP** via [Composer](https://getcomposer.org). If you don't know how to use Composer, enter in their [documentation](https://getcomposer.org/doc/) or read this good [intruduction/tutorial](http://code.tutsplus.com/tutorials/easy-package-management-with-composer--net-25530).
After that, put this package in your requirements:
```json
"gabrieljmj/should-php": "1.0.*@dev"
```

## How it works?
The tests are written with a simple syntax, easy to understand, based in "*should*". Basically "*should be*" and "*should have*". You can test classes, objects, methods, methods arguments and properties.

### Creating an ambient
Ambient in **ShouldPHP** are basically test suites. To create a standard ambient you have to instaciate the class ```Gabrieljmj\Should\Ambient\Ambient```. Like that, simply:
```php
use Gabrieljmj\Should\Ambient\Ambient;

$ambient = new Ambient('my_ambient');
```
and have as return in the file the instance:
```php
$ambient->theClass('Foo')->should->be->instance('Bar');
return $ambient;
```
You can also create ambients objects extending ```Gabrieljmj\Should\Ambient\Ambient```. It will provides to you all assertion types methods. Each test from ambient must have the preffix ```test```.
``` php
use Gabrieljmj\Should\Ambient\Ambient;
use MyApp\User;

class UserAmbient extends Ambient
{
    public function testIfTheGetterForNameReturnsTheCorrectValue()
    {
        $name = 'Gabriel';
        $user = new User();
        $user->setName($name);
        
        $this->theMethod($user, 'getName')->should->have->asReturn($name);
    }
}
```

### Creating an assertion
All the assertions types are provided by an ambient. You can see an example here:
```php
$ambient->theClass('Foo')->should->have->theProperty('bar');
```
| Ambient method | Arguments | Description |
| :------------- | :-------- | :---------- |
| ```Ambient::theClass``` | ```$class``` | Provides assertions for classes and objects. |
| ```Ambient::theMethod``` | ```$class, $method``` | Provides assertions for classes methods. |
| ```Ambient::theParameter``` | ```$class, $method, $parameter``` | Provides assertions for methods parameters. |
| ```Ambient::theProperty``` | ```$class, $property``` | Provies assertions for classes/objects properties. |
##Assertions

### Assertions for classes and objects
| Assert | Arguments | Description |
| :----- | :-------- | :---------- |
| *be*.equal | ```object $class[, $message = null]``` | Tests if an object is equal another. |
| *be*.instance | ```$class[, $message = null]``` | Tests if a object is of the a class or has this class as one of its parents. |
| *have*.theProperty | ```$property[, $message = null]``` | Tests if a class has certain property. |
| *have*.theMethod | ```$method[, $message = null]``` | Tests if a class has certain method. |

### Assertions for methods
| Assert | Arguments | Description |
| :----- | :-------- | :---------- |
| *be*.visible | ```$as[, $message = null]``` | Tests if the visibility is the same as the determined. Is recommended to use the constants of ```Gabrieljmj\Should\Options\Visibility```. Check it [here](https://github.com/GabrielJMJ/ShouldPHP/wiki/Documentation#visibility). |
| *have*.argumentsEqual | ```array $args[, $message = null]``` | Tests if the arguments of the method are equal expected. |
| *have*.asReturn | ```$return, array $args[, $message = null]``` | Tests if the return of a method is equal expected. |

### Assertions for properties
| Assert | Arguments | Description |
| :----- | :-------- | :---------- |
| *be*.equal | ```$value[, $message = null]``` | Tests if a class has a property with a certain value. If the property is not public, the default value will be used. |
| *be*.visible | ```$as[, $message = null]``` | Tests if the visibility is the same as the determined. Is recommended to use the constants of ```Gabrieljmj\Should\Options\Visibility```. Check it [here](https://github.com/GabrielJMJ/ShouldPHP/wiki/Documentation#visibility). |

### Assertions for methods parameters
| Assert | Arguments | Description |
| :----- | :-------- | :---------- |
| *have*.acceptOnly | ```$type[, $message = null]``` | Tests if certain parameter accept determined value type. Recommended to use the contants of ```Gabrieljmj\Should\Options\TypeHinting```. Check it [here](https://github.com/GabrielJMJ/ShouldPHP/wiki/Documentation#type-hinting) |
| *have*.asDefaultValue | ```$value[, $message = null]``` | Tests if certain parameter of a method has the default value equals determined one. |

## Options

### Visibility
| Constant | What means? |
| :------- | :---------- |
| ```Visibility::AS_PUBLIC``` | Public visibility |
| ```Visibility::AS_PROTECTED``` | Protected visibility |
| ```Visibility::AS_PRIVATE``` | Private visibility |

### Type Hinting
| Constant | What means? |
| :------- | :---------- |
| ```TypeHinting::ARR``` | Array type |
| ```TypeHinting::CALL``` | Callable type |
| ```TypeHinting::VARIADIC``` | Variadic type |
| ```TypeHinting::INSTANCE_OF``` | Instance of some class or interface determined by the static method ```TypeHinting::anInstanceOf($class)```. |

## Executing tests

The execetion of all tests are made with a console command. After executing, in the console will appear a little report. If some test fail, the report will explain why.
```
php vendor/bin/should excute test.php
```
<div style="text-align: center;"><img src="http://i.imgur.com/1n9zBaP.png"/></div>
*Yes, I use Windows. Judge me.*

#### should.json
The ```should.json``` is a collection of tests, where you can indicate what tests should be executed. The file, in the truth, may have any name, but have to be JSON and to have ```ambients``` index.
```json
{
    "ambients": [
        "test.php",
        "Test\\UserAmbient",
        "tests/"
    ]
}
```

#### Rules
You can define rules for the execution tests like just test files from a directory with certain suffix or preffix. To it, indicate the rules on JSON file.
```json
"rules": {
    "directory": {
        "suffix": [
            "Test.php"
        ]
    }
}
```

#### Rules list

| Rule | Category | What means? |
| :--- | :------- | :---------- |
| Suffix | Directory | Execute all ambient files with determined suffix in the name. |
| Preffix | Directory | Execute all ambient files with determined preffix in the name. |

**Console:**
```console
php vendor/bin/should execute should.json
```

#### Explaining by the example
| Local | Description |
| :---- | :---------- |
| ```test.php``` | Executes a file that return an instance of an ambient. |
| ```Test\\UserAmbient``` | Executes all test methods from an ambient custom object. In the console you must to use ```/``` instead ```\```. Like that: ```php vendor/bin/should excute Test/Ambient```. |
| ```tests/``` | Executes all ambient files of a directory. You must to put ```/``` in the end of the directory name both console and JSON. |

### Saving the report logs
To save the report logs, add the option ```-s|--save```to the execution follow by the logs file:
```console
php vendor/bin/should execute should.json -s "tests.log"
``` 
### Showing the report with console colors
Add the option ```-c|--colors```:
```console
php vendor/bin/should execute should.json -c
``` 
