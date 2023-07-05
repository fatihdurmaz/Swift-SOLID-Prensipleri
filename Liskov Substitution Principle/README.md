## Liskov Substitution Principle

Liskov Yerine Geçme Prensibi (LSP), nesne tabanlı programlamada temel bir prensiptir ve bir üst sınıfa ait nesnelerin, onun alt sınıflarıyla değiştirilebilmesi durumunda programın doğruluğunu etkilemeden çalışması gerektiğini ifade eder. Daha basit bir ifadeyle, bir temel sınıf beklediğimiz herhangi bir yerde türetilmiş bir sınıfı kullanabilmeliyiz ve her şey doğru çalışmalıdır.

LSP'yi daha iyi anlamak için bir örnek üzerinde düşünelim. CalculateArea adında bir yöntem içeren Shape adında bir üst sınıfımız olduğunu varsayalım. Ayrıca Rectangle ve Square adında iki alt sınıfımız var. Rectangle sınıfı uzunluk ve genişliğe sahipken, Square sınıfı sadece bir kenar uzunluğuna sahiptir. İşte LSP'yi uygulamadan bu sınıfların nasıl görünebileceği bir örnek:

```swift 
class Shape {
    // Method to calculate area
    func calculateArea() -> Double {
        fatalError("Must be overridden")
    }
}

class Rectangle: Shape {
    var length: Double
    var width: Double
    
    init(length: Double, width: Double) {
        self.length = length
        self.width = width
    }
    
    override func calculateArea() -> Double {
        return length * width
    }
}

class Square: Shape {
    var sideLength: Double
    
    init(sideLength: Double) {
        self.sideLength = sideLength
    }
    
    override func calculateArea() -> Double {
        return sideLength * sideLength
    }
}
```
Şimdi, Shape'in bir örneğini bekleyen ve calculateArea yöntemini çağıran bir işlevimiz olduğunu varsayalım:

```swift 
func printArea(shape: Shape) {
    let area = shape.calculateArea()
    print("Area: \(area)")
}
```

Bu kod, printArea işlevine Square nesnesini geçirmeye çalıştığımızda sorun çıkar:

```swift 
let rectangle = Rectangle(length: 5, width: 3)
printArea(shape: rectangle) // Output: Area: 15

let square = Square(sideLength: 4)
printArea(shape: square) // Output: Area: 16
```

Bu durumda, çıktı doğru olsa da Square nesnesi, Shape üst sınıfının beklenen davranışına tam olarak uymamaktadır. Liskov Substitution Prensibi, alt sınıfların üst sınıfın yerine geçebilmesi gerektiğini ve herhangi bir soruna yol açmaması gerektiğini belirtir.

Bunu düzeltmek için kodu LSP'ye uygun şekilde yeniden düzenleyebiliriz. Bir olası çözüm, kalıtım yerine bileşimi kullanmaktır:

```swift 
protocol Shape {
    // Method to calculate area
    func calculateArea() -> Double
}

struct Rectangle: Shape {
    var length: Double
    var width: Double
    
    func calculateArea() -> Double {
        return length * width
    }
}

struct Square: Shape {
    var sideLength: Double
    
    func calculateArea() -> Double {
        return sideLength * sideLength
    }
}
```
Şimdi, Shape protokolü alanın hesaplanması için bir sözleşme tanımlar ve Rectangle ve Square protokolü uygular. Buna göre printArea fonksiyonunu düzenleyebiliriz:

```swift 
func printArea(shape: Shape) {
    let area = shape.calculateArea()
    print("Area: \(area)")
}
``` 

Bu yeniden düzenlenmiş kod ile, Rectangle ve Square nesnelerini güvenli bir şekilde printArea fonksiyonuna geçirebiliriz ve bu şekilde Liskov Substitution Prensibini karşılamış oluruz:

```swift 
let rectangle = Rectangle(length: 5, width: 3)
printArea(shape: rectangle) // Output: Area: 15

let square = Square(sideLength: 4)
printArea(shape: square) // Output: Area: 16
```
Şimdi, kod Liskov Substitution Prensibine uyar, çünkü üst sınıfı (Shape) alt sınıfları (Rectangle ve Square) ile sorunsuz bir şekilde değiştirebiliriz.
