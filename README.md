# Windows Server 2025 Active Directory ve DNS Kurulum Rehberi

## 1. Server Manager Başlatma

**Dosya: 1.png**

- **Amaç**: Sunucu yönetim konsolunu başlatma
- **İşlem**: 
  - Server Manager dashboard'ını aç
  - "Add roles and features" seçeneğini seç
- **Not**: Bu, rollerin ve özelliklerin kurulumunu başlatmak için başlangıç noktasıdır

## 2. Kurulum Sihirbazı Başlangıç

**Dosya: 2.png**

- **Ön Gereksinimler Kontrolü**:
  - Administrator hesabında güçlü parola kontrolü
  - Statik IP adresi gibi ağ ayarlarının doğrulanması
  - En güncel Windows Update güvenlik güncellemelerinin yüklü olduğunun teyidi
- **Seçenek**: "Skip this page by default" - Bu sayfanın varsayılan olarak atlanması

## 3. Kurulum Türü Seçimi

**Dosya: 3.png**

- **Kurulum Türleri**:
  - **Role-based or feature-based installation**: Tek sunucu üzerinde rol, rol servisleri ve özelliklerin kurulumu
  - **Remote Desktop Services installation**: VDI (Virtual Desktop Infrastructure) için gerekli rol servislerinin kurulumu
- **Seçim**: Role-based or feature-based installation seçildi

## 4. Hedef Sunucu Seçimi

**Dosya: 4.png**

- **Sunucu Havuzu**: DOMAIN (192.168.31.100)
- **İşletim Sistemi**: Microsoft Windows Server 2025 Standard Evaluation
- **Seçim**: Sunucu havuzundan mevcut sunucu seçildi
- **Filtre**: Windows Server 2012 veya üzeri çalışan sunucular gösterilir

## 5. Sunucu Rolleri Seçimi

**Dosya: 5.png**

- **Seçilen Rol**: Active Directory Domain Services (AD DS)
- **Gerekli Özellikler Otomatik Tespit**:
  - Group Policy Management
  - Remote Server Administration Tools
  - AD DS and AD LDS Tools
  - Active Directory module for Windows PowerShell
  - Active Directory Administrative Center
  - AD DS Snap-Ins and Command-Line Tools
- **Açıklama**: AD DS, ağ üzerindeki nesneler hakkında bilgi depolar ve bu bilgiyi kullanıcılara ve ağ yöneticilerine sağlar

## 6. Kurulum İlerlemesi

**Dosya: 6.png**

- **Kurulan Bileşenler**:
  - Active Directory Domain Services
  - Tüm yönetim araçları ve PowerShell modülleri
- **Özellik**: Kurulum devam ederken sihirbaz kapatılabilir
- **İzleme**: Notification Center üzerinden task detayları takip edilebilir

## 7. Post-Deployment Yapılandırma

**Dosya: 7.png**

- **Sonraki Adım**: "Promote this server to a domain controller"
- **Durum**: Özellik kurulumu başarılı, yapılandırma gerekli
- **Server Manager Dashboard**: AD DS servisi artık yönetilebilir durumda

## 8. AD DS Dağıtım Yapılandırması

**Dosya: 8.png**

- **Dağıtım İşlemi**: "Add a new forest" seçildi
- **Kök Domain Adı**: serifselen.local
- **Doğrulama**: Forest ismi doğrulaması başarısız (DNS ismi kontrolü)
- **Not**: Yeni bir Active Directory ormanı oluşturuluyor

## 9. Domain Controller Seçenekleri

**Dosya: 9.png**

- **Fonksiyonel Seviyeler**:
  - Forest functional level: Windows Server 2025
  - Domain functional level: Windows Server 2025
- **Domain Controller Yetenekleri**:
  - ✓ Domain Name System (DNS) server
  - ✓ Global Catalog (GC)
  - ✗ Read only domain controller (RODC)
- **DSRM Password**: Directory Services Restore Mode için parola ayarlandı

## 10. Önkoşul Kontrolleri

**Dosya: 10.png**

- **Sonuç**: Tüm önkoşul kontrolleri başarıyla geçildi
- **DNS Uyarısı**: Üst DNS zone bulunamadı veya Windows DNS sunucusu değil
- **Çözüm**: Mevcut DNS altyapısı ile entegrasyon için manuel delegation oluşturulması önerildi
- **Otomatik Yeniden Başlatma**: Kurulum tamamlandığında sunucu otomatik olarak yeniden başlayacak

---

## Teknik Notlar

- **DNS Entegrasyonu**: Mevcut DNS altyapısı ile uyumluluk için manuel zone delegation gerekli
- **Fonksiyonel Seviye**: Windows Server 2025 seviyesi, en yeni özelliklerin kullanımını sağlar
- **Global Catalog**: Çok domainli ortamlarda arama işlemlerini optimize eder
- **DSRM**: Directory Services kurtarma modu için kritik parola yönetimi