
[TOC]

# [Linkedin](https://github.com/linkedin/swift-style-guide)

## 1. 代码格式

### **1.1** tab设置为4个空格

### **1.3** 避免出现单行超过160字符的情况`Xcode->Preferences->Text Editing->Page guide at column: 160 is helpful for this`

### **1.4** 文件结束的末尾要留有空行

### **1.5** 确保不在任何地方出现尾随的空格`Xcode->Preferences->Text Editing->Automatically trim trailing whitespace + Including whitespace-only lines`

### **1.6** 括号的开头不起新行

```swift
// specifying type
let pirateViewController: PirateViewController

// dictionary syntax (note that we left-align as opposed to aligning colons)
let ninjaDictionary: [String: AnyObject] = [
    "fightLikeDairyFarmer": false,
    "disgusting": true
]

// declaring a function
func myFunction<T, U: SomeProtocol>(firstArgument: U, secondArgument: T) where T.RelatedType == U {
    /* ... */
}

// calling a function
someFunction(someArgument: "Kitten")

// superclasses
class PirateViewController: UIViewController {
    /* ... */
}

// protocols
extension PirateViewController: UITableViewDataSource {
    /* ... */
}
```

### **1.7** 冒号前无空格，冒号后有且仅有一个空格

### **1.8** 逗号后跟随一个空格

### **1.9** 操作符前后均有一个空格，`(`和`)`内部不需空格

### **1.10** 调用函数如果参数有多个，尽量将每个参数放在单独一行

```swift
someFunctionWithManyArguments(
    firstArgument: "Hello, I am a string",
    secondArgument: resultFromSomeFunction(),
    thirdArgument: someOtherLocalProperty)
```

### **1.11** 在使用元素较多的数组或者字典时，`[`和`]`处理方式和代码块的处理方式相同比如`if`语句

```swift
someFunctionWithABunchOfArguments(
    someStringArgument: "hello I am a string",
    someArrayArgument: [
        "dadada daaaa daaaa dadada daaaa daaaa dadada daaaa daaaa",
        "string one is crazy - what is it thinking?"
    ],
    someDictionaryArgument: [
        "dictionary key 1": "some value 1, but also some more text here",
        "dictionary key 2": "some value 2"
    ],
    someClosure: { parameter1 in
        print(parameter1)
    })
```

### **1.12** 使用局部常量来避免判断语句过长

```swift
// PREFERRED
let firstCondition = x == firstReallyReallyLongPredicateFunction()
let secondCondition = y == secondReallyReallyLongPredicateFunction()
let thirdCondition = z == thirdReallyReallyLongPredicateFunction()
if firstCondition && secondCondition && thirdCondition {
    // do something
}

// NOT PREFERRED
if x == firstReallyReallyLongPredicateFunction()
    && y == secondReallyReallyLongPredicateFunction()
    && z == thirdReallyReallyLongPredicateFunction() {
    // do something
}
```


## 2. 命名方式

### **2.1**  ~~不再需要类似OC的前缀命名~~

### **2.2**  大写驼峰法来命名类型（`struct`,`enum`, `class`, `typedef`, `associatedtype`, etc）

### **2.3**  小写驼峰法来命名`函数`,`方法`，`属性`，`变/常量`等

### **2.4**  对于缩略词（e.g. `HTML`, `HTTP`, `URL`, `ID`），如果在开头则依据大小驼峰法全部使用大写(`类型等/2.2`)或者小写(`函数等/2.3`)，而不在开头的则全部需要用大写

```swift
// "HTML" is at the start of a constant name, so we use lowercase "html"
let htmlBodyContent: String = "<p>Hello, World!</p>"
// Prefer using ID to Id
let profileID: Int = 1
// Prefer URLFinder to UrlFinder
class URLFinder {
    /* ... */
}
```

### **2.5**  和实例无关的常量需要使用`static`关键字标示，同时所有`static`标记的常量都应该放在同一个区域并用`MARK`标识

