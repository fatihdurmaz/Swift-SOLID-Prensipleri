##  Interface Segregation Principle

Arayüz Ayırma Prensibi (ISP), büyük, monolitik arayüzleri daha küçük, daha özelleşmiş arayüzler haline getirme önerisinde bulunan bir tasarım prensibidir. Prensip, istemcilerin kullanmadıkları arayüzlere bağımlı olmamaları gerektiğini vurgular. Basit bir ifadeyle, her bir istemcinin ihtiyaçlarına uygun odaklanmış ve belirli arayüzlerin oluşturulmasını teşvik eder.

ISP'yi uygulamadan önce, çok sayıda yönteme sahip bir Printer protokolüne sahip bir örneği düşünelim:

```swift
protocol Printer {
    func printDocument()
    func scanDocument()
    func faxDocument()
    func copyDocument()
}

class OfficePrinter: Printer {
    func printDocument() {
        // Implementation
    }
    
    func scanDocument() {
        // Implementation
    }
    
    func faxDocument() {
        // Implementation
    }
    
    func copyDocument() {
        // Implementation
    }
}

class HomePrinter: Printer {
    func printDocument() {
        // Implementation
    }
    
    func scanDocument() {
        // Implementation
    }
    
    func faxDocument() {
        // Implementation
    }
    
    func copyDocument() {
        // Implementation
    }
}
```

Bu durumda, OfficePrinter ve HomePrinter, yazdırma, tarama, faks çekme ve kopyalama gibi yöntemleri içeren aynı Printer protokolünü uygular. Ancak pratikte, bir ev yazıcısının faks çekme veya kopyalama yeteneği olmayabilir. Tüm Printer protokolünü uygulayarak, ev yazıcısını bu yöntemler için boş veya ilgisiz uygulamalar sunmaya zorlarız.

ISP'yi uyguladıktan sonra, arayüzleri daha özelleştirilmiş hale getiririz:

```swift
protocol Printable {
    func printDocument()
}

protocol Scanable {
    func scanDocument()
}

protocol Faxable {
    func faxDocument()
}

protocol Copyable {
    func copyDocument()
}

class OfficePrinter: Printable, Scanable, Faxable, Copyable {
    func printDocument() {
        // Implementation
    }
    
    func scanDocument() {
        // Implementation
    }
    
    func faxDocument() {
        // Implementation
    }
    
    func copyDocument() {
        // Implementation
    }
}

class HomePrinter: Printable, Scanable {
    func printDocument() {
        // Implementation
    }
    
    func scanDocument() {
        // Implementation
    }
}
```

ISP'yi uygulayarak, işlevleri ayrı protokollere ayırdık: Printable, Scanable, Faxable ve Copyable. Şimdi, OfficePrinter ve HomePrinter yalnızca ihtiyaç duydukları protokolleri uygulayabilir. HomePrinter sınıfının gereksiz Faxable ve Copyable protokollerini uygulamasına gerek kalmaz.

Bu ayrıma sayesinde, her sınıf belirli sorumluluklarına odaklanabilir ve daha temiz ve sürdürülebilir bir kod elde edilir. Ayrıca, istemcilerin kullanmadıkları yöntemlere bağımlı olmasını engeller, hataların ve gereksiz bağlantıların oluşma olasılığını azaltır.
