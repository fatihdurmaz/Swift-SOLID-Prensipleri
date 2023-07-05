# SOLID Prensipleri

![blg_inline_solid_principles](https://github.com/vishalMalvi/SOLID-Principles-in-Swift/assets/97470591/4fba6f05-ad99-42e1-b53a-7abaced1d6f0)


### SOLID prensipleri, iyi ve bakımı kolay kod yazmak için bir dizi kılavuzdur. İşte Swift bağlamında her prensibin kısa bir açıklaması:

Tek Sorumluluk Prensibi (SRP): Her sınıf veya modülün yalnızca bir sorumluluğu olmalıdır. Swift'te bu, bir sınıfın yalnızca değişiklik yapma sebebi olması gerektiği anlamına gelir.

Açık/Kapalı Prensibi (OCP): Sınıflar genişletmeye açık, değişikliğe kapalı olmalıdır. Başka bir deyişle, mevcut kodunu değiştirmeden bir sınıfa yeni işlevsellik ekleyebilmelisiniz.

Liskov Yerine Geçme Prensibi (LSP): Alt tipler, temel tiplerinin yerine geçebilmelidir. Swift'te bu, bir alt sınıfın, üst sınıfının yerine kullanılabilmeli ve beklenmeyen davranışlara neden olmamalıdır.

Arayüz Ayırma Prensibi (ISP): Müşteriler, kullanmadıkları arayüzlerden bağımlı olmamalıdır. Swift'te bu, ihtiyaç duyulmayan yöntemleri içeren büyük arayüzler yerine daha küçük protokoller tanımlamanız gerektiği anlamına gelir.

Bağımlılık Tersine Çevirme Prensibi (DIP): Yüksek seviyeli modüller, düşük seviyeli modüllere bağlı olmamalıdır. Bunun yerine her ikisi de soyutlamalara bağlı olmalıdır. Swift'te bu, sınıflar arasındaki arayüzleri tanımlamak için somut uygulamalara dayanmak yerine protokoller kullanmanız gerektiği anlamına gelir.