```swift
// PREFERRED    
class MyClassName {
    // MARK: - Constants
    static let buttonPadding: CGFloat = 20.0
    static let indianaPi = 3
    static let shared = MyClassName()
}

// NOT PREFERRED
class MyClassName {
    // Don't use `k`-prefix
    static let kButtonPadding: CGFloat = 20.0

    // Don't namespace constants
    enum Constant {
        static let indianaPi = 3
    }
}
```

### **2.6**  名称应该是具有描述性且无歧义的

### **2.7**  不使用缩写词，或者单字母的名称

```swift
// PREFERRED
class RoundAnimatingButton: UIButton {
    let animationDuration: NSTimeInterval

    func startAnimating() {
        let firstSubview = subviews.first
    }

}

// NOT PREFERRED
class RoundAnimating: UIButton {
    let aniDur: NSTimeInterval

    func srtAnmating() {
        let v = subviews.first
    }
}
```

### **2.8**  如果常量/变量名称的含义不明显，可以把类型信息包含进去

```swift
// PREFERRED
class ConnectionTableViewCell: UITableViewCell {
    let personImageView: UIImageView

    let animationDuration: TimeInterval

    // it is ok not to include string in the ivar name here because it's obvious
    // that it's a string from the property name
    let firstName: String

    // though not preferred, it is OK to use `Controller` instead of `ViewController`
    let popupController: UIViewController
    let popupViewController: UIViewController

    // when working with a subclass of `UIViewController` such as a table view
    // controller, collection view controller, split view controller, etc.,
    // fully indicate the type in the name.
    let popupTableViewController: UITableViewController

    // when working with outlets, make sure to specify the outlet type in the
    // property name.
    @IBOutlet weak var submitButton: UIButton!
    @IBOutlet weak var emailTextField: UITextField!
    @IBOutlet weak var nameLabel: UILabel!

}

// NOT PREFERRED
class ConnectionTableViewCell: UITableViewCell {
    // this isn't a `UIImage`, so shouldn't be called image
    // use personImageView instead
    let personImage: UIImageView

    // this isn't a `String`, so it should be `textLabel`
    let text: UILabel

    // `animation` is not clearly a time interval
    // use `animationDuration` or `animationTimeInterval` instead
    let animation: TimeInterval

    // this is not obviously a `String`
    // use `transitionText` or `transitionString` instead
    let transition: String

    // this is a view controller - not a view
    let popupView: UIViewController

    // as mentioned previously, we don't want to use abbreviations, so don't use
    // `VC` instead of `ViewController`
    let popupVC: UIViewController

    // even though this is still technically a `UIViewController`, this property
    // should indicate that we are working with a *Table* View Controller
    let popupViewController: UITableViewController

    // for the sake of consistency, we should put the type name at the end of the
    // property name and not at the start
    @IBOutlet weak var btnSubmit: UIButton!
    @IBOutlet weak var buttonSubmit: UIButton!

    // we should always have a type in the property name when dealing with outlets
    // for example, here, we should have `firstNameLabel` instead
    @IBOutlet weak var firstName: UILabel!
}
```

### **2.9** 在为函数的参数命名时，确保每个参数都容易理解

### **2.10**  协议的命名：如果表示正在发生的事情使用名词命名；如果表示某种能力使用`able`,`ible`,`ing`;如果以上两个规则都不符合那就直接加上`Protocol`

```swift
// here, the name is a noun that describes what the protocol does
protocol TableViewSectionProvider {
    func rowHeight(at row: Int) -> CGFloat
    var numberOfRows: Int { get }
    /* ... */
}

// here, the protocol is a capability, and we name it appropriately
protocol Loggable {
    func logCurrentState()
    /* ... */
}

// suppose we have an `InputTextView` class, but we also want a protocol
// to generalize some of the functionality - it might be appropriate to
// use the `Protocol` suffix here
protocol InputTextViewProtocol {
    func sendTrackingEvent()
    func inputText() -> String
    /* ... */
}
```
    
