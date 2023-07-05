## Single Responsibility Principle

Tek Sorumluluk Prensibi (SRP), bir sınıfın veya modülün yalnızca bir değişiklik nedenine sahip olması gerektiğini ifade eden bir yazılım tasarım prensibidir. Daha basit bir ifadeyle, her sınıfın yalnızca bir sorumluluğu veya görevi olmalı ve birden fazla ilişkisiz görevle uğraşmamalıdır.

SRP'yi uygulamadan önce, bir örnek üzerinde düşünelim. Diyelim ki bir maaş bordrosu sisteminde Employee adında bir sınıfımız var. Bu sınıf, çalışan bilgilerini depolamak, maaşlarını hesaplamak ve bordro oluşturmakla ilgilenmektedir. İşte sınıfın yaklaşık olarak nasıl görünebileceği:

```swift 

class Employee {
    var name: String
    var id: String
    var salary: Double
    
    init(name: String, id: String, salary: Double) {
        self.name = name
        self.id = id
        self.salary = salary
    }
    
    func calculateSalary() {
        // Calculate salary logic
    }
    
    func generatePayslip() {
        // Generate payslip logic
    }
    
    // Other methods related to employee management
}

```
Bu örnekte, Employee sınıfı SRP'yi ihlal ediyor çünkü birden fazla sorumluluğa sahip. Sınıf, sadece çalışan bilgilerini depolamakla kalmıyor, aynı zamanda maaş hesaplamalarını yapmak ve bordro oluşturmakla da ilgileniyor. Bu durum, sınıfın gelecekte bakımını ve değişikliklerini zorlaştırabilir. Maaş hesaplama mantığı veya bordro oluşturma gibi konularda değişiklik yapılması gerektiğinde Employee sınıfını değiştirmemiz gerekecektir.

SRP'ye uymak için sorumlulukları farklı sınıflara ayırmamız gerekmektedir. İşte SRP'nin uygulandığı bir kod örneği:

```swift 

class Employee {
    var name: String
    var id: String
    
    init(name: String, id: String) {
        self.name = name
        self.id = id
    }
}

class SalaryCalculator {
    func calculateSalary(employee: Employee) -> Double {
        // Calculate salary logic
    }
}

class PayslipGenerator {
    func generatePayslip(employee: Employee) {
        // Generate payslip logic
    }
}

```

Güncellenen kodda, Employee sınıfı artık sadece çalışan bilgilerini depolama sorumluluğunu üstlenmektedir. SalaryCalculator sınıfı maaş hesaplamasından, PayslipGenerator sınıfı ise bordro oluşturmaktan sorumludur. Her bir sınıfın tek bir sorumluluğu vardır ve diğerlerini etkilemeden bağımsız olarak değiştirilebilir.

Sorumlulukları ayırarak daha iyi bir kod organizasyonu, bakım kolaylığı ve esneklik elde ederiz. Maaş hesaplama veya bordro oluşturma mantığında değişiklik yapılması gerektiğinde, ilgili sınıfları değiştirebiliriz ve Employee sınıfını etkilemeden kalabiliriz. Bu modüler yaklaşım, kodun uzun vadede daha kolay anlaşılmasını, test edilmesini ve bakımını sağlar. Bu da Tek Sorumluluk Prensibi'nin temelidir.

