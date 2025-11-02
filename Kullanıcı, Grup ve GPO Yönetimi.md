# Active Directory ve DNS Kurulum Rehberi  
**Windows Server 2025 Üzerinde AD DS ve DNS Kurulumu**

Bu rehber, **Windows Server 2025 Standard Evaluation** sistemine **Active Directory Domain Services (AD DS)** ve **DNS Server** rollerinin nasıl kurulacağını adım adım açıklar. Kurulum, `Server Manager` aracılığıyla gerçekleştirilir.

---

## 📑 İçindekiler

- [Adım 1: Server Manager Ana Ekranı](#adım-1-server-manager-ana-ekranı)
- [Adım 2: "Add Roles and Features Wizard" Başlatma](#adım-2-add-roles-and-features-wizard-başlatma)
- [Adım 3: Kurulum Türü Seçimi](#adım-3-kurulum-türü-seçimi)
- [Adım 4: Hedef Sunucu Seçimi](#adım-4-hedef-sunucu-seçimi)
- [Adım 5: Active Directory Domain Services Rolü Seçimi](#adım-5-active-directory-domain-services-rolü-seçimi)
- [Adım 6: Deployment Configuration – Yeni Orman Oluşturma](#adım-6-deployment-configuration--yeni-orman-oluşturma)
- [Adım 7: Domain Controller Seçenekleri](#adım-7-domain-controller-seçenekleri)
- [Adım 8: Ön Koşul Denetimi](#adım-8-ön-koşul-denetimi)
- [Adım 9: Kurulum İlerleme Durumu](#adım-9-kurulum-ilerleme-durumu)
- [Adım 10: Post-deployment Yapılandırma Uyarısı](#adım-10-post-deployment-yapılandırma-uyarısı)
- [Active Directory Yönetimi](#active-directory-yönetimi)

---

## Adım 1: Server Manager Ana Ekranı

![Adım 1](Images/1.png)

`Server Manager` açıldığında sol üst köşede **"QUICK START"** bölümü görünür. Burada:

- **Configure this local server**
- **Add roles and features**
- **Add other servers to manage**

seçenekleri yer alır.

> ✅ AD DS kurulumuna başlamak için **"Add roles and features"** bağlantısına tıklayın.

---

## Adım 2: "Add Roles and Features Wizard" Başlatma

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

> ✅ **"Role-based or feature-based installation"** seçeneğini işaretleyin. Bu, sunucuya roller eklemek için kullanılır.  
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

**Server Roles** listesinden **"Active Directory Domain Services"** kutusunu işaretleyin.

Sistem, bu rol için gerekli yönetim araçlarını önerir:

- Group Policy Management
- AD DS and AD LDS Tools
- Active Directory Administrative Center
- AD DS Snap-Ins and Command-Line Tools

> ✅ **"Include management tools (if applicable)"** seçeneği otomatik işaretlenir.  
> Açılan pencerede **Add Features** butonuna tıklayıp **Next** butonuna geçin.

---

## Adım 6: Deployment Configuration – Yeni Orman Oluşturma

![Adım 6](Images/6.png)

AD DS kurulumu tamamlandıktan sonra **"Promote this server to a domain controller"** bağlantısıyla açılan sihirbazda:

- ☑ **Add a new forest** seçeneği işaretlenir  
- **Root domain name**: `serifselen.local` girilir

> ⚠️ Eğer **"Verification of forest name failed"** uyarısı alırsanız:
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

> ⚠️ "A delegation for this DNS server cannot be created…" uyarısı, mevcut bir DNS altyapısı yoksa **ihmal edilebilir**.  
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

Sunucu yeniden başladığında `Server Manager` dashboard'unda sağ üst köşede bir uyarı simgesi belirir:

> **Post-deployment Configuration**  
> Configuration required for Active Directory Domain Services at DOMAIN  
> **Promote this server to a domain controller**

> ✅ Bu uyarı, AD DS yapılandırmasının tamamlanmadığını gösterir.  
> Bağlantıya tıklayarak yapılandırmayı tamamlayabilir veya komut satırından `dcpromo` ile devam edebilirsiniz.

---

## 🎉 Kurulum Tamamlandı!

Sunucunuz artık **`serifselen.local`** etki alanında bir **Domain Controller** olarak çalışmaktadır. **DNS Server** hizmeti de otomatik olarak yapılandırılmıştır.

---

## 📂 Active Directory Yönetimi

Kurulumun tamamlanmasından sonra Active Directory ortamınızı yapılandırmak için aşağıdaki adımları takip edebilirsiniz.

---

## 📑 Kurulum Sonrası Yapılandırma İçindekiler

- [Adım 11: Windows Tools ve Active Directory Araçlarına Erişim](#adım-11-windows-tools-ve-active-directory-araçlarına-erişim)
- [Adım 12: Active Directory Users and Computers Arayüzü](#adım-12-active-directory-users-and-computers-arayüzü)
- [Adım 13: Yeni Öğe Oluşturma Menüsü](#adım-13-yeni-öğe-oluşturma-menüsü)
- [Adım 14: İlk Organizational Unit (OU) Oluşturma](#adım-14-i̇lk-organizational-unit-ou-oluşturma)
- [Adım 15: Alt Organizational Unit Oluşturma](#adım-15-alt-organizational-unit-oluşturma)
- [Adım 16: Detaylı OU Yapısı ve Departman Organizasyonu](#adım-16-detaylı-ou-yapısı-ve-departman-organizasyonu)
- [Adım 17: Güvenlik Grubu Oluşturma Menüsü](#adım-17-güvenlik-grubu-oluşturma-menüsü)
- [Adım 18: Yeni Güvenlik Grubu Özellikleri](#adım-18-yeni-güvenlik-grubu-özellikleri)
- [Adım 19: Grup Özelliklerini Düzenleme](#adım-19-grup-özelliklerini-düzenleme)
- [Adım 20: Kullanıcı Hesabı Oluşturma - Kişisel Bilgiler](#adım-20-kullanıcı-hesabı-oluşturma---kişisel-bilgiler)
- [Adım 21: Kullanıcı Hesabı - Şifre Ayarları](#adım-21-kullanıcı-hesabı---şifre-ayarları)
- [Adım 22: Gruba Üye Ekleme](#adım-22-gruba-üye-ekleme)
- [Adım 23: Kullanıcı Seçimi ve Doğrulama](#adım-23-kullanıcı-seçimi-ve-doğrulama)
- [Adım 24: Group Policy Management Konsolu](#adım-24-group-policy-management-konsolu)

---

## Adım 11: Windows Tools ve Active Directory Araçlarına Erişim

![Adım 11](Images/11.png)

Active Directory yönetim araçlarına erişmek için **Windows Tools** klasörünü kullanın.

### Erişim Yöntemleri:

**Yöntem 1: Başlat Menüsü**
1. **Start** menüsüne tıklayın
2. **Windows Tools** yazın
3. Açılan klasörde aşağıdaki araçlar bulunur:
   - **Active Directory Administrative Center**
   - **Active Directory Domains and Trusts**
   - **Active Directory Module for Windows PowerShell**
   - **Active Directory Sites and Services**
   - **Active Directory Users and Computers** ← Yaygın kullanılan

**Yöntem 2: Doğrudan Run Komutları**

| Araç | Run Komutu |
|------|-----------|
| Active Directory Users and Computers | `dsa.msc` |
| Active Directory Sites and Services | `dssite.msc` |
| Active Directory Domains and Trusts | `domain.msc` |
| Group Policy Management | `gpmc.msc` |

**Yöntem 3: Server Manager**
- **Server Manager** > **Tools** menüsünden erişim

> ✅ **Active Directory Users and Computers** seçeneğine tıklayarak devam edin.

---

## Adım 12: Active Directory Users and Computers Arayüzü

![Adım 12](Images/12.png)

**Active Directory Users and Computers (ADUC)** konsolu açıldığında varsayılan yapı görüntülenir.

### Sol Panel - Domain Yapısı:
```
📁 Active Directory Users and Computers
  📁 Saved Queries
  📁 serifselen.local
    📁 Builtin
    📁 Computers
    📁 Domain Controllers
    📁 ForeignSecurityPrincipals
    📁 Managed Service Accounts
    📁 Users
```

### Sağ Panel - Container İçeriği:

| Name | Type | Description |
|------|------|-------------|
| 📁 Builtin | builtinDomain | Default container for up... |
| 📁 Computers | Container | Default container for up... |
| 📁 Domain Controllers | Organizational... | Default container for do... |
| 📁 ForeignSecurityPrincipals | Container | Default container for sec... |
| 📁 Managed Service Accounts | Container | Default container for ma... |
| 📁 Users | Container | Default container for up... |

> 💡 Bu varsayılan container'lar silinemez ve taşınamaz. Yeni organizasyon yapısı için **Organizational Unit (OU)** oluşturmanız önerilir.

---

## Adım 13: Yeni Öğe Oluşturma Menüsü

![Adım 13](Images/13.png)

Domain üzerine sağ tıklayarak yeni nesneler oluşturabilirsiniz.

### Sağ Tıklama Menüsü - New (Yeni) Alt Menüsü:

| İkon | Nesne Tipi | Açıklama |
|------|-----------|----------|
| 💻 | **Computer** | Bilgisayar hesabı |
| 👤 | **Contact** | İletişim nesnesi |
| 👥 | **Group** | Güvenlik veya dağıtım grubu |
| 👤 | **InetOrgPerson** | İnternet organizasyon kişisi |
| 📂 | **Organizational Unit** | **← Organizasyon birimi** |
| 🖨️ | **Printer** | Yazıcı nesnesi |
| 👤 | **User** | Kullanıcı hesabı |
| 📁 | **Shared Folder** | Paylaşılan klasör |

> ✅ Yeni bir organizasyon yapısı oluşturmak için **New > Organizational Unit** seçeneğini kullanın.

---

## Adım 14: İlk Organizational Unit (OU) Oluşturma

![Adım 14](Images/14.png)

İlk seviye OU oluşturarak organizasyon yapınızın temelini atın.

### New Object - Organizational Unit Penceresi:

📁 **Create in:** `serifselen.local/`

**Name:** 
```
Selen Holding
```

☑ **Protect container from accidental deletion**

### 🔒 Önemli Güvenlik Özelliği:

**"Protect container from accidental deletion"** seçeneği:
- OU'nun yanlışlıkla silinmesini önler
- Active Directory'de Object Protection özelliğini aktifleştirir
- **Üretim ortamlarında mutlaka işaretlenmelidir**

> ✅ OU adını girin, koruma seçeneğini işaretleyin ve **OK** butonuna tıklayın.

---

## Adım 15: Alt Organizational Unit Oluşturma

![Adım 15](Images/15.png)

Ana OU altında alt OU'lar oluşturarak hiyerarşik yapı kurun.

### New Object - Organizational Unit Penceresi:

📁 **Create in:** `serifselen.local/Selen Holding`

**Name:** 
```
Ankara
```

☑ **Protect container from accidental deletion**

### 🗂️ Hiyerarşik Yapı Mantığı:
```
Şirket (Selen Holding)
  └── Lokasyon (Ankara, Istanbul, İzmir)
      └── Departman (IT, Finance, HR)
          └── Kaynak Tipi (Users, Computers, Groups)
```

> ✅ Alt OU adını girin ve **OK** butonuna tıklayın. Aynı yöntemi kullanarak `Istanbul` ve `Izmir` OU'larını da oluşturun.

---

## Adım 16: Detaylı OU Yapısı ve Departman Organizasyonu

![Adım 16](Images/16.png)

Tam bir organizasyon yapısı oluşturduktan sonra ADUC şu şekilde görünür:

### Sol Panel - Tam OU Ağacı:
```
📁 serifselen.local
  📁 Selen Holding
    📁 Ankara
      📁 Istanbul
        📁 Computers
        📁 Groups
        📁 Servers
        📁 Users
          📁 Finance
          📁 HR
          📁 IT
    📁 Izmir
```

### 📊 Önerilen OU Yapısı:

#### Seviye 1: Şirket/Organizasyon
```
Selen Holding
```

#### Seviye 2: Lokasyon
```
├── Ankara
├── Istanbul
└── Izmir
```

#### Seviye 3: Kaynak Tipi
```
Istanbul/
├── Computers
├── Servers
├── Users
└── Groups
```

#### Seviye 4: Departman
```
Istanbul/Users/
├── Finance
├── HR
└── IT
```

---

## Adım 17: Güvenlik Grubu Oluşturma Menüsü

![Adım 17](Images/17.png)

Kullanıcıları gruplandırmak ve izin yönetimini kolaylaştırmak için güvenlik grubu oluşturun.

### Sağ Tıklama Menüsü:

`Istanbul/Users/Finance` klasörü üzerine sağ tıklayın:

- **New >**
  - **Group** ← **Seçilecek**
  - User
  - Contact
  - Computer
  - Organizational Unit
  - ...

> ✅ **New > Group** seçeneğine tıklayın.

---

## Adım 18: Yeni Güvenlik Grubu Özellikleri

![Adım 18](Images/18.png)

Grup oluşturma penceresinde gerekli bilgileri doldurun.

### New Object - Group Penceresi:

👥 **Create in:** `serifselen.local/Selen Holding/Istanbul/Groups`

**Group name:**
```
Finance
```

**Group name (pre-Windows 2000):**
```
Finance
```

### Group scope (Grup Kapsamı):

- ⚪ **Domain local**
- 🔘 **Global** ← Önerilen
- ⚪ **Universal**

### Group type (Grup Tipi):

- 🔘 **Security** ← Önerilen
- ⚪ **Distribution**

### 📚 Grup Kapsamları Detaylı Açıklama:

| Kapsam | Üyeler | Kullanılabileceği Yer | Kullanım Amacı |
|--------|--------|----------------------|----------------|
| **Domain Local** | Herhangi bir domain'den | Sadece kendi domain'inde | Kaynaklara izin vermek |
| **Global** | Sadece kendi domain'inden | Herhangi bir domain'de | Kullanıcıları gruplamak |
| **Universal** | Herhangi bir domain'den | Herhangi bir domain'de | Multi-domain ortamlar |

> ✅ Grup bilgilerini doldurun ve **OK** butonuna tıklayın.

---

## Adım 19: Grup Özelliklerini Düzenleme

![Adım 19](Images/19.png)

Oluşturulan grubun özelliklerini görüntülemek ve düzenlemek için çift tıklayın.

### Finance Properties Penceresi:

#### Sekmeler:
- **General** ← Aktif sekme
- Members
- Member Of
- Managed By

### General Sekmesi:

**Group name (pre-Windows 2000):** `Finance`

**Description:** `Finance`

**E-mail:** `finance@serifselen.local`

### Group scope:
- 🔘 **Global**

### Group type:
- 🔘 **Security**

**Notes:** (Özel notlar için alan)

> 💡 **Members** sekmesinden gruba üye ekleyebilirsiniz.

---

## Adım 20: Kullanıcı Hesabı Oluşturma - Kişisel Bilgiler

![Adım 20](Images/20.png)

Yeni kullanıcı hesabı oluştururken kişisel bilgileri ve oturum açma bilgilerini girin.

### New Object - User Penceresi (1. Sayfa):

👤 **Create in:** `selen.local/Selen Holding/Istanbul/Users/Finance`

### Kişisel Bilgiler:

**First name:** `Serif`

**Last name:** `SELEN`

**Full name:** `Serif SELEN`

### Oturum Açma Bilgileri:

**User logon name:** `serifselen` @ `serifselen.local`

**User logon name (pre-Windows 2000):** `SERIFSELEN\serifselen`

### 📝 İsimlendirme Standartları:

| Format | Örnek | Kullanım |
|--------|-------|----------|
| firstname.lastname | serif.selen | Yaygın kurumsal standart |
| firstnamelastname | serifselen | Kısa ve basit |
| flastname | sselen | Büyük organizasyonlar |

> ✅ Kullanıcı bilgilerini doldurun ve **Next >** butonuna tıklayın.

---

## Adım 21: Kullanıcı Hesabı - Şifre Ayarları

![Adım 21](Images/21.png)

Kullanıcı hesabı için şifre ve şifre politikası seçeneklerini belirleyin.

### New Object - User Penceresi (2. Sayfa):

**Password:** `••••••••`

**Confirm password:** `••••••••`

### Şifre Seçenekleri:

- ☐ **User must change password at next logon**
- ☐ **User cannot change password**
- ☐ **Password never expires**
- ☐ **Account is disabled**

### 🔐 Şifre Seçenekleri Rehberi:

| Seçenek | Ne Zaman İşaretlenir? | Örnek Senaryo |
|---------|----------------------|---------------|
| **Must change at next logon** | Normal kullanıcılar için (ÖNERİLİR) | Yeni işe başlayan personel |
| **Cannot change password** | Servis hesapları | SQL Server service account |
| **Password never expires** | Kritik servis hesapları | Backup service account |
| **Account is disabled** | Geçici devre dışı | Tatildeki personel |

### Güçlü Şifre Gereksinimleri:

- En az **7 karakter** (önerilen: 12+)
- **3 karakter kategorisinden** karakter içermeli:
  - Büyük harfler (A-Z)
  - Küçük harfler (a-z)
  - Rakamlar (0-9)
  - Özel karakterler (!@#$%^&*)

> ✅ Şifre ve seçenekleri belirleyin, ardından **Next >** butonuna tıklayın.

---

## Adım 22: Gruba Üye Ekleme

![Adım 22](Images/22.png)

Oluşturulan kullanıcıyı ilgili güvenlik grubuna ekleyin.

### Finance Properties - Members Sekmesi:

**Members** sekmesine gidin.

**Members:** (Boş liste - henüz üye yok)

> 💡 Gruba kullanıcı eklemek için **Add...** butonuna tıklayın.

---

## Adım 23: Kullanıcı Seçimi ve Doğrulama

![Adım 23](Images/23.png)

Gruba eklenecek kullanıcıları seçin ve doğrulayın.

### Select Users, Contacts, Computers, Service Accounts, or Groups:

**From this location:** `serifselen.local`

**Enter the object names to select:**
```
serifselen
```

**Check Names** ← İsmi doğrula

### 💡 Check Names Fonksiyonu:

- Girilen isim Active Directory'de aranır
- Bulunursa altı çizili olarak görünür
- Doğru kullanıcı seçildiğinden emin olunur

> ✅ İsmi girin, **Check Names** ile doğrulayın ve **OK** butonuna tıklayın.

---

## Adım 24: Group Policy Management Konsolu

![Adım 24](Images/24.png)

Group Policy Management (GPM) konsolu, GPO'ları merkezi olarak yönetmenizi sağlar.

### Group Policy Management Yapısı:
```
📁 Group Policy Management
  📁 Forest: serifselen.local
    📁 Domains
      📁 serifselen.local
        📋 Default Domain Policy
        📋 Default Domain Controllers Policy
        📁 Group Policy Objects
          📋 New Group Policy Object
```

### Yeni GPO Oluşturma:

1. **Group Policy Objects** üzerine sağ tıklayın
2. **New** seçeneğine tıklayın
3. GPO adını girin
4. **OK** butonuna tıklayın

### 📋 Group Policy Object (GPO) Türleri:

**Computer Configuration:**
- Bilgisayar bazlı ayarlar
- Güvenlik duvarı kuralları
- Yazılım kurulumu
- Sistem ayarları

**User Configuration:**
- Kullanıcı bazlı ayarlar
- Masaüstü arka planı
- Drive mapping
- Uygulama ayarları

---

## 🔧 Kurulum Sonrası Öneriler

### 1. Kullanıcı ve Grup Yönetimi
- Active Directory Users and Computers (ADUC) üzerinden ilk kullanıcıları oluşturun
- Departman bazlı güvenlik grupları oluşturun
- AGDLP stratejisini uygulayın

### 2. Grup İlkesi (GPO) Yapılandırması
- Şifre politikaları tanımlayın
- Güvenlik ayarlarını yapılandırın
- Kullanıcı ortamını standartlaştırın

### 3. Diğer Sunucuları Etki Alanına Katma
- Üye sunucuları `serifselen.local` etki alanına ekleyin
- Bilgisayar hesaplarını ilgili OU'lara taşıyın

### 4. Yedekleme ve Kurtarma Planı
- System State yedeklemesi yapın
- AD Recycle Bin'i etkinleştirin
- Düzenli yedekleme stratejisi oluşturun

### 5. Güvenlik Duvarı ve Ağ İzolasyonu
- Gerekli portları açın (TCP 53, 88, 389, 445, 3268, 3269)
- Güvenlik duvarı kurallarını yapılandırın

---

## 💡 En İyi Uygulamalar

### OU Yapısı:
- Coğrafi ve departman bazlı hiyerarşi oluşturun
- "Protect from accidental deletion" seçeneğini aktif edin
- Açıklayıcı ve standart isimler kullanın

### Grup Yönetimi:
- AGDLP stratejisini uygulayın
- Tutarlı isimlendirme kullanın
- Security Groups kullanın (Distribution Groups değil)

### Kullanıcı Hesapları:
- İlk oturumda şifre değişikliği zorunlu tutun
- Karmaşık şifre gereksinimleri tanımlayın
- Standart bir isimlendirme formatı belirleyin

### GPO Yönetimi:
- Her GPO'nun tek bir amacı olmalı
- Açıklayıcı isimler kullanın
- Test ortamında deneyin

---

## 🔧 Yaygın PowerShell Komutları

### Kullanıcı İşlemleri:
```powershell
# Kullanıcı oluşturma
New-ADUser -Name "Serif SELEN" -GivenName "Serif" -Surname "SELEN" -SamAccountName "serifselen" -UserPrincipalName "serifselen@serifselen.local" -Path "OU=Finance,OU=Users,OU=Istanbul,OU=Selen Holding,DC=serifselen,DC=local" -AccountPassword (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force) -Enabled $true

# Kullanıcıyı gruba ekleme
Add-ADGroupMember -Identity "Finance" -Members serifselen

# Kullanıcı bilgilerini görüntüleme
Get-ADUser -Identity serifselen -Properties *
```

### Grup İşlemleri:
```powershell
# Grup oluşturma
New-ADGroup -Name "Finance" -GroupScope Global -GroupCategory Security -Path "OU=Groups,OU=Istanbul,OU