## 3. 代码风格

### **3.1** 通用

#### **3.1.1** 能用`let`不用 `var`

#### **3.1.2** 集合间的转换更推荐使用 `map`，`filter`, `reduce` 而不是遍历

```swift
// PREFERRED
let stringOfInts = [1, 2, 3].flatMap { String($0) }
// ["1", "2", "3"]

// NOT PREFERRED
var stringOfInts: [String] = []
for integer in [1, 2, 3] {
    stringOfInts.append(String(integer))
}

// PREFERRED
let evenNumbers = [4, 8, 15, 16, 23, 42].filter { $0 % 2 == 0 }
// [4, 8, 16, 42]

// NOT PREFERRED
var evenNumbers: [Int] = []
for integer in [4, 8, 15, 16, 23, 42] {
    if integer % 2 == 0 {
        evenNumbers.append(integer)
    }
}
```

#### **3.1.3** 常量/变量 如果可以推断出其类型，在声明时就不必指定类型

#### **3.1.4** 如果一个函数有多个返回值，推荐使用有标签表明的元组；如果一个元组使用超过了1次考虑使用`typealias`;如果元组中的元素超过了3个，请使用`struct`或者`class`

```swift
func pirateName() -> (firstName: String, lastName: String) {
    return ("Guybrush", "Threepwood")
}

let name = pirateName()
let firstName = name.firstName
let lastName = name.lastName
```

#### **3.1.5** 使用delegate和protocols要警惕循环引用，我们明确规定声明这些属性的时候应使用`weak`关键字

#### **3.1.6** 在逃逸闭包中直接使用self的时候要小心，使用`[weak self]`或者`guard let strongSelf = self else { return }`

```swift
myFunctionWithEscapingClosure() { [weak self] (error) -> Void in
    // you can do this

    self?.doSomething()

    // or you can do this

    guard let strongSelf = self else {
        return
    }

    strongSelf.doSomething()
}
```

#### **3.1.7** 控制流的判断条件不需要加括号

```swift
// PREFERRED
if x == y {
    /* ... */
}

// NOT PREFERRED
if (x == y) {
    /* ... */
}
```

#### **3.1.8** 避免写`enum`的类型，而是直接用case

```swift
// PREFERRED
imageView.setImageWithURL(url, type: .person)

// NOT PREFERRED
imageView.setImageWithURL(url, type: AsyncImageView.Type.person)
```

#### **3.1.9** 类方法禁止使用缩略，因为这样会和`enum`难以区分

```swift
// PREFERRED
imageView.backgroundColor = UIColor.white

// NOT PREFERRED
imageView.backgroundColor = .white
```

#### **3.1.10** 非必须情况下不要使用`self.`

#### **3.1.11** 时刻注意，如果一个方法不允许被重载，要使用`final`(可以提升编译时间)

#### **3.1.12** `else`,`catch`这类的控制流语句关键字不必新起一行

```swift
if someBoolean {
    // do something
} else {
    // do something else
}

do {
    let fileContents = try readFile("filename.txt")
} catch {
    print(error)
}
```

#### **3.1.13** 声明类方法的时候推荐使用`static`关键字，而不是`class`

#### **3.1.14** 如果一些方法没有入参，没有一些其他作用而仅仅是返回一个对象或者值，那就应该使用计算属性替代它


### **3.2** 访问修饰符


#### **3.2.1** 访问修饰符应在所有修饰符之前

```swift
// PREFERRED
private static let myPrivateNumber: Int

// NOT PREFERRED
static private let myPrivateNumber: Int
```

#### **3.2.2** 所有的权限修饰符应该与其修饰的内容在同一行

```
// PREFERRED
open class Pirate {
    /* ... */
}

// NOT PREFERRED
open
class Pirate {
    /* ... */
}
```

