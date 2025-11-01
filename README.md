# Active Directory Domain Services ve DNS Kurulum Rehberi

Bu dokümanda Windows Server 2025 üzerinde Active Directory Domain Services (AD DS) ve DNS kurulum adımları detaylı olarak açıklanmaktadır.

## İçindekiler

- [Adım 1: Server Manager Dashboard - Başlangıç](#adım-1-server-manager-dashboard---başlangıç)
- [Adım 2: Add Roles and Features Wizard - Before You Begin](#adım-2-add-roles-and-features-wizard---before-you-begin)
- [Adım 3: Installation Type Seçimi](#adım-3-installation-type-seçimi)
- [Adım 4: Server Selection - Hedef Sunucu Seçimi](#adım-4-server-selection---hedef-sunucu-seçimi)
- [Adım 5: Server Roles - Active Directory Domain Services Seçimi](#adım-5-server-roles---active-directory-domain-services-seçimi)
- [Adım 6: Installation Progress - Kurulum İlerlemesi](#adım-6-installation-progress---kurulum-i̇lerlemesi)
- [Adım 7: Server Manager - Post-deployment Configuration](#adım-7-server-manager---post-deployment-configuration)
- [Adım 8: Deployment Configuration - Yeni Forest Oluşturma](#adım-8-deployment-configuration---yeni-forest-oluşturma)
- [Adım 9: Domain Controller Options - Fonksiyonel Seviye ve DSRM Şifresi](#adım-9-domain-controller-options---fonksiyonel-seviye-ve-dsrm-şifresi)
- [Adım 10: Prerequisites Check - Son Kontrol ve Kurulum](#adım-10-prerequisites-check---son-kontrol-ve-kurulum)

---

## Adım 1: Server Manager Dashboard - Başlangıç

![Adım 1](Images/1.png)

Server Manager'ın "Welcome to Server Manager" ana dashboard ekranıdır. Bu ekran, sunucu kurulumuna başlamak için hızlı başlangıç adımlarını sunar.

### Ekran Başlığı:

**WELCOME TO SERVER MANAGER**

### Sol Panel - Quick Access Links:

#### **QUICK START** (Turuncu panel)
1️⃣ **Configure this local server**
- Yerel sunucu ayarlarını yapılandır

#### **WHAT'S NEW** (Sarı-turuncu panel)
2️⃣ **Add roles and features**
- Roller ve özellikler ekle

3️⃣ **Add other servers to manage**
- Yönetilecek diğer sunucuları ekle

4️⃣ **Create a server group**
- Sunucu grubu oluştur

5️⃣ **Connect this server to cloud services**
- Bu sunucuyu bulut hizmetlerine bağla

#### **LEARN MORE** (Sarı panel)
- Daha fazla bilgi edin

### 💡 İlk Adım:

Active Directory Domain Services kurulumuna başlamak için **"Add roles and features"** (2. seçenek) linkine tıklamanız gerekmektedir.

> ✅ **"Add roles and features"** seçeneğine tıklayarak kurulum sihirbazını başlatınız.

---

## Adım 2: Add Roles and Features Wizard - Before You Begin

![Adım 2](Images/2.png)

Add Roles and Features Wizard'ın başlangıç ekranıdır. Bu ekran, kuruluma başlamadan önce gereksinimleri kontrol etmenizi sağlar.

### Üst Bilgi:

**DESTINATION SERVER**
**DOMAIN**

### Başlık:

**Before you begin**

### Açıklama:

> "This wizard helps you install roles, role services, or features. You determine which roles, role services, or features to install based on the computing needs of your organization, such as sharing documents, or hosting a website."

Bu sihirbaz, roller, rol servisleri veya özellikleri yüklemenize yardımcı olur. Kuruluşunuzun bilgi işlem ihtiyaçlarına göre hangi rollerin, rol servislerinin veya özelliklerin yükleneceğini belirlersiniz; örneğin belge paylaşımı veya web sitesi barındırma.

### Rolleri veya Özellikleri Kaldırmak İçin:

**To remove roles, role services, or features:**
**Start the Remove Roles and Features Wizard**

### Devam Etmeden Önce Doğrulayın:

**Before you continue, verify that the following tasks have been completed:**

Devam etmeden önce, aşağıdaki görevlerin tamamlandığını doğrulayın:

- **• The Administrator account has a strong password**
  - Yönetici hesabının güçlü bir şifresi var

- **• Network settings, such as static IP addresses, are configured**
  - Statik IP adresleri gibi ağ ayarları yapılandırıldı

- **• The most current security updates from Windows Update are installed**
  - Windows Update'ten en güncel güvenlik güncellemeleri yüklendi

### 💡 Önemli Not:

> "If you must verify that any of the preceding prerequisites have been completed, close the wizard, complete the steps, and then run the wizard again."

Önkoşullardan herhangi birinin tamamlandığını doğrulamanız gerekiyorsa, sihirbazı kapatın, adımları tamamlayın ve ardından sihirbazı tekrar çalıştırın.

**To continue, click Next.**

### Sol Menü Adımları:

1. **Before You Begin** ← (Mevcut adım)
2. Installation Type
3. Server Selection
4. Server Roles
5. Features
6. Confirmation
7. Results

### Seçenekler:

☐ **Skip this page by default**
- Bu sayfayı varsayılan olarak atla

### Butonlar:

- **< Previous**: Önceki adım (pasif)
- **Next >**: Sonraki adım
- **Install**: Kur (pasif)
- **Cancel**: İptal et

> ✅ Ön koşulların sağlandığından emin olduktan sonra **"Next >"** butonuna tıklayınız.

---

## Adım 3: Installation Type Seçimi

![Adım 3](Images/3.png)

Select installation type ekranında kurulum türü belirlenir.

### Üst Bilgi:

**DESTINATION SERVER**
**DOMAIN**

### Başlık:

**Select installation type**

### Açıklama:

> "Select the installation type. You can install roles and features on a running physical computer or virtual machine, or on an offline virtual hard disk (VHD)."

Kurulum türünü seçin. Rolleri ve özellikleri çalışan bir fiziksel bilgisayara, sanal makineye veya çevrimdışı sanal sabit diske (VHD) yükleyebilirsiniz.

### Kurulum Seçenekleri:

#### ☑ Role-based or feature-based installation

**Açıklama:**
> "Configure a single server by adding roles, role services, and features."

Tek bir sunucuyu roller, rol servisleri ve özellikler ekleyerek yapılandırın.

#### ☐ Remote Desktop Services installation

**Açıklama:**
> "Install required role services for Virtual Desktop Infrastructure (VDI) to create a virtual machine-based or session-based desktop deployment."

Virtual Desktop Infrastructure (VDI) için gerekli rol servislerini yükleyin; sanal makine tabanlı veya oturum tabanlı masaüstü dağıtımı oluşturun.

### Sol Menü Adımları:

1. Before You Begin
2. **Installation Type** ← (Mevcut adım)
3. Server Selection
4. Server Roles
5. Features
6. Confirmation
7. Results

### Butonlar:

- **< Previous**: Önceki adıma dön
- **Next >**: Sonraki adım
- **Install**: Kur (pasif)
- **Cancel**: İptal et

### 💡 Önerilen Seçim:

Active Directory Domain Services kurulumu için **"Role-based or feature-based installation"** seçeneği kullanılır.

> ✅ **"Role-based or feature-based installation"** seçeneğini işaretli bırakın ve **"Next >"** butonuna tıklayınız.

---

## Adım 4: Server Selection - Hedef Sunucu Seçimi

![Adım 4](Images/4.png)

Select destination server ekranında rollerin ve özelliklerin yükleneceği sunucu belirlenir.

### Üst Bilgi:

**DESTINATION SERVER**
**DOMAIN**

### Başlık:

**Select destination server**

### Açıklama:

> "Select a server or a virtual hard disk on which to install roles and features."

Roller ve özellikleri yüklemek için bir sunucu veya sanal sabit disk seçin.

### Seçim Türü:

#### ☑ Select a server from the server pool

Sunucu havuzundan bir sunucu seçin.

#### ☐ Select a virtual hard disk

Sanal sabit disk seçin.

### Server Pool (Sunucu Havuzu):

**Filter:** (Arama kutusu - boş)

#### Sunucu Listesi:

| Name | IP Address | Operating System |
|------|------------|------------------|
| **DOMAIN** | 192.168.31.100 | Microsoft Windows Server 2025 Standard Evaluation |

**1 Computer(s) found**

### 📋 Açıklama:

> "This page shows servers that are running Windows Server 2012 or a newer release of Windows Server, and that have been added by using the Add Servers command in Server Manager. Offline servers and newly-added servers from which data collection is still incomplete are not shown."

Bu sayfa, Windows Server 2012 veya daha yeni bir Windows Server sürümünü çalıştıran ve Server Manager'da Add Servers komutu kullanılarak eklenmiş sunucuları gösterir. Çevrimdışı sunucular ve veri toplama işlemi henüz tamamlanmamış yeni eklenen sunucular gösterilmez.

### Sol Menü Adımları:

1. Before You Begin
2. Installation Type
3. **Server Selection** ← (Mevcut adım)
4. Server Roles
5. Features
6. Confirmation
7. Results

### Butonlar:

- **< Previous**: Önceki adıma dön
- **Next >**: Sonraki adım
- **Install**: Kur (pasif)
- **Cancel**: İptal et

### 💡 Notlar:

Listede **DOMAIN** (192.168.31.100) sunucusu görünmektedir. Bu, Active Directory Domain Services'in kurulacağı hedef sunucudur.

> ✅ **DOMAIN** sunucusunun seçili olduğundan emin olun ve **"Next >"** butonuna tıklayınız.

---

## Adım 5: Server Roles - Active Directory Domain Services Seçimi

![Adım 5](Images/5.png)

Select server roles ekranında kurulacak roller seçilir. Bu görüntüde Active Directory Domain Services seçildiğinde açılan gerekli özellikler penceresi görülmektedir.

### Ana Ekran:

**DESTINATION SERVER**
**DOMAIN**

### Başlık:

**Select server roles**

### Açıklama:

> "Select one or more roles to install on the selected server."

Seçilen sunucuya yüklenecek bir veya daha fazla rol seçin.

### Roles Tablosu:

| Seçim | Rol | Açıklama |
|-------|-----|----------|
| ☐ | Active Directory Certificate Services | - |
| ☑ | **Active Directory Domain Services** | **Active Directory Domain Services (AD DS) stores information about objects on the network and makes this information available to users and network administrators. AD DS uses domain controllers to give network users access to permitted resources anywhere on the network through a single logon process.** |
| ☐ | Active Directory Federation Services | - |
| ☐ | Active Directory Lightweight Directory Services | - |
| ☐ | Active Directory Rights Management Services | - |
| ☐ | Device Health Attestation | - |

### 🔵 Pop-up Dialog Penceresi:

**Add Roles and Features Wizard**

#### Başlık:
**Add features that are required for Active Directory Domain Services?**

Active Directory Domain Services için gerekli özellikleri ekle?

#### Mesaj:

> "You cannot install Active Directory Domain Services unless the following role services or features are also installed."

Aşağıdaki rol servisleri veya özellikleri de yüklemedikçe Active Directory Domain Services'i yükleyemezsiniz.

#### Gerekli Özellikler Ağacı:

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

#### Seçenek:

☑ **Include management tools (if applicable)**

Yönetim araçlarını dahil et (uygunsa).

#### Pop-up Butonları:

- **Add Features**: Özellikleri ekle
- **Cancel**: İptal et

### Sol Menü Adımları:

1. Before You Begin
2. Installation Type
3. Server Selection
4. **Server Roles** ← (Mevcut adım)
5. Features
6. Confirmation
7. Results

### Ana Ekran Butonları:

- **< Previous**: Önceki adıma dön
- **Next >**: Sonraki adım (pop-up açıkken pasif)
- **Install**: Kur (pasif)
- **Cancel**: İptal et

### 📝 Açıklama:

Active Directory Domain Services rolü seçildiğinde, sistem otomatik olarak bu rol için gerekli olan ek özellikleri ve yönetim araçlarını tespit eder. Bu özellikler AD DS'nin tam işlevsellik kazanması için zorunludur.

### Gerekli Özellikler:

- **Group Policy Management**: Grup politikalarını yönetmek için
- **Remote Server Administration Tools**: Uzaktan yönetim araçları
- **AD DS and AD LDS Tools**: Active Directory yönetim araçları
- **Active Directory module for Windows PowerShell**: PowerShell yönetimi
- **Active Directory Administrative Center**: Grafik arayüzlü yönetim
- **AD DS Snap-Ins and Command-Line Tools**: Ek yönetim araçları

### 💡 Yapılacaklar:

1. Ana ekranda **Active Directory Domain Services** kutusunun işaretli olduğunu doğrulayın
2. Pop-up pencerede **"Include management tools (if applicable)"** kutusunun işaretli olduğunu kontrol edin
3. **"Add Features"** butonuna tıklayarak gerekli özellikleri ekleyin
4. Pop-up kapandıktan sonra ana ekranda **"Next >"** butonuna tıklayın

> ✅ **"Add Features"** butonuna tıklayınız.

---

## Adım 6: Installation Progress - Kurulum İlerlemesi

![Adım 6](Images/6.png)

Installation progress ekranı, seçilen rollerin ve özelliklerin kurulum ilerlemesini gösterir.

### Üst Bilgi:

**DESTINATION SERVER**
**DOMAIN**

### Başlık:

**Installation progress**

### İlerleme Durumu:

**View installation progress**

#### 🔵 Feature installation

**İlerleme Çubuğu:** (Mavi renkte, kurulum devam ediyor)

**Installation started on DOMAIN**

### 📦 Yüklenen Bileşenler:

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

### 🔗 Bağlantı:

**Export configuration settings**

Yapılandırma ayarlarını dışa aktarın.

### Sol Menü Adımları:

1. Before You Begin
2. Installation Type
3. Server Selection
4. Server Roles
5. Features
6. AD DS
7. Confirmation
8. **Results** ← (Mevcut adım)

### Butonlar:

- **< Previous**: Önceki adıma dön (pasif)
- **Next >**: Sonraki adım (pasif)
- **Close**: Kapat
- **Cancel**: İptal et (pasif)

### 📝 Notlar:

Kurulum aktif olarak devam etmektedir. İlerleme çubuğu, kurulumun ne kadarının tamamlandığını gösterir. Kurulum tamamlandığında başarı mesajı görüntülenecek ve "Close" butonu aktif hale gelecektir.

### ⏳ Bekleme Süresi:

Active Directory Domain Services ve ilgili bileşenlerin kurulumu genellikle 5-10 dakika sürer. Sunucu performansına göre bu süre değişebilir.

> ⏳ Kurulum tamamlanana kadar bekleyiniz. Kurulum bittiğinde "Close" butonuna tıklayarak sihirbazı kapatınız.

---

## Adım 7: Server Manager - Post-deployment Configuration

![Adım 7](Images/7.png)

Server Manager Dashboard ekranında, Active Directory Domain Services rolünün başarıyla yüklendiği ve yapılandırma gerektirdiği bildirilmektedir.

### Sağ Üst Köşe - Bildirimler:

#### ⚠️ Post-deployment Configuration (Sarı Uyarı İkonu)

**Configuration required for Active Directory Domain Services at DOMAIN**

Active Directory Domain Services için DOMAIN'de yapılandırma gerekiyor.

**Eylem Bağlantısı:**
**Promote this server to a domain controller**

Bu sunucuyu bir domain controller'a yükseltin.

---

#### ℹ️ Feature installation (Mavi Bilgi İkonu)

**TASKS** ▼ | **✕**

**Configuration required. Installation succeeded on DOMAIN.**

Yapılandırma gerekli. DOMAIN üzerinde kurulum başarılı oldu.

**Eylem Bağlantısı:**
**Add Roles and Features**

**Task Details**

### Ana Dashboard Alanı:

**WELCOME TO SERVER MANAGER**

#### Sol Panel:

**QUICK START** (Turuncu panel)
1️⃣ **Configure this local server**

**WHAT'S NEW** (Sarı panel)
2️⃣ **Add roles and features**
3️⃣ **Add other servers to manage**
4️⃣ **Create a server group**

### Sol Menü:

- 📊 **Dashboard** (Aktif - mavi vurgu)
- 💻 Local Server
- 📁 All Servers
- 📘 **AD DS** ← (Yeni eklendi! Active Directory Domain Services yüklendi)
- 📂 File and Storage Services

### 📝 Açıklama:

Active Directory Domain Services rolü başarıyla kurulmuştur ancak henüz yapılandırılmamıştır. Sunucu şu anda bir **member server** durumundadır ve **domain controller** haline gelmek için "promote" işlemi yapılması gerekmektedir.

### 🔄 Domain Controller Promotion Nedir?

Domain Controller Promotion işlemi şunları içerir:
- Yeni bir Active Directory forest (orman) oluşturma VEYA mevcut bir domain'e katılma
- DNS yapılandırması
- Active Directory veritabanı ve SYSVOL konumlarının belirlenmesi
- Directory Services Restore Mode (DSRM) şifresinin ayarlanması
- Global Catalog ve DNS sunucusu rollerinin etkinleştirilmesi

### 💡 Kritik Adım:

Bu noktada sunucu üzerinde AD DS rolü yüklü ancak pasif durumdadır. Sunucuyu aktif bir domain controller yapmak için yapılandırma gereklidir.

> ⚠️ **"Promote this server to a domain controller"** bağlantısına tıklayarak Active Directory yapılandırmasına başlayınız.

---

## Adım 8: Deployment Configuration - Yeni Forest Oluşturma

![Adım 8](Images/8.png)

Active Directory Domain Services Configuration Wizard'ın Deployment Configuration ekranıdır. Bu ekranda yeni bir forest oluşturulacak ve domain adı belirlenecektir.

### Üst Bilgi:

**TARGET SERVER**
**DOMAIN**

### Başlık:

**Deployment Configuration**

### ❌ Üst Kısım - Hata Mesajı (Kırmızı Banner):

> **"Verification of forest name failed. The DNS name "serifselen" proposed for this Active Directory domain con..."**

**Show more** | **✕**

⚠️ Bu hata, domain adının `.local` veya başka bir geçerli TLD uzantısı olmadan girilmesi durumunda oluşur.

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

Domain adının geçerli bir formatta olması gerekir:

**✅ Doğru formatlar:**
- `serifselen.local`
- `company.local`
- `organization.local`
- `domain.com`

**❌ Yanlış formatlar:**
- `serifselen` (uzantısız)
- `domain` (uzantısız)

### 🔗 Bağlantı:

**More about deployment configurations**

Dağıtım yapılandırmaları hakkında daha fazla bilgi.

### Sol Menü Adımları:

1. **Deployment Configuration** ← (Mevcut adım)
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

### 📝 Açıklama:

Bu ekranda yeni bir Active Directory forest'i oluşturulacaktır. "Add a new forest" seçeneği, tamamen yeni bir AD ortamı kurmak için kullanılır. Root domain name alanına girilen isim, forest'in kök domain'i olacaktır.

### ⚠️ Önemli Notlar:

1. **Domain adı** mutlaka `.local`, `.com`, `.net` gibi bir uzantı içermelidir
2. `.local` uzantısı, dahili/test ortamları için yaygın olarak kullanılır
3. Üretim ortamlarında, kuruluşunuza ait bir public domain kullanılabilir
4. Domain adı sonradan değiştirilemez, dikkatli seçilmelidir

> ✅ Root domain name alanına **`serifselen.local`** yazın ve **"Next >"** butonuna tıklayınız.

---

## Adım 9: Domain Controller Options - Fonksiyonel Seviye ve DSRM Şifresi

![Adım 9](Images/9.png)

Domain Controller Options ekranında forest ve domain fonksiyonel seviyeleri, domain controller yetenekleri ve DSRM şifresi belirlenir.

### Üst Bilgi:

**TARGET SERVER**
**DOMAIN**

### Başlık:

**Domain Controller Options**

### Select functional level of the new forest and root domain

Yeni forest ve root domain'in fonksiyonel seviyesini seçin:

#### Forest functional level:
```
Windows Server 2025 ▼
```

#### Domain functional level:
```
Windows Server 2025 ▼
```

### 📋 Fonksiyonel Seviye Nedir?

Fonksiyonel seviye, Active Directory'de kullanılabilecek özellikleri belirler. Daha yüksek seviyeler daha fazla özellik sunar ancak eski Windows Server sürümlerini desteklemez.

### Specify domain controller capabilities

Domain controller yeteneklerini belirtin:

#### ☑ Domain Name System (DNS) server

DNS sunucusu rolünü ekler. Active Directory için DNS zorunludur.

#### ☑ Global Catalog (GC)

Global Catalog sunucusu yeteneğini ekler. İlk domain controller her zaman GC olmalıdır.

#### ☐ Read only domain controller (RODC)

Salt okunur domain controller (Yeni forest'te kullanılamaz - gri/pasif).

### 🔐 Type the Directory Services Restore Mode (DSRM) password

Directory Services Restore Mode (DSRM) şifresini yazın:

#### Password:
```
••••••••
```

#### Confirm password:
```
••••••••
```

### 🔒 DSRM Şifresi Hakkında:

**DSRM (Directory Services Restore Mode)** şifresi:
- Active Directory veritabanını geri yüklemek için kullanılır
- Domain controller'ı özel restore modunda başlatmak için gereklidir
- Normal domain şifresinden farklıdır
- Acil durumlarda kritik öneme sahiptir

**Güvenlik Önerileri:**
- ✅ Güçlü ve karmaşık bir şifre seçin (en az 8 karakter)
- ✅ Büyük harf, küçük harf, rakam ve özel karakter içermeli
- ✅ Şifreyi güvenli bir yerde saklayın (şifre yöneticisi, güvenli kasa)
- ⚠️ Bu şifreyi unutmak ciddi sorunlara yol açabilir

### 🔗 Bağlantı:

**More about domain controller options**

Domain controller seçenekleri hakkında daha fazla bilgi.

### Sol Menü Adımları:

1. Deployment Configuration
2. **Domain Controller Options** ← (Mevcut adım)
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

### 💡 Yapılandırma Önerileri:

1. ✅ **Forest functional level**: Windows Server 2025 (en yüksek seviye)
2. ✅ **Domain functional level**: Windows Server 2025 (en yüksek seviye)
3. ✅ **DNS server**: İşaretli bırakın (zorunlu)
4. ✅ **Global Catalog**: İşaretli bırakın (ilk DC için zorunlu)
5. 🔐 **DSRM şifresi**: Güçlü bir şifre belirleyin ve kaydedin

### 📝 Notlar:

- İlk domain controller her zaman Global Catalog olmalıdır
- DNS sunucusu Active Directory için kritik öneme sahiptir
- RODC (Read-Only Domain Controller) yeni forest'te kullanılamaz
- Fonksiyonel seviyeleri sonradan yükseltilebilir ancak düşürülemez

> ✅ Tüm ayarları yapılandırdıktan ve güçlü bir DSRM şifresi belirledikten sonra **"Next >"** butonuna tıklayınız.

---

## Adım 10: Prerequisites Check - Son Kontrol ve Kurulum

![Adım 10](Images/10.png)

Active Directory Domain Services Configuration Wizard'ın Prerequisites Check (Ön Koşullar Kontrolü) ekranıdır. Bu ekran, kuruluma başlamadan önce tüm gereksinimlerin karşılandığını doğrular.

### Üst Bilgi:

**TARGET SERVER**
**DOMAIN**

### Başlık:

**Prerequisites Check**

### ✅ Üst Kısım - Başarı Mesajı (Yeşil Banner):

> ✅ **"All prerequisite checks passed successfully. Click 'Install' to begin installation."**

Tüm ön koşul kontrolleri başarıyla geçildi. Kuruluma başlamak için 'Install'a tıklayın.

**Show more** | **✕**

### Ana İçerik:

**Prerequisites need to be validated before Active Directory Domain Services is installed on this computer**

Ön koşulların bu bilgisayara Active Directory Domain Services yüklenmeden önce doğrulanması gerekiyor.

**Rerun prerequisites check**

Ön koşul kontrolünü yeniden çalıştır.

###