## Dependency Inversion Principle

Bağımlılık Tersine Çevirme Prensibi (DIP), yüksek seviye modüllerin/sınıfların düşük seviye modüllere/sınıflara doğrudan bağımlı olmamasını öneren bir yazılım tasarım prensibidir. Bunun yerine, yüksek seviye modüller/sınıflar soyutlamalara (arayüzler veya protokoller) bağımlı olmalıdır ve düşük seviye modüller/sınıflar bu soyutlamaları uygulamalıdır.

Bağımlılık Tersine Çevirme Prensibi'ni uygulamadan önce, yüksek seviye modül düşük seviye modüle doğrudan bağımlıdır. Bu, düşük seviye modülde yapılacak herhangi bir değişikliğin yüksek seviye modülü etkileyeceği ve sıkıca bağlı bir sistem oluşacağı anlamına gelir. Ödeme sistemi bir örnek alalım:

DIP'nden Önce:

```swift
class PaymentProcessor {
    private let paymentGateway: PaymentGateway

    init() {
        paymentGateway = PaymentGateway()
    }

    func processPayment(amount: Double) {
        // Process the payment using the payment gateway
        paymentGateway.processPayment(amount)
    }
}

class PaymentGateway {
    func processPayment(amount: Double) {
        // Actual implementation of processing the payment
    }
}
```

Yukarıdaki örnekte, PaymentProcessor doğrudan PaymentGateway'in somut uygulamasına bağımlıdır. Ödeme ağ geçidini değiştirmek veya başka bir ödeme ağ geçidi eklemek istediğimizde, PaymentProcessor sınıfını değiştirmemiz gerekecektir. Bu, kapsülleme prensibini ihlal eder ve kodun sürdürülmesini ve test edilmesini zorlaştırır.

Dependency Inversion Prensibini uyguladıktan sonra, yüksek seviye modül düşük seviye modülün uyguladığı soyutlamaya (arayüz veya protokol) bağımlı hale gelir. Böylelikle, yüksek seviye modül düşük seviye modülün belirli uygulama detaylarından bağımsız hale gelir.

DIP'nden Sonra:

```swift
protocol PaymentGateway {
    func processPayment(amount: Double)
}

class PaymentProcessor {
    private let paymentGateway: PaymentGateway

    init(paymentGateway: PaymentGateway) {
        self.paymentGateway = paymentGateway
    }

    func processPayment(amount: Double) {
        // Process the payment using the provided payment gateway
        paymentGateway.processPayment(amount)
    }
}

class PayPalGateway: PaymentGateway {
    func processPayment(amount: Double) {
        // Implementation of processing the payment using PayPal
    }
}

class StripeGateway: PaymentGateway {
    func processPayment(amount: Double) {
        // Implementation of processing the payment using Stripe
    }
}
```

Güncellenmiş örnekte, ödeme işlemlerini gerçekleştirmek için PaymentGateway protokolünü tanıtıyoruz. PaymentProcessor sınıfı artık somut bir uygulamaya değil soyutlamaya (protokol) bağımlıdır. PaymentGateway protokolünü uygulayan farklı ödeme ağ geçitleri (örneğin PayPalGateway, StripeGateway) oluşturabilir ve çalışma zamanında bunları PaymentProcessor'a iletebiliriz.

Bu tasarım, PaymentProcessor sınıfını değiştirmeden ödeme ağ geçitlerini kolayca değiştirme veya genişletme olanağı sağlar. Gevşek bağlılığı teşvik eder ve kodun sürdürülebilirliğini, test edilebilirliğini ve esnekliğini artırır.


