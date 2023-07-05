
## Open/Closed Principle 

Açık/Kapalı Prensibi, yazılım varlıklarının (sınıflar, modüller, fonksiyonlar vb.) genişletmeye açık, değişikliğe kapalı olması gerektiğini belirten bir tasarım prensibidir. Bu, mevcut kodunu değiştirmeden bir sınıfa yeni işlevsellik veya davranış ekleyebilmeniz gerektiği anlamına gelir.

Açık/Kapalı Prensibi'ni uygulamadan önce, bir örnek üzerinde düşünelim. İlk olarak, calculateArea() yöntemine sahip bir Shape sınıfımız olduğunu varsayalım. Başlangıçta, sadece bir dikdörtgenin alanını hesaplamayı desteklemektedir:

```swift
class Shape {
    func calculateArea(length: Double, width: Double) -> Double {
        return length * width
    }
}
```

Şimdi, bir dairenin alanını hesaplamayı desteklemek istediğimizi varsayalım. Açık/Kapalı Prensibi'ni takip etmeden, mevcut Shape sınıfını değiştirerek ve yeni bir calculateArea(radius: Double) yöntemi ekleyerek bu işlevselliği eklemeye yönelebiliriz:

```swift
class Shape {
    func calculateArea(length: Double, width: Double) -> Double {
        return length * width
    }
    
    func calculateArea(radius: Double) -> Double {
        return 3.14 * radius * radius
    }
}
```
Bu yaklaşımın sorunu, mevcut sınıfı değiştirmemizdir, bu da hatalara yol açabilir ve Shape sınıfına bağımlı olan mevcut kodu etkileyebilir.

Açık/Kapalı Prensibi'ni uyguladıktan sonra:
Açık/Kapalı Prensibi'ne uymak için, Shape adında soyut bir temel sınıf veya protokol oluşturabilir ve ardından belirli şekilleri uygulayan somut sınıfları tanımlayabiliriz. İşte bir örnek:

```swift
protocol Shape {
    func calculateArea() -> Double
}

class Rectangle: Shape {
    let length: Double
    let width: Double
    
    init(length: Double, width: Double) {
        self.length = length
        self.width = width
    }
    
    func calculateArea() -> Double {
        return length * width
    }
}

class Circle: Shape {
    let radius: Double
    
    init(radius: Double) {
        self.radius = radius
    }
    
    func calculateArea() -> Double {
        return 3.14 * radius * radius
    }
}
```
Bu yaklaşımda, Shape protokolü tüm şekillerin ortak davranışını tanımlar ve her bir somut sınıf (örneğin, Rectangle ve Circle) calculateArea() yöntemini kendi şekillerinin mantığına göre uygular. Yeni bir şekil için destek eklememiz gerektiğinde, mevcut herhangi bir kodu değiştirmeden Shape protokolünü uygulayan yeni bir sınıf oluşturabiliriz.

Açık/Kapalı Prensibi'ni takip ederek, mevcut kodu değiştirmeden yazılımımızı kolayca yeni işlevlerle genişletebiliriz. Bu şekilde hata riskini ve mevcut kodu bozma riskini en aza indirebiliriz.