#### **3.2.3** 不要写`internal`修饰符，这是默认的

#### **3.2.4** 如果单元测试中需要使用某个属性，那么它应该被声明成`internal`,并且通过`@testable import ModuleName`方式引入

```swift
/**
 This property defines the pirate's name.
 - warning: Not `private` for `@testable`.
 */
let pirateName = "LeChuck"
```

#### **3.2.5** `private`要比`filePrivate`更好

#### **3.2.6** `open` 要比 `public`更好

### **3.3**自定义操作符

#### **3.3.1** 能使用一个函数就不要使用自定义操作符

### **3.4** `switch` 语句和 `enum`s

#### **3.4.1** 在swift选择语句中，如果选项是有限个，就不要使用`default`, 而应该把用不到的case放在底部并用`break`关键字防止被执行

#### **3.4.2** 由于Swift中的 `switch case`会默认返回，所以除非必要，不必显式声明`break`

#### **3.4.3** `case`语句要和`switch`语句对齐

#### **3.4.4** 如果一个case有关联值，确保使用枚举值而不是直接使用关联值

```swift
enum Problem {
    case attitude
    case hair
    case hunger(hungerLevel: Int)
}

func handleProblem(problem: Problem) {
    switch problem {
    case .attitude:
        print("At least I don't have a hair problem.")
    case .hair:
        print("Your barber didn't know when to stop.")
    case .hunger(let hungerLevel):
        print("The hunger level is \(hungerLevel).")
    }
}
```

#### **3.4.5** 推荐使用case列表（e.g. `case 1, 2, 3:`），而不是使用`fallthrough`关键字

#### **3.4.6** 如果default情况不能使用，那么应该抛出一个error或者assert

```swift
func handleDigit(_ digit: Int) throws {
    switch digit {
    case 0, 1, 2, 3, 4, 5, 6, 7, 8, 9:
        print("Yes, \(digit) is a digit!")
    default:
        throw Error(message: "The given number was not a digit.")
    }
}
```

### **3.5** 可选值

#### **3.5.1** 隐式解包（`implicitly unwrapped optionals`）的唯一场景式在使用`@IBOUtlet`时候。**尽量避免使用强制解包**

#### **3.5.3** 不要使用`as!`或`try!`

#### **3.5.4** 对可选值判空操作直接使用`!= nil`

```swift
// PREFERERED
if someOptional != nil {
    // do something
}

// NOT PREFERRED
if let _ = someOptional {
    // do something
}
```


#### **3.5.5** 不要使用`unowned`,可以认为`unowend`是对`weak`的隐式解包，要避免隐式解包的情况出现

#### **3.5.6** 对一个可选值解包的时，使用相同的名称来进行解包操作

```swift
guard let myValue = myValue else {
    return
}
```

### **3.6**  协议

#### **3.6.1** 在实现协议时候，有两种方式(`MARK`和`extension`)来组织代码

    1. 用`//MARK:`来分割协议的实现和其他部分

    2. 在同一个文件中使用类或者结构体的扩展来实现协议

#### **3.6.3** 使用扩展的时候要注意，扩展中的方法不能被子类重载，可能会对测试带来一些麻烦

### **3.7** 属性

#### **3.7.1** 对于一个`read-only`的计算属性，需要提供一个getter方法，且不需要`get{}`包裹

```swift
var computedProperty: String {
    if someBool {
        return "I'm a mighty pirate!"
    }
    return "I'm selling these fine leather jackets."
}
```

#### **3.7.2**  `get{}`,`set{}`, `willSet{}`, `didSet{}`方法使用时要带上缩进

#### **3.7.3**  尽管你可以对`set`/`willSet`/`didSet`方法自定义名称，但推荐使用标准的`newValue`和`oldValue`

