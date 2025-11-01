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

<<<<<<< HEAD
**Before you continue, verify that the following tasks have been completed:**

Devam etmeden önce, aşağıdaki görevlerin tamamlandığını doğrulayın:

- **• The Administrator account has a strong password**
  - Yönetici hesabının güçlü bir şifresi var

- **• Network settings, such as static IP addresses, are configured**
  - Statik IP adresleri gibi ağ ayarları yapılandırıldı

- **• The most current security updates from Windows Update are installed**
=======
Aşağıdaki görevlerin tamamlandığını doğrulayın:

- ✅ **The Administrator account has a strong password**
  - Yönetici hesabının güçlü bir şifresi var

- ✅ **Network settings, such as static IP addresses, are configured**
  - Statik IP adresleri gibi ağ ayarları yapılandırıldı

- ✅ **The most current security updates from Windows Update are installed**
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596
  - Windows Update'ten en güncel güvenlik güncellemeleri yüklendi

### 💡 Önemli Not:

> "If you must verify that any of the preceding prerequisites have been completed, close the wizard, complete the steps, and then run the wizard again."

Önkoşullardan herhangi birinin tamamlandığını doğrulamanız gerekiyorsa, sihirbazı kapatın, adımları tamamlayın ve ardından sihirbazı tekrar çalıştırın.

<<<<<<< HEAD
**To continue, click Next.**

### Sol Menü Adımları:

1. **Before You Begin** ← (Mevcut adım)
=======
### Ek Bilgi:

"To continue, click Next."

### Sol Menü Adımları:

1. **Before You Begin** (Mevcut adım)
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596
2. Installation Type
3. Server Selection
4. Server Roles
5. Features
6. Confirmation
7. Results

### Seçenekler:

☐ **Skip this page by default**
<<<<<<< HEAD
- Bu sayfayı varsayılan olarak atla
=======
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

### Butonlar:

- **< Previous**: Önceki adım (pasif)
- **Next >**: Sonraki adım
- **Install**: Kur (pasif)
- **Cancel**: İptal et

<<<<<<< HEAD
> ✅ Ön koşulların sağlandığından emin olduktan sonra **"Next >"** butonuna tıklayınız.
=======
**"Next >"** butonuna tıklayarak devam ediniz.
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

---

## Adım 3: Installation Type Seçimi

![Adım 3](Images/3.png)

Select installation type ekranında kurulum türü belirlenir.

<<<<<<< HEAD
### Üst Bilgi:

**DESTINATION SERVER**
**DOMAIN**

### Başlık:

**Select installation type**

### Açıklama:

> "Select the installation type. You can install roles and features on a running physical computer or virtual machine, or on an offline virtual hard disk (VHD)."

Kurulum türünü seçin. Rolleri ve özellikleri çalışan bir fiziksel bilgisayara, sanal makineye veya çevrimdışı sanal sabit diske (VHD) yükleyebilirsiniz.

### Kurulum Seçenekleri:
=======
### Installation Type Seçenekleri:
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

#### ☑ Role-based or feature-based installation

**Açıklama:**
<<<<<<< HEAD
> "Configure a single server by adding roles, role services, and features."

Tek bir sunucuyu roller, rol servisleri ve özellikler ekleyerek yapılandırın.
=======
- Tek bir sunucuyu roller, rol servisleri ve özellikler ekleyerek yapılandırın
- Configure a single server by adding roles, role services, and features
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

#### ☐ Remote Desktop Services installation

**Açıklama:**
<<<<<<< HEAD
> "Install required role services for Virtual Desktop Infrastructure (VDI) to create a virtual machine-based or session-based desktop deployment."

Virtual Desktop Infrastructure (VDI) için gerekli rol servislerini yükleyin; sanal makine tabanlı veya oturum tabanlı masaüstü dağıtımı oluşturun.
=======
- Virtual Desktop Infrastructure (VDI) için gerekli rol servislerini yükleyin
- Sanal makine tabanlı veya oturum tabanlı masaüstü dağıtımı oluşturun
- Install required role services for Virtual Desktop Infrastructure (VDI) to create a virtual machine-based or session-based desktop deployment
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

### Sol Menü Adımları:

1. Before You Begin
<<<<<<< HEAD
2. **Installation Type** ← (Mevcut adım)
=======
2. **Installation Type** (Mevcut adım)
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596
3. Server Selection
4. Server Roles
5. Features
6. Confirmation
7. Results

<<<<<<< HEAD
=======
### Önerilen Seçim:

> ✅ **Role-based or feature-based installation** seçeneğini işaretleyiniz.

>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596
### Butonlar:

- **< Previous**: Önceki adıma dön
- **Next >**: Sonraki adım
- **Install**: Kur (pasif)
- **Cancel**: İptal et

<<<<<<< HEAD
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
=======
**"Next >"** butonuna tıklayarak devam ediniz.

---

## Adım 4: Hedef Sunucu Seçimi

![Adım 4](Images/4.png)

Select destination server ekranında roller ve özelliklerin yükleneceği sunucu veya sanal sabit disk seçilir.

### Seçenekler:
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

#### ☑ Select a server from the server pool

Sunucu havuzundan bir sunucu seçin.

#### ☐ Select a virtual hard disk

Sanal sabit disk seçin.

<<<<<<< HEAD
### Server Pool (Sunucu Havuzu):

**Filter:** (Arama kutusu - boş)

#### Sunucu Listesi:
=======
### Server Pool

Sunucu listesi aşağıdaki bilgileri içermektedir:
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

| Name | IP Address | Operating System |
|------|------------|------------------|
| **DOMAIN** | 192.168.31.100 | Microsoft Windows Server 2025 Standard Evaluation |

**1 Computer(s) found**

<<<<<<< HEAD
### 📋 Açıklama:
=======
### 💡 Önemli Bilgi:
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

> "This page shows servers that are running Windows Server 2012 or a newer release of Windows Server, and that have been added by using the Add Servers command in Server Manager. Offline servers and newly-added servers from which data collection is still incomplete are not shown."

Bu sayfa, Windows Server 2012 veya daha yeni bir Windows Server sürümünü çalıştıran ve Server Manager'da Add Servers komutu kullanılarak eklenmiş sunucuları gösterir. Çevrimdışı sunucular ve veri toplama işlemi henüz tamamlanmamış yeni eklenen sunucular gösterilmez.

### Sol Menü Adımları:

1. Before You Begin
2. Installation Type
<<<<<<< HEAD
3. **Server Selection** ← (Mevcut adım)
=======
3. **Server Selection** (Mevcut adım)
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596
4. Server Roles
5. Features
6. Confirmation
7. Results

### Butonlar:

- **< Previous**: Önceki adıma dön
- **Next >**: Sonraki adım
- **Install**: Kur (pasif)
- **Cancel**: İptal et

<<<<<<< HEAD
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
=======
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
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

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

<<<<<<< HEAD
#### Seçenek:

☑ **Include management tools (if applicable)**

Yönetim araçlarını dahil et (uygunsa).

#### Pop-up Butonları:
=======
### Seçenekler:

☑ **Include management tools (if applicable)**

Yönetim araçları (varsa) dahil edilsin.

### Pop-up Butonları:
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

- **Add Features**: Özellikleri ekle
- **Cancel**: İptal et

### Sol Menü Adımları:

1. Before You Begin
2. Installation Type
3. Server Selection
<<<<<<< HEAD
4. **Server Roles** ← (Mevcut adım)
=======
4. **Server Roles** (Mevcut adım)
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596
5. Features
6. Confirmation
7. Results

<<<<<<< HEAD
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
=======
### Yapılacaklar:

1. **Active Directory Domain Services** kutusunu işaretleyiniz
2. Açılan pop-up'ta **"Add Features"** butonuna tıklayınız
3. Ana ekranda **"Next >"** butonuna tıklayarak devam ediniz

---

## Adım 6: Features Kurulum ve İlerleme
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

![Adım 6](Images/6.png)

Installation progress ekranı, seçilen rollerin ve özelliklerin kurulum ilerlemesini gösterir.

<<<<<<< HEAD
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
=======
### View installation progress

#### 🔵 Feature installation

**İlerleme Çubuğu:** Kurulum devam ediyor

**Installation started on DOMAIN**

### Yüklenen Bileşenler:
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

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

<<<<<<< HEAD
### 🔗 Bağlantı:

**Export configuration settings**

Yapılandırma ayarlarını dışa aktarın.
=======
### Ek Seçenek:

**Export configuration settings** - Yapılandırma ayarlarını dışa aktar
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

### Sol Menü Adımları:

1. Before You Begin
2. Installation Type
3. Server Selection
4. Server Roles
5. Features
6. AD DS
7. Confirmation
<<<<<<< HEAD
8. **Results** ← (Mevcut adım)
=======
8. **Results** (Mevcut adım)
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

