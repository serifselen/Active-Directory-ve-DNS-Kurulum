# Active Directory Domain Services ve DNS Kurulum Rehberi

Bu dokümanda Windows Server 2025 üzerinde Active Directory Domain Services (AD DS) ve DNS kurulum adımları detaylı olarak açıklanmaktadır.

## İçindekiler

- [Adım 1: Active Directory Domain Services Prerequisites Check](#adım-1-active-directory-domain-services-prerequisites-check)
- [Adım 2: Add Roles and Features Wizard - Başlangıç](#adım-2-add-roles-and-features-wizard---başlangıç)
- [Adım 3: Installation Type Seçimi](#adım-3-installation-type-seçimi)
- [Adım 4: Hedef Sunucu Seçimi](#adım-4-hedef-sunucu-seçimi)
- [Adım 5: Server Roles Seçimi](#adım-5-server-roles-seçimi)
- [Adım 6: Features Kurulum ve İlerleme](#adım-6-features-kurulum-ve-i̇lerleme)
- [Adım 7: Post-deployment Configuration](#adım-7-post-deployment-configuration)
- [Adım 8: Deployment Configuration](#adım-8-deployment-configuration)
- [Adım 9: Domain Controller Options](#adım-9-domain-controller-options)
- [Adım 10: Kurulum Tamamlandı](#adım-10-kurulum-tamamlandı)

---

## Adım 1: Active Directory Domain Services Prerequisites Check

![Adım 1](Images/1.png)

Active Directory Domain Services Configuration Wizard'ın Prerequisites Check ekranıdır.

### Durum:

✅ **All prerequisite checks passed successfully. Click 'Install' to begin installation.**

### Uyarılar ve Bilgiler:

#### ⚠️ DNS Delegation Uyarısı:

> "A delegation for this DNS server cannot be created because the authoritative parent zone cannot be found or it does not run Windows DNS server. If you are integrating with an existing DNS infrastructure, you should manually create a delegation to this DNS server in the parent zone to ensure reliable name resolution from outside the domain "serifselen.local". Otherwise, no action is required."

**Açıklama:**
- Bu DNS sunucusu için delegasyon oluşturulamıyor
- Üst bölge bulunamıyor veya Windows DNS sunucusu çalıştırmıyor
- Mevcut DNS altyapısıyla entegrasyon yapıyorsanız, güvenilir isim çözümlemesi için parent zone'da manuel olarak delegasyon oluşturmalısınız
- Aksi takdirde herhangi bir işlem gerekmez

#### ℹ️ Prerequisites Check Completed:

✅ **"All prerequisite checks passed successfully. Click 'Install' to begin installation."**

### Sol Menü Adımları:

1. Deployment Configuration
2. Domain Controller Options
3. DNS Options
4. Additional Options
5. Paths
6. Review Options
7. **Prerequisites Check** (Mevcut adım)
8. Installation
9. Results

### ⚠️ Önemli Not:

> "If you click Install, the server automatically reboots at the end of the promotion operation."

Sunucu, promotion işleminin sonunda otomatik olarak yeniden başlatılacaktır.

### Butonlar:

- **< Previous**: Önceki adıma dön
- **Next >**: Sonraki adım (pasif)
- **Install**: Kurulumu başlat
- **Cancel**: İptal et

**"Install"** butonuna tıklayarak Active Directory Domain Services kurulumunu başlatınız.

---

## Adım 2: Add Roles and Features Wizard - Başlangıç

![Adım 2](Images/2.png)

Add Roles and Features Wizard'ın başlangıç ekranıdır.

### Before you begin

Bu sihirbaz, roller, rol servisleri veya özellikleri yüklemenize yardımcı olur. Hangi rol, rol servisi veya özelliklerin yükleneceğini, kuruluşunuzun bilgi işlem ihtiyaçlarına göre belirlersiniz (örneğin belge paylaşımı veya web sitesi barındırma).

### Roller veya Servisleri Kaldırmak İçin:

**Start the Remove Roles and Features Wizard**

### Devam Etmeden Önce Doğrulayın:

Aşağıdaki görevlerin tamamlandığını doğrulayın:

- ✅ **The Administrator account has a strong password**
  - Yönetici hesabının güçlü bir şifresi var

- ✅ **Network settings, such as static IP addresses, are configured**
  - Statik IP adresleri gibi ağ ayarları yapılandırıldı

- ✅ **The most current security updates from Windows Update are installed**
  - Windows Update'ten en güncel güvenlik güncellemeleri yüklendi

### 💡 Önemli Not:

> "If you must verify that any of the preceding prerequisites have been completed, close the wizard, complete the steps, and then run the wizard again."

Önkoşullardan herhangi birinin tamamlandığını doğrulamanız gerekiyorsa, sihirbazı kapatın, adımları tamamlayın ve ardından sihirbazı tekrar çalıştırın.

### Ek Bilgi:

"To continue, click Next."

### Sol Menü Adımları:

1. **Before You Begin** (Mevcut adım)
2. Installation Type
3. Server Selection
4. Server Roles
5. Features
6. Confirmation
7. Results

### Seçenekler:

☐ **Skip this page by default**

### Butonlar:

- **< Previous**: Önceki adım (pasif)
- **Next >**: Sonraki adım
- **Install**: Kur (pasif)
- **Cancel**: İptal et

**"Next >"** butonuna tıklayarak devam ediniz.

---

## Adım 3: Installation Type Seçimi

![Adım 3](Images/3.png)

Select installation type ekranında kurulum türü belirlenir.

### Installation Type Seçenekleri:

#### ☑ Role-based or feature-based installation

**Açıklama:**
- Tek bir sunucuyu roller, rol servisleri ve özellikler ekleyerek yapılandırın
- Configure a single server by adding roles, role services, and features

#### ☐ Remote Desktop Services installation

**Açıklama:**
- Virtual Desktop Infrastructure (VDI) için gerekli rol servislerini yükleyin
- Sanal makine tabanlı veya oturum tabanlı masaüstü dağıtımı oluşturun
- Install required role services for Virtual Desktop Infrastructure (VDI) to create a virtual machine-based or session-based desktop deployment

### Sol Menü Adımları:

1. Before You Begin
2. **Installation Type** (Mevcut adım)
3. Server Selection
4. Server Roles
5. Features
6. Confirmation
7. Results

### Önerilen Seçim:

> ✅ **Role-based or feature-based installation** seçeneğini işaretleyiniz.

### Butonlar:

- **< Previous**: Önceki adıma dön
- **Next >**: Sonraki adım
- **Install**: Kur (pasif)
- **Cancel**: İptal et

**"Next >"** butonuna tıklayarak devam ediniz.

---

## Adım 4: Hedef Sunucu Seçimi

![Adım 4](Images/4.png)

Select destination server ekranında roller ve özelliklerin yükleneceği sunucu veya sanal sabit disk seçilir.

### Seçenekler:

#### ☑ Select a server from the server pool

Sunucu havuzundan bir sunucu seçin.

#### ☐ Select a virtual hard disk

Sanal sabit disk seçin.

### Server Pool

Sunucu listesi aşağıdaki bilgileri içermektedir:

| Name | IP Address | Operating System |
|------|------------|------------------|
| **DOMAIN** | 192.168.31.100 | Microsoft Windows Server 2025 Standard Evaluation |

**1 Computer(s) found**

### 💡 Önemli Bilgi:

> "This page shows servers that are running Windows Server 2012 or a newer release of Windows Server, and that have been added by using the Add Servers command in Server Manager. Offline servers and newly-added servers from which data collection is still incomplete are not shown."

Bu sayfa, Windows Server 2012 veya daha yeni bir Windows Server sürümünü çalıştıran ve Server Manager'da Add Servers komutu kullanılarak eklenmiş sunucuları gösterir. Çevrimdışı sunucular ve veri toplama işlemi henüz tamamlanmamış yeni eklenen sunucular gösterilmez.

### Sol Menü Adımları:

1. Before You Begin
2. Installation Type
3. **Server Selection** (Mevcut adım)
4. Server Roles
5. Features
6. Confirmation
7. Results

### Butonlar:

- **< Previous**: Önceki adıma dön
- **Next >**: Sonraki adım
- **Install**: Kur (pasif)
- **Cancel**: İptal et

Listeden **DOMAIN** sunucusunu seçili bırakın ve **"Next >"** butonuna tıklayınız.

---

## Adım 5: Server Roles Seçimi

![Adım 5](Images/5.png)

Select server roles ekranında seçilen sunucuya yüklenecek bir veya daha fazla rol seçilir.

### Roles Listesi:

| Rol | Açıklama |
|-----|----------|
| ☐ Active Directory Certificate Services | - |
| ☑ **Active Directory Domain Services** | **AD DS, ağdaki nesneler hakkında bilgi depolar ve bu bilgiyi kullanıcılar ve ağ yöneticileri için kullanılabilir hale getirir. AD DS, kullanıcılara ağdaki kaynaklara erişim izni vermek için domain controller'ları kullanır.** |
| ☐ Active Directory Federation Services | - |
| ☐ Active Directory Lightweight Directory Services | - |
| ☐ Active Directory Rights Management Services | - |
| ☐ Device Health Attestation | - |

### Pop-up Dialog: Add features that are required for Active Directory Domain Services?

**Mesaj:**
> "You cannot install Active Directory Domain Services unless the following role services or features are also installed."

Active Directory Domain Services'i yükleyemezsininiz, aşağıdaki rol servisleri veya özellikleri de yüklenmediği sürece.

### Gerekli Özellikler:

```
[Tools] Group Policy Management
  ✓ Remote Server Administration Tools
    ✓ Role Administration Tools
      ✓ AD DS and AD LDS Tools
        ✓ Active Directory module for Windows PowerShell
        ✓ AD DS Tools
          ✓ [Tools] Active Directory Administrative Center
          ✓ [Tools] AD DS Snap-Ins and Command-Line Tools
```

### Seçenekler:

☑ **Include management tools (if applicable)**

Yönetim araçları (varsa) dahil edilsin.

### Pop-up Butonları:

- **Add Features**: Özellikleri ekle
- **Cancel**: İptal et

### Sol Menü Adımları:

1. Before You Begin
2. Installation Type
3. Server Selection
4. **Server Roles** (Mevcut adım)
5. Features
6. Confirmation
7. Results

### Yapılacaklar:

1. **Active Directory Domain Services** kutusunu işaretleyiniz
2. Açılan pop-up'ta **"Add Features"** butonuna tıklayınız
3. Ana ekranda **"Next >"** butonuna tıklayarak devam ediniz

---

## Adım 6: Features Kurulum ve İlerleme

![Adım 6](Images/6.png)

Installation progress ekranı, seçilen rollerin ve özelliklerin kurulum ilerlemesini gösterir.

### View installation progress

#### 🔵 Feature installation

**İlerleme Çubuğu:** Kurulum devam ediyor

**Installation started on DOMAIN**

### Yüklenen Bileşenler:

```
Active Directory Domain Services
Group Policy Management
Remote Server Administration Tools
  Role Administration Tools
    AD DS and AD LDS Tools
      Active Directory module for Windows PowerShell
      AD DS Tools
        Active Directory Administrative Center
        AD DS Snap-Ins and Command-Line Tools
```

### 💡 Önemli Bilgi:

> "You can close this wizard without interrupting running tasks. View task progress or open this page again by clicking Notifications in the command bar, and then Task Details."

Çalışan görevleri kesmeden bu sihirbazı kapatabilirsiniz. Görev ilerlemesini görüntüleyin veya komut çubuğundaki Notifications'a ve ardından Task Details'e tıklayarak bu sayfayı tekrar açın.

### Ek Seçenek:

**Export configuration settings** - Yapılandırma ayarlarını dışa aktar

### Sol Menü Adımları:

1. Before You Begin
2. Installation Type
3. Server Selection
4. Server Roles
5. Features
6. AD DS
7. Confirmation
8. **Results** (Mevcut adım)

### Butonlar:

- **< Previous**: Önceki adıma dön (pasif)
- **Next >**: Sonraki adım (pasif)
- **Close**: Kapat
- **Cancel**: İptal et (pasif)

> ⏳ Kurulum tamamlanana kadar bekleyiniz. Kurulum başarıyla tamamlandığında bir sonraki adıma geçebilirsiniz.

---

## Adım 7: Post-deployment Configuration

![Adım 7](Images/7.png)

Server Manager Dashboard ekranında kurulum sonrası yapılandırma bildirimi görüntülenmektedir.

### Bildirimler:

#### ⚠️ Post-deployment Configuration

**Configuration required for Active Directory Domain Services at DOMAIN**

**Bağlantı:**
**Promote this server to a domain controller**

Bu sunucuyu bir domain controller'a yükseltin.

#### ℹ️ Feature installation

**TASKS** ▼ | ✕

**Configuration required. Installation succeeded on DOMAIN.**

Yapılandırma gerekli. Kurulum DOMAIN üzerinde başarılı oldu.

**Add Roles and Features**

**Task Details** - Görev detayları

### WELCOME TO SERVER MANAGER

#### 1️⃣ Configure this local server

#### 2️⃣ Add roles and features

#### 3️⃣ Add other servers to manage

#### 4️⃣ Create a server group

### Sol Panel:

- 📊 **Dashboard** (Aktif)
- 💻 Local Server
- 📁 All Servers
- 📘 AD DS
- 📂 File and Storage Services

### Yapılacak İşlem:

> ✅ **"Promote this server to a domain controller"** bağlantısına tıklayarak Active Directory yapılandırmasına başlayınız.

Bu adım, sunucunuzu bir domain controller'a dönüştürecek ve Active Directory hizmetlerini başlatacaktır.

---

## Adım 8: Deployment Configuration

![Adım 8](Images/8.png)

Active Directory Domain Services Configuration Wizard'ın Deployment Configuration ekranıdır.

### ❌ Hata Mesajı:

> **"Verification of forest name failed. The DNS name "serifselen" proposed for this Active Directory domain con..."**

**Show more** | ✕

### Select the deployment operation

Dağıtım işlemini seçin:

#### ☐ Add a domain controller to an existing domain

Mevcut bir domain'e domain controller ekleyin.

#### ☐ Add a new domain to an existing forest

Mevcut bir forest'e yeni domain ekleyin.

#### ☑ Add a new forest

Yeni bir forest ekleyin.

### Specify the domain information for this operation

Bu işlem için domain bilgilerini belirtin:

**Root domain name:**
```
serifselen.local
```

### 💡 Domain Adı Formatı:

> Domain adının `.local` uzantısıyla bitmesi önerilir. Bu, yerel ağ domain'leri için standart bir uygulamadır.

**Örnek doğru formatlar:**
- `serifselen.local`
- `company.local`
- `organization.local`

### Bağlantı:

**More about deployment configurations** - Dağıtım yapılandırmaları hakkında daha fazla bilgi

### Sol Menü Adımları:

1. **Deployment Configuration** (Mevcut adım)
2. Domain Controller Options
3. Additional Options
4. Paths
5. Review Options
6. Prerequisites Check
7. Installation
8. Results

### Butonlar:

- **< Previous**: Önceki adıma dön
- **Next >**: Sonraki adım
- **Install**: Kur (pasif)
- **Cancel**: İptal et

### ⚠️ Önemli Not:

Hata mesajı görünüyorsa, root domain name'i kontrol ediniz. Doğru format: `serifselen.local`

**"Next >"** butonuna tıklayarak devam ediniz.

---

## Adım 9: Domain Controller Options

![Adım 9](Images/9.png)

Domain Controller Options ekranında yeni forest ve root domain için fonksiyonel seviye ve domain controller özellikleri belirlenir.

### Select functional level of the new forest and root domain

#### Forest functional level:
```
Windows Server 2025 ▼
```

#### Domain functional level:
```
Windows Server 2025 ▼
```

### Specify domain controller capabilities

Domain controller yeteneklerini belirtin:

#### ☑ Domain Name System (DNS) server

DNS sunucusu yeteneği ekler.

#### ☑ Global Catalog (GC)

Global Catalog sunucusu yeteneği ekler.

#### ☐ Read only domain controller (RODC)

Salt okunur domain controller (pasif - yeni forest'te kullanılamaz).

### Type the Directory Services Restore Mode (DSRM) password

DSRM şifresi, Active Directory'yi geri yükleme modunda başlatırken kullanılır.

#### Password:
```
••••••••
```

#### Confirm password:
```
••••••••
```

### 🔒 DSRM Şifresi Hakkında:

> **Directory Services Restore Mode (DSRM)** şifresi:
> - Active Directory veritabanını geri yüklemek için kullanılır
> - Acil durumlarda domain controller'ı özel modda başlatır
> - Güçlü ve unutulmayacak bir şifre seçiniz
> - Bu şifreyi güvenli bir yerde saklayınız

### Bağlantı:

**More about domain controller options** - Domain controller seçenekleri hakkında daha fazla bilgi

### Sol Menü Adımları:

1. Deployment Configuration
2. **Domain Controller Options** (Mevcut adım)
3. DNS Options
4. Additional Options
5. Paths
6. Review Options
7. Prerequisites Check
8. Installation
9. Results

### Butonlar:

- **< Previous**: Önceki adıma dön
- **Next >**: Sonraki adım
- **Install**: Kur (pasif)
- **Cancel**: İptal et

### Yapılandırma Önerileri:

1. ✅ **DNS server** işaretli kalmalı
2. ✅ **Global Catalog** işaretli kalmalı
3. 🔐 DSRM şifresini güvenli bir şekilde belirleyin
4. 📝 Şifreyi not edin ve güvenli bir yerde saklayın

**"Next >"** butonuna tıklayarak devam ediniz.

---

## Adım 10: Kurulum Tamamlandı

![Adım 10](Images/10.png)

Server Manager Dashboard ekranı, Active Directory Domain Services kurulumunun tamamlandığını göstermektedir.

### WELCOME TO SERVER MANAGER

Dashboard, sunucu yapılandırması için hızlı başlangıç adımlarını içerir:

#### Quick Start Menüsü:

**QUICK START**
1️⃣ **Configure this local server**

**WHAT'S NEW**
2️⃣ **Add roles and features**
3️⃣ **Add other servers to manage**
4️⃣ **Create a server group**
5️⃣ **Connect this server to cloud services**

**LEARN MORE**

### Sol Panel Menüsü:

- 📊 Dashboard
- 💻 Local Server
- 📁 All Servers
- 📘 **AD DS** (Active Directory Domain Services artık görünüyor)
- 📂 File and Storage Services

### 🎉 Kurulum Başarıyla Tamamlandı!

Active Directory Domain Services ve DNS kurulumu başarıyla tamamlanmıştır. Sunucu artık bir Domain Controller olarak yapılandırılmıştır.

---

## ✅ Kurulum Sonrası Kontroller

Kurulumun başarılı olduğunu doğrulamak için aşağıdaki kontrolleri yapınız:

### 1. Active Directory Users and Computers

**Başlat > Windows Administrative Tools > Active Directory Users and Computers**

- Domain yapısını kontrol edin
- Varsayılan OU'ların (Organizational Units) oluşturulduğunu doğrulayın

### 2. DNS Manager

**Başlat > Windows Administrative Tools > DNS**

- Forward Lookup Zones'u kontrol edin
- Reverse Lookup Zones'u kontrol edin
- Domain kaydının düzgün oluşturulduğunu doğrulayın

### 3. Server Manager

**AD DS** sekmesinden:
- Domain Controller'ın çalıştığını doğrulayın
- Event logs'u kontrol edin
- Hata veya uyarı olup olmadığına bakın

### 4. PowerShell Kontrolü

Aşağıdaki PowerShell komutlarını çalıştırarak kontrollerinizi yapabilirsiniz:

```powershell
# AD Domain bilgilerini görüntüle
Get-ADDomain

# Domain Controller bilgilerini görüntüle
Get-ADDomainController

# DNS Zones'ları listele
Get-DnsServerZone

# AD DS Service durumunu kontrol et
Get-Service NTDS, DNS, Netlogon
```

---

## 📋 Yapılandırma Özeti

### Active Directory Yapılandırması:

| Özellik | Değer |
|---------|-------|
| **Forest Name** | serifselen.local |
| **Domain Name** | serifselen.local |
| **Forest Functional Level** | Windows Server 2025 |
| **Domain Functional Level** | Windows Server 2025 |
| **Server Name** | DOMAIN |
| **IP Address** | 192.168.31.100 |

### Yüklenen Roller ve Özellikler:

- ✅ Active Directory Domain Services
- ✅ DNS Server
- ✅ Group Policy Management
- ✅ Remote Server Administration Tools
- ✅ Active Directory module for Windows PowerShell
- ✅ Active Directory Administrative Center
- ✅ AD DS Snap-Ins and Command-Line Tools

---

## 🚀 Sonraki Adımlar

### 1. Kullanıcı ve Grup Yönetimi

- Organizational Units (OU) oluşturun
- Kullanıcı hesapları ekleyin
- Güvenlik grupları tanımlayın

### 2. Group Policy Yönetimi

- GPO'lar oluşturun
- Güvenlik politikaları tanımlayın
- Kullanıcı ve bilgisayar ayarlarını yapılandırın

### 3. DNS Yapılandırması

- Ek DNS kayıtları ekleyin
- Reverse Lookup Zones yapılandırın
- Forwarders ayarlayın

### 4. Yedekleme Stratejisi

- Windows Server Backup yapılandırın
- System State yedekleme planlayın
- Disaster Recovery planı oluşturun

### 5. Güvenlik Sertleştirme

- Firewall kurallarını yapılandırın
- Audit policies aktifleştirin
- Şifre politikalarını gözden geçirin
- Multi-factor authentication düşünün

---

## ⚠️ Önemli Güvenlik Notları

### Şifre Yönetimi:

🔐 **Administrator Şifresi:**
- Güçlü ve karmaşık olmalı
- Düzenli olarak değiştirilmeli
- Güvenli bir yerde saklanmalı

🔐 **DSRM Şifresi:**
- Active Directory geri yükleme için kritik
- Asla unutulmamalı
- Güvenli bir kasada saklanmalı

### Yedekleme:

💾 **System State Backup:**
- Günlük yedekleme yapın
- Yedekleri farklı bir konumda saklayın
- Düzenli olarak restore testleri yapın

### İzleme:

👁️ **Event Logs:**
- Düzenli olarak kontrol edin
- Security logs'u inceleyin
- Anormal aktiviteleri takip edin

---

## 🔧 Sorun Giderme

### Yaygın Sorunlar ve Çözümleri:

#### DNS Çözümlenme Sorunları:

```powershell
# DNS cache temizle
ipconfig /flushdns

# DNS kayıtlarını yeniden kaydet
ipconfig /registerdns

# DNS servisini yeniden başlat
Restart-Service DNS
```

#### Active Directory Replikasyon Sorunları:

```powershell
# Replikasyon durumunu kontrol et
repadmin /showrepl

# Replikasyonu zorla
repadmin /syncall
```

#### Domain Controller Sağlık Kontrolü:

```powershell
# DCDiag çalıştır
dcdiag /v

# Netlogon servisini test et
nltest /dsgetdc:serifselen.local
```

---

## 📚 Faydalı Kaynaklar

### Microsoft Dokümantasyon:

- [Active Directory Domain Services Overview](https://docs.microsoft.com/windows-server/identity/ad-ds/)
- [DNS Server Overview](https://docs.microsoft.com/windows-server/networking/dns/)
- [Group Policy Overview](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/group-policy/)

### PowerShell Komutları:

- [Active Directory PowerShell Module](https://docs.microsoft.com/powershell/module/activedirectory/)
- [DNS Server PowerShell Module](https://docs.microsoft.com/powershell/module/dnsserver/)

---

## 📝 Doküman Bilgileri

| Bilgi | Değer |
|-------|-------|
| **Hazırlayan** | Serif Belen |
| **Tarih** | 2 Kasım 2025 |
| **Platform** | VMware Workstation Pro 17 |
| **İşletim Sistemi** | Windows Server 2025 Standard Evaluation |
| **Domain** | serifselen.local |
| **Sunucu Adı** | DOMAIN |
| **IP Adresi** | 192.168.31.100 |
| **Toplam Adım** | 10 |

---

## 📄 Lisans ve Uyarılar

> ⚠️ Bu doküman eğitim ve test amaçlı hazırlanmıştır. Üretim ortamlarında kullanmadan önce Microsoft'un resmi dokümantasyonunu inceleyin ve profesyonel danışmanlık alın.

> 📌 Windows Server 2025 Evaluation sürümü 180 gün süreyle kullanılabilir.

> 🔒 Üretim ortamlarında mutlaka lisanslı sürümleri kullanın ve güvenlik en iyi uygulamalarını takip edin.

---

**Son Güncelleme:** 2 Kasım 2025