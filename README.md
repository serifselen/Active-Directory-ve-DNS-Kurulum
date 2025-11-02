# Active Directory ve DNS Kurulum Rehberi  
**Windows Server 2025 Üzerinde AD DS ve DNS Kurulumu**

Bu rehber, **Windows Server 2025 Standard Evaluation** sistemine **Active Directory Domain Services (AD DS)** ve **DNS Server** rollerinin nasıl kurulacağını adım adım açıklar. Kurulum, `Server Manager` aracılığıyla gerçekleştirilir.

---

## 📑 İçindekiler

- [Adım 1: Server Manager Ana Ekranı](#adım-1-server-manager-ana-ekranı)
- [Adım 2: “Add Roles and Features Wizard” Başlatma](#adım-2-add-roles-and-features-wizard-başlatma)
- [Adım 3: Kurulum Türü Seçimi](#adım-3-kurulum-türü-seçimi)
- [Adım 4: Hedef Sunucu Seçimi](#adım-4-hedef-sunucu-seçimi)
- [Adım 5: Active Directory Domain Services Rolü Seçimi](#adım-5-active-directory-domain-services-rolü-seçimi)
- [Adım 6: Deployment Configuration – Yeni Orman Oluşturma](#adım-6-deployment-configuration--yeni-orman-oluşturma)
- [Adım 7: Domain Controller Seçenekleri](#adım-7-domain-controller-seçenekleri)
- [Adım 8: Ön Koşul Denetimi](#adım-8-ön-koşul-denetimi)
- [Adım 9: Kurulum İlerleme Durumu](#adım-9-kurulum-ilerleme-durumu)
- [Adım 10: Post-deployment Yapılandırma Uyarısı](#adım-10-post-deployment-yapılandırma-uyarısı)
- [Kurulum Sonrası Öneriler](#kurulum-sonrası-öneriler)
- [Doküman Bilgileri](#doküman-bilgileri)

---

## Adım 1: Server Manager Ana Ekranı

![Adım 1](Images/1.png)

`Server Manager` açıldığında sol üst köşede **“QUICK START”** bölümü görünür. Burada:

- **Configure this local server**
- **Add roles and features**
- **Add other servers to manage**

seçenekleri yer alır.

> ✅ AD DS kurulumuna başlamak için **“Add roles and features”** bağlantısına tıklayın.

---

## Adım 2: “Add Roles and Features Wizard” Başlatma

![Adım 2](Images/2.png)

**Before You Begin** ekranında, kurulum öncesi ön koşullar özetlenir:

- Güçlü bir yönetici şifresi
- Statik IP yapılandırması
- Güncel sistem yamaları

> 💡 Bu sayfa yalnızca bilgilendiricidir. **Next** butonuna tıklayarak devam edin.

---

## Adım 3: Kurulum Türü Seçimi

![Adım 3](Images/3.png)

**Installation Type** ekranında iki seçenek sunulur:

- **Role-based or feature-based installation**  
- **Remote Desktop Services installation**

> ✅ **“Role-based or feature-based installation”** seçeneğini işaretleyin. Bu, sunucuya roller eklemek için kullanılır.  
> **Next** butonuna tıklayın.

---

## Adım 4: Hedef Sunucu Seçimi

![Adım 4](Images/4.png)

**Server Selection** ekranında:

- **Name**: `DOMAIN`  
- **IP Address**: `192.168.31.100`  
- **Operating System**: `Windows Server 2025 Standard Evaluation`

gibi bilgiler görüntülenir.

> ✅ Kurulum yapılacak sunucu zaten seçili gelir. Doğru sunucuyu seçtiğinizden emin olduktan sonra **Next** butonuna tıklayın.

---

## Adım 5: Active Directory Domain Services Rolü Seçimi

![Adım 5](Images/5.png)

**Server Roles** listesinden **“Active Directory Domain Services”** kutusunu işaretleyin.

Sistem, bu rol için gerekli yönetim araçlarını önerir:

- Group Policy Management
- AD DS and AD LDS Tools
- Active Directory Administrative Center
- AD DS Snap-Ins and Command-Line Tools

> ✅ **“Include management tools (if applicable)”** seçeneği otomatik işaretlenir.  
> Açılan pencerede **Add Features** butonuna tıklayıp **Next** butonuna geçin.

---

## Adım 6: Deployment Configuration – Yeni Orman Oluşturma

![Adım 6](Images/6.png)

AD DS kurulumu tamamlandıktan sonra **“Promote this server to a domain controller”** bağlantısıyla açılan sihirbazda:

- ☑ **Add a new forest** seçeneği işaretlenir  
- **Root domain name**: `serifselen.local` girilir

> ⚠️ Eğer **“Verification of forest name failed”** uyarısı alırsanız:
> - Etki alanı adını basitleştirin (`ad.local` gibi)
> - DNS sunucusu ayarlarını kontrol edin

**Next** butonuna tıklayın.

---

## Adım 7: Domain Controller Seçenekleri

![Adım 7](Images/7.png)

**Domain Controller Options** ekranında:

- **Forest functional level**: `Windows Server 2025`  
- **Domain functional level**: `Windows Server 2025`  
- ☑ **DNS server**  
- ☑ **Global Catalog (GC)**  
- **DSRM password**: Güçlü bir şifre girilir

> 🔒 DSRM (Directory Services Restore Mode) şifresi, acil durum kurtarma modu için gereklidir.  
> **Next** butonuna tıklayın.

---

## Adım 8: Ön Koşul Denetimi

![Adım 8](Images/8.png)

**Prerequisites Check** ekranında:

- ✅ **All prerequisite checks passed successfully**

uyarıları görüntülenir.

> ⚠️ “A delegation for this DNS server cannot be created…” uyarısı, mevcut bir DNS altyapısı yoksa **ihmal edilebilir**.  
> **Install** butonuna tıklayarak kurulumu başlatın.

---

## Adım 9: Kurulum İlerleme Durumu

![Adım 9](Images/9.png)

**Installation progress** ekranında yüklenen bileşenler listelenir:

- Active Directory Domain Services  
- Group Policy Management  
- Remote Server Administration Tools  
- AD DS Tools  
- Active Directory PowerShell modülleri

> 🔄 Kurulum tamamlandığında sunucu **otomatik olarak yeniden başlatılır**.

---

## Adım 10: Post-deployment Yapılandırma Uyarısı

![Adım 10](Images/10.png)

Sunucu yeniden başladığında `Server Manager` dashboard’unda sağ üst köşede bir uyarı simgesi belirir:

> **Post-deployment Configuration**  
> Configuration required for Active Directory Domain Services at DOMAIN  
> **Promote this server to a domain controller**

> ✅ Bu uyarı, AD DS yapılandırmasının tamamlanmadığını gösterir.  
> Bağlantıya tıklayarak yapılandırmayı tamamlayabilir veya komut satırından `dcpromo` ile devam edebilirsiniz.

---

## 🎉 Kurulum Tamamlandı!

Sunucunuz artık **`serifselen.local`** etki alanında bir **Domain Controller** olarak çalışmaktadır. **DNS Server** hizmeti de otomatik olarak yapılandırılmıştır.

---

## 🔧 Kurulum Sonrası Öneriler

1. **Kullanıcı ve Grup Yönetimi**  
   - Active Directory Users and Computers (ADUC) üzerinden ilk kullanıcıları oluşturun.
2. **Grup İlkesi (GPO) Yapılandırması**  
   - Güvenlik politikaları, şifre kuralları gibi ayarları tanımlayın.
3. **Diğer Sunucuları Etki Alanına Katma**  
   - Üye sunucuların `serifselen.local` etki alanına katılmasını sağlayın.
4. **Yedekleme ve Kurtarma Planı**  
   - System State yedeklemesi alın.
5. **Güvenlik Duvarı ve Ağ İzolasyonu**  
   - Gerekli portları (TCP 53, 88, 389, 445, 3268 vb.) açın.

---

## 📄 Doküman Bilgileri

| Özellik | Değer |
|--------|-------|
| **Yazar** | Serif Belen |
| **Tarih** | 2 Kasım 2025 |
| **Platform** | VMware Workstation Pro 17 |
| **İşletim Sistemi** | Windows Server 2025 Standard Evaluation |
| **Etki Alanı Adı** | `serifselen.local` |
| **DNS** | Otomatik olarak kurulmuştur |
| **Lisans** | Evaluation (180 gün) |

---

> 📝 Bu doküman **eğitim ve test ortamları** için hazırlanmıştır. Üretimde lisanslı yazılım ve güvenlik önlemleri kullanılmalıdır.