### Butonlar:

- **< Previous**: Önceki adıma dön (pasif)
- **Next >**: Sonraki adım (pasif)
- **Close**: Kapat
- **Cancel**: İptal et (pasif)

<<<<<<< HEAD
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
=======
> ⏳ Kurulum tamamlanana kadar bekleyiniz. Kurulum başarıyla tamamlandığında bir sonraki adıma geçebilirsiniz.

---

## Adım 7: Post-deployment Configuration

![Adım 7](Images/7.png)

Server Manager Dashboard ekranında kurulum sonrası yapılandırma bildirimi görüntülenmektedir.

### Bildirimler:

#### ⚠️ Post-deployment Configuration

**Configuration required for Active Directory Domain Services at DOMAIN**

**Bağlantı:**
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596
**Promote this server to a domain controller**

Bu sunucuyu bir domain controller'a yükseltin.

<<<<<<< HEAD
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
=======
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
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

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

<<<<<<< HEAD
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
=======
> Domain adının `.local` uzantısıyla bitmesi önerilir. Bu, yerel ağ domain'leri için standart bir uygulamadır.

**Örnek doğru formatlar:**
- `serifselen.local`
- `company.local`
- `organization.local`

### Bağlantı:

**More about deployment configurations** - Dağıtım yapılandırmaları hakkında daha fazla bilgi

### Sol Menü Adımları:

1. **Deployment Configuration** (Mevcut adım)
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596
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

<<<<<<< HEAD
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

=======
### ⚠️ Önemli Not:

Hata mesajı görünüyorsa, root domain name'i kontrol ediniz. Doğru format: `serifselen.local`

**"Next >"** butonuna tıklayarak devam ediniz.

---

## Adım 9: Domain Controller Options

![Adım 9](Images/9.png)

Domain Controller Options ekranında yeni forest ve root domain için fonksiyonel seviye ve domain controller özellikleri belirlenir.

### Select functional level of the new forest and root domain

>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596
#### Forest functional level:
```
Windows Server 2025 ▼
```

#### Domain functional level:
```
Windows Server 2025 ▼
```

<<<<<<< HEAD
### 📋 Fonksiyonel Seviye Nedir?

Fonksiyonel seviye, Active Directory'de kullanılabilecek özellikleri belirler. Daha yüksek seviyeler daha fazla özellik sunar ancak eski Windows Server sürümlerini desteklemez.

=======
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596
### Specify domain controller capabilities

Domain controller yeteneklerini belirtin:

#### ☑ Domain Name System (DNS) server

<<<<<<< HEAD
DNS sunucusu rolünü ekler. Active Directory için DNS zorunludur.

#### ☑ Global Catalog (GC)

Global Catalog sunucusu yeteneğini ekler. İlk domain controller her zaman GC olmalıdır.

#### ☐ Read only domain controller (RODC)

Salt okunur domain controller (Yeni forest'te kullanılamaz - gri/pasif).

### 🔐 Type the Directory Services Restore Mode (DSRM) password

Directory Services Restore Mode (DSRM) şifresini yazın:
=======
DNS sunucusu yeteneği ekler.

#### ☑ Global Catalog (GC)

Global Catalog sunucusu yeteneği ekler.

#### ☐ Read only domain controller (RODC)

Salt okunur domain controller (pasif - yeni forest'te kullanılamaz).

### Type the Directory Services Restore Mode (DSRM) password

DSRM şifresi, Active Directory'yi geri yükleme modunda başlatırken kullanılır.
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

#### Password:
```
••••••••
```

#### Confirm password:
```
••••••••
```

### 🔒 DSRM Şifresi Hakkında:

<<<<<<< HEAD
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
=======
> **Directory Services Restore Mode (DSRM)** şifresi:
> - Active Directory veritabanını geri yüklemek için kullanılır
> - Acil durumlarda domain controller'ı özel modda başlatır
> - Güçlü ve unutulmayacak bir şifre seçiniz
> - Bu şifreyi güvenli bir yerde saklayınız

### Bağlantı:

**More about domain controller options** - Domain controller seçenekleri hakkında daha fazla bilgi
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596

### Sol Menü Adımları:

1. Deployment Configuration
<<<<<<< HEAD
2. **Domain Controller Options** ← (Mevcut adım)
=======
2. **Domain Controller Options** (Mevcut adım)
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596
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

<<<<<<< HEAD
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
=======
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
>>>>>>> a49ac8631698e37bf5aad058f2519b2bfaae1596