```swift
var storedProperty: String = "I'm selling these fine leather jackets." {
    willSet {
        print("will set to \(newValue)")
    }
    didSet {
        print("did set from \(oldValue) to \(storedProperty)")
    }
}

var computedProperty: String  {
    get {
        if someBool {
            return "I'm a mighty pirate!"
        }
        return storedProperty
    }
    set {
        storedProperty = newValue
    }
}
```

#### **3.7.4**  声明一个单例可以采用以下的方式

```
class PirateManager {
    static let shared = PirateManager()

    /* ... */
}
```

### **3.8** 闭包

#### **3.8.1**  如果闭包的参数是显而易见的，类型名称可写可不写

#### **3.8.2** 闭包的参数和大括号应在同一行

#### **3.8.3** 如果没有参数的话闭包的含义不明显，那就不要使用尾随闭包

### **3.9** 数组

#### **3.9.1** 尽量避免使用下标访问数组，可以使用`.first`或者`.last`访存器来避免crash。尽可能使用 `for in`而不是`for i in 0 ..< items.count`。如果确实要使用下标访问要对数组边界情况有判定。推荐使用`for (index, value) in items.enumerated()`来遍历数组

#### **3.9.2** 不要使用`+=`和`+`来追加/拼接数组，而应该使用`.append()`和`.append(contentsOf:)`

### **3.10** 错误处理

### **3.11** 使用`guard`

#### **3.11.1** 我们采用及时返回的策略来处理if语句，使用guard语句可以达到这个目的

```swift
// PREFERRED
func eatDoughnut(at index: Int) {
    guard index >= 0 && index < doughnuts.count else {
        // return early because the index is out of bounds
        return
    }

    let doughnut = doughnuts[index]
    eat(doughnut)
}

// NOT PREFERRED
func eatDoughnut(at index: Int) {
    if index >= 0 && index < doughnuts.count {
        let doughnut = doughnuts[index]
        eat(doughnut)
    }
}
```

#### **3.11.2**  使用`gaurd`而不是`if`来降低代码的嵌套层次

```swift
// PREFERRED
guard let monkeyIsland = monkeyIsland else {
    return
}
bookVacation(on: monkeyIsland)
bragAboutVacation(at: monkeyIsland)

// NOT PREFERRED
if let monkeyIsland = monkeyIsland {
    bookVacation(on: monkeyIsland)
    bragAboutVacation(at: monkeyIsland)
}

// EVEN LESS PREFERRED
if monkeyIsland == nil {
    return
}
bookVacation(on: monkeyIsland!)
bragAboutVacation(at: monkeyIsland!)
```

#### **3.11.3**  `guard`和`if`在功能上是等效的，何时使用取决哪个更能提高代码可读性，如果不知道用哪个，那就用`guard`

#### **3.11.4**  在两个状态中选择时，使用if更合理

#### **3.11.5**  有时可能需要对多个可选值解包，推荐做法是对多个可选值分别使用`gurad`,以此来单独处理各个情况

```swift
// combined because we just return
guard let thingOne = thingOne,
    let thingTwo = thingTwo,
    let thingThree = thingThree else {
    return
}

// separate statements because we handle a specific error in each case
guard let thingOne = thingOne else {
    throw Error(message: "Unwrapping thingOne failed.")
}

guard let thingTwo = thingTwo else {
    throw Error(message: "Unwrapping thingTwo failed.")
}

guard let thingThree = thingThree else {
    throw Error(message: "Unwrapping thingThree failed.")
}
```

#### **3.11.6**  禁止将`guard`语句写在一行以内

```swift
// PREFERRED
guard let thingOne = thingOne else {
    return
}

// NOT PREFERRED
guard let thingOne = thingOne else { return }
```

## 4. 文档/注释

### **4.1** 文档

#### **4.1.1** 在每个类的头部标明这个类的用途

#### **4.1.2** 对复杂度超过O(1)的函数注释，使用`opt+cmd+/`

### **4.2** 注释规则

#### **4.2.1** 注释符`//` 之后要留有一个空格

#### **4.2.2** 使用`// MARK: `时，下面空一行
