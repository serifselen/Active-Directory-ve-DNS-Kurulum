# Active Directory ve DNS Kurulum Rehberi  
## Windows Server 2025 Üzerinde AD DS ve DNS Kurulumu

Bu rehber, Windows Server 2025 Standard Evaluation sistemine Active Directory Domain Services (AD DS) ve DNS Server rollerinin nasıl kurulacağını adım adım açıklar. Kurulum, Server Manager aracılığıyla gerçekleştirilir.

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
- [Active Directory Yönetim İşlemleri](#active-directory-yönetim-i̇şlemleri)
  - [Adım 11: Windows Tools ve Active Directory Araçlarına Erişim](#adım-11-windows-tools-ve-active-directory-araçlarına-erişim)
  - [Adım 12: Active Directory Users and Computers Arayüzü](#adım-12-active-directory-users-and-computers-arayüzü)
  - [Adım 13: Yeni Nesne Oluşturma Menüsü](#adım-13-yeni-nose-oluşturma-menüsü)
  - [Adım 14: İlk Organizational Unit (OU) Oluşturma](#adım-14-i̇lk-organizational-unit-ou-oluşturma)
  - [Adım 15: Alt Organizational Unit Oluşturma](#adım-15-alt-organizational-unit-oluşturma)
  - [Adım 16: OU Hiyerarşisi ve Yapılandırması](#adım-16-ou-hiyerarşisi-ve-yapılandırması)
  - [Adım 17: Güvenlik Grubu Oluşturma](#adım-17-güvenlik-grubu-oluşturma)
  - [Adım 18: Kullanıcı Hesabı Oluşturma](#adım-18-kullanıcı-hesabı-oluşturma)
  - [Adım 19: Gruba Üye Ekleme](#adım-19-gruba-üye-ekleme)
  - [Adım 20: Group Policy Yönetim Konsolu](#adım-20-group-policy-yönetim-konsolu)
  - [Adım 21: Yeni Grup İlkesi (GPO) Oluşturma](#adım-21-yeni-grup-i̇lkesi-gpo-oluşturma)
  - [Adım 22: GPO Ayarlarının Yapılandırılması](#adım-22-gpo-ayarlarının-yapılandırılması)
  - [Adım 23: GPO'nun OU'ya Bağlanması](#adım-23-gponun-ouya-bağlanması)
  - [Adım 24: Delegated Administration Yapılandırması](#adım-24-delegated-administration-yapılandırması)
- [Kurulum Sonrası Öneriler](#kurulum-sonrası-öneriler)
- [En İyi Uygulamalar (Best Practices)](#en-i̇yi-uygulamalar-best-practices)
- [Yaygın PowerShell Komutları](#yaygın-powershell-komutları)
- [Doküman Bilgileri](#doküman-bilgileri)

---

## 🖥️ AD DS Kurulum Adımları

### Adım 1: Server Manager Ana Ekranı

![Adım 1](Images/1.png)

Server Manager açıldığında sol üst köşede **"QUICK START"** bölümü görünür. Bu bölümde:
- **Configure this local server**
- **Add roles and features**
- **Add other servers to manage**

seçenekleri yer alır.

✅ AD DS kurulumuna başlamak için **"Add roles and features"** bağlantısına tıklayın.

---

### Adım 10: Post-deployment Yapılandırma Uyarısı

![Adım 10](Images/10.png)

Sunucu yeniden başladığında Server Manager dashboard'unda sağ üst köşede bir uyarı simgesi belirir:

> **Post-deployment Configuration**  
> Configuration required for Active Directory Domain Services at DOMAIN  
> **Promote this server to a domain controller**

✅ Bu uyarı, AD DS yapılandırmasının tamamlanmadığını gösterir.  
Bağlantıya tıklayarak yapılandırmayı tamamlayabilir veya komut satırından aşağıdaki komutu çalıştırabilirsiniz:

```powershell
Install-ADDSDomainController -DomainName "serifselen.local" -SafeModeAdministratorPassword (Read-Host -Prompt "DSRM Password" -AsSecureString)
```

---

## 🎉 Kurulum Tamamlandı!

Sunucunuz artık **serifselen.local** etki alanında bir **Domain Controller** olarak çalışmaktadır. **DNS Server** hizmeti de otomatik olarak yapılandırılmıştır.

---

## 📂 Active Directory Yönetim İşlemleri

### Adım 11: Windows Tools ve Active Directory Araçlarına Erişim

![Adım 11](Images/11.png)

#### Yönetim Araçlarına Erişim Yöntemleri:

**1. Windows Tools Menüsü:**
- **Start** menüsünden **Windows Tools** klasörüne gidin
- Aşağıdaki araçlar mevcuttur:
  - Active Directory Users and Computers (dsa.msc)
  - Active Directory Sites and Services (dssite.msc)
  - Active Directory Domains and Trusts (domain.msc)
  - Group Policy Management (gpmc.msc)

**2. Komut Satırı Erişimi:**
```cmd
:: Active Directory Users and Computers
dsa.msc

:: Group Policy Management
gpmc.msc

:: Active Directory Administrative Center
dsac.exe
```

**3. PowerShell Modülleri:**
```powershell
# Active Directory modülünü yükleme
Import-Module ActiveDirectory

# Mevcut tüm AD cmdlet'lerini listeleme
Get-Command -Module ActiveDirectory
```

> **📌 Not:** Tüm yönetim araçlarının çalışması için **Active Directory Domain Services Tools** ve **RSAT (Remote Server Administration Tools)** yüklü olmalıdır.

---

### Adım 12: Active Directory Users and Computers Arayüzü

![Adım 12](Images/12.png)

#### ADUC (Active Directory Users and Computers) Arayüzü:

**Sol Panel - Domain Hiyerarşisi:**
```
📁 serifselen.local
  📁 Builtin
  📁 Computers
  📁 Domain Controllers
  📁 ForeignSecurityPrincipals
  📁 Managed Service Accounts
  📁 Users
```

**Sağ Panel - Varsayılan Container'lar:**
| Container | Açıklama | Taşınabilir | Silinebilir |
|-----------|----------|------------|-------------|
| **Builtin** | Yerleşik gruplar (Administrators, Users) | ❌ | ❌ |
| **Computers** | Etki alanına katılan bilgisayarlar | ❌ | ❌ |
| **Domain Controllers** | Domain Controller'lar | ❌ | ❌ |
| **Users** | Varsayılan kullanıcılar | ❌ | ❌ |

> **⚠️ Kritik Uyarı:** Varsayılan container'lar (Builtin, Users, Computers) **taşınamaz ve silinemez**. Kurumsal ortamlarda hiyerarşik OU yapısı oluşturmanız gerekir.

---

### Adım 13: Yeni Nesne Oluşturma Menüsü

![Adım 13](Images/13.png)

#### Sağ Tık Menüsü - Yeni Nesne Oluşturma:

**Mevcut Nesne Türleri:**
- 📂 **Organizational Unit** - Organizasyon birimleri
- 👥 **Group** - Güvenlik/dağıtım grupları
- 👤 **User** - Kullanıcı hesapları
- 💻 **Computer** - Bilgisayar hesapları
- 📇 **Contact** - İletişim bilgileri
- 🖨️ **Printer** - Paylaşılan yazıcılar
- 📁 **Shared Folder** - Paylaşılan klasörler

**Teknik Açıklama:**
- **Organizational Unit (OU)**: AD nesnelerini hiyerarşik olarak düzenlemek ve GPO uygulamak için kullanılır.
- **Group**: Kullanıcıları ve bilgisayarları topluca yönetmek ve izin atamak için kullanılır.
- **User**: Etki alanına kimlik doğrulaması yapacak kullanıcı hesapları.

> **💡 En İyi Uygulama:** OU yapısı oluştururken **"Protect container from accidental deletion"** seçeneğini mutlaka işaretleyin.

---

### Adım 14: İlk Organizational Unit (OU) Oluşturma

![Adım 14](Images/14.png)

#### OU Oluşturma Adımları:

1. `serifselen.local` domaini üzerinde sağ tık → **New** → **Organizational Unit**
2. **Name** alanı: `Selen Holding`
3. **Security settings** alanında:
   - ☑ **Protect container from accidental deletion** (ZORUNLU)
4. **OK** butonuna tıklayın

**Teknik Özellikler:**
- **Distinguished Name (DN):** `OU=Selen Holding,DC=serifselen,DC=local`
- **Object Class:** `organizationalUnit`
- **Security Descriptor:** OU'ya erişim izinleri

> **🔒 Güvenlik Önlemi:** "Protect container from accidental deletion" seçeneği, OU'nun yanlışlıkla silinmesini engeller. Bu özellik, Active Directory'ye **Deny Delete** izni ekler.

---

### Adım 15: Alt Organizational Unit Oluşturma

![Adım 15](Images/15.png)

#### Alt OU Oluşturma Adımları:

1. `Selen Holding` OU'su üzerinde sağ tık → **New** → **Organizational Unit**
2. **Name** alanı: `Istanbul`
3. **Security settings** alanında:
   - ☑ **Protect container from accidental deletion** (ZORUNLU)
4. **OK** butonuna tıklayın

**Teknik Yapılandırma:**
- **Parent Path:** `OU=Selen Holding,DC=serifselen,DC=local`
- **Child Path:** `OU=Istanbul,OU=Selen Holding,DC=serifselen,DC=local`
- **Linked Group Policy Objects:** (Henüz yok)

> **📊 Hiyerarşik Yapı:** Active Directory'de OU'lar üst-alt ilişkisiyle yönetilir. Alt OU'lar, üst OU'daki GPO'ları miras alır.

---

### Adım 16: OU Hiyerarşisi ve Yapılandırması

![Adım 16](Images/16.png)

#### Örnek Kurumsal OU Yapısı:

```
serifselen.local
└── Selen Holding (Top-level OU)
    ├── Istanbul (Location-based OU)
    │   ├── Users (Resource-type OU)
    │   │   ├── Finance (Department OU)
    │   │   ├── HR (Department OU)
    │   │   └── IT (Department OU)
    │   ├── Computers (Resource-type OU)
    │   ├── Servers (Resource-type OU)
    │   └── Groups (Resource-type OU)
    ├── Ankara (Location-based OU)
    └── Izmir (Location-based OU)
```

#### OU Tasarım İlkeleri:
1. **Kaynak Tabanlı:** Nesne türüne göre (Users, Computers, Groups)
2. **Coğrafi Tabanlı:** Lokasyona göre (Istanbul, Ankara)
3. **İşlevsel Tabanlı:** Departmana göre (Finance, HR, IT)
4. **GPO Uygulama Noktası:** Her OU seviyesi için ayrı GPO'lar

> **💡 En İyi Uygulama:** OU yapısı, organizasyonun fiziksel veya mantıksal yapısını yansıtmalıdır. Aşırı karmaşık OU hiyerarşilerinden kaçının.

---

### Adım 17: Güvenlik Grubu Oluşturma

![Adım 17](Images/17.png)
![Adım 18](Images/18.png)

#### Grup Oluşturma Adımları:

1. İlgili OU üzerinde sağ tık → **New** → **Group**
2. **Group Name:** `Finance`
3. **Group name (pre-Windows 2000):** `Finance`
4. **Group Scope:** `Global` (Önerilen)
5. **Group type:** `Security` (Önerilen)

#### Grup Kapsamları ve Kullanım Senaryoları:

| Kapsam | Açıklama | Kullanım Senaryosu |
|--------|----------|-------------------|
| **Domain Local** | Yalnızca kendi domain'inde kaynaklara izin verir | Sunucu paylaşımlarına erişim |
| **Global** | Kullanıcıları gruplar, tüm forest'te kullanılabilir | Departman grupları |
| **Universal** | Tüm domain'lerde kullanıcı grupları oluşturur | Çok domain'li ortamlar |

#### AGDLP Stratejisi:
- **A**ccounts → Kullanıcı hesapları
- **G**lobal Groups → Kullanıcıları gruplar
- **D**omain Local Groups → Kaynak izinleri
- **P**ermissions → İzin atamaları

```powershell
# PowerShell ile grup oluşturma
New-ADGroup -Name "Finance" -GroupScope Global -GroupCategory Security `
-Path "OU=Groups,OU=Istanbul,OU=Selen Holding,DC=serifselen,DC=local" `
-Description "Finance Department Users"
```

---

### Adım 18: Kullanıcı Hesabı Oluşturma

![Adım 19](Images/19.png)
![Adım 20](Images/20.png)
![Adım 21](Images/21.png)

#### Kullanıcı Oluşturma Adımları:

1. İlgili OU üzerinde sağ tık → **New** → **User**
2. **Personal Information:**
   - First name: `Serif`
   - Last name: `SELEN`
   - Full name: `Serif SELEN`
3. **Account Information:**
   - User logon name: `serifselen`
   - User logon name (pre-Windows 2000): `serifselen`
4. **Password Settings:**
   - Password: `P@ssw0rd123!`
   - User must change password at next logon: ☑ (Önerilen)

#### Kullanıcı Hesabı Özellikleri:

**Hesap Ayarları:**
- **User Principal Name (UPN):** `serifselen@serifselen.local`
- **Security Identifier (SID):** `S-1-5-21-315493517-3524552478-143585978-1105`
- **Primary Group ID:** `513` (Domain Users)

**Güvenlik Politikaları:**
- Parola süresizliği (`Password never expires`)
- Hesap kilitlenme eşiği
- Logon saatleri

```powershell
# PowerShell ile kullanıcı oluşturma
New-ADUser -Name "Serif SELEN" -GivenName "Serif" -Surname "SELEN" `
-UserPrincipalName "serifselen@serifselen.local" -SamAccountName "serifselen" `
-Path "OU=Finance,OU=Users,OU=Istanbul,OU=Selen Holding,DC=serifselen,DC=local" `
-Description "Finance Manager" -OfficePhone "+902125551234" `
-Enabled $true -AccountPassword (ConvertTo-SecureString "P@ssw0rd123!" -AsPlainText -Force) `
-ChangePasswordAtLogon $true
```

---

### Adım 19: Gruba Üye Ekleme

![Adım 22](Images/22.png)
![Adım 23](Images/23.png)

#### Üye Ekleme Adımları:

1. Grup üzerinde sağ tık → **Properties** → **Members** sekmesi
2. **Add...** butonuna tıklayın
3. **Select Users, Contacts, Computers** penceresinde:
   - **Enter the object names to select:** `serifselen`
   - **Check Names** butonuna tıklayarak doğrulama yapın
4. **OK** butonuna tıklayarak ekleyin

#### Üyelik Yönetimi Seçenekleri:

| Yöntem | Açıklama | PowerShell Komutu |
|--------|----------|-------------------|
| **Grup Özellikleri** | Grafik arayüz ile üyelik yönetimi | `Add-ADGroupMember` |
| **Delegation** | Belirli gruplara üyelik yönetimi yetkisi | `Set-ADGroup -AddAllowedAttributes` |
| **Bulk Operations** | Toplu üyelik yönetimi | `Get-ADUser -Filter * \| Add-ADPrincipalGroupMembership` |

```powershell
# Kullanıcıyı gruba ekleme
Add-ADGroupMember -Identity "Finance" -Members "serifselen"

# Grup üyelerini listeleme
Get-ADGroupMember -Identity "Finance" | Select-Object Name, SamAccountName, ObjectClass
```

---

### Adım 20: Group Policy Yönetim Konsolu

![Adım 24](Images/24.png)

#### GPMC (Group Policy Management Console) Arayüzü:

**Sol Panel - GPO Hiyerarşisi:**
```
📁 Group Policy Management
  📁 Forest: serifselen.local
    📁 Domains
      📁 serifselen.local
        📋 Default Domain Policy
        📋 Default Domain Controllers Policy
        📁 Group Policy Objects
        📁 Sites
        📁 Domain Controllers
        📁 Users
```

**Sağ Panel - GPO Özellikleri:**
- **Policy Name:** İlkenin adı
- **Links:** Bağlı olduğu OU'lar
- **Security Filtering:** İlke uygulamasına yetkili gruplar
- **WMI Filtering:** Koşullu uygulama (WMI sorguları)
- **Delegation:** Yönetim yetkileri

> **💡 En İyi Uygulama:** Her GPO'nun tek bir amacı olmalıdır. "Security Settings" ve "User Configuration" gibi farklı amaçları olan ayarları ayrı GPO'larda tutun.

---

### Adım 21: Yeni Grup İlkesi (GPO) Oluşturma

#### GPO Oluşturma Adımları:

1. **Group Policy Objects** klasörü üzerinde sağ tık → **New**
2. **Name** alanına: `Security - Password Policy`
3. **OK** butonuna tıklayın

#### GPO Kapsam Türleri:

| Kapsam Türü | Açıklama | Örnek |
|-------------|----------|-------|
| **Local GPO** | Yalnızca yerel makinede uygulanır | Tek makine politikaları |
| **Domain GPO** | Domain seviyesinde uygulanır | Şifre politikaları |
| **OU-linked GPO** | Belirli OU'ya uygulanır | Departman politikaları |
| **Site-linked GPO** | AD Sites seviyesinde uygulanır | Lokasyon bazlı politikalar |

```powershell
# Yeni GPO oluşturma
New-GPO -Name "Security - Password Policy" -Comment "Kurumsal şifre politikaları"

# GPO'yu domain seviyesine bağlama
New-GPLink -Name "Security - Password Policy" -Target "DC=serifselen,DC=local"
```

---

### Adım 22: GPO Ayarlarının Yapılandırılması

#### GPO Düzenleme Adımları:

1. Yeni oluşturulan GPO üzerinde sağ tık → **Edit**
2. **Group Policy Management Editor** açılır
3. **Computer Configuration** → **Policies** → **Windows Settings** → **Security Settings** → **Account Policies** → **Password Policy**

**Temel Şifre Politikaları:**
- **Enforced password history:** 24 passwords remembered
- **Maximum password age:** 90 days
- **Minimum password age:** 1 day
- **Minimum password length:** 14 characters
- **Password must meet complexity requirements:** Enabled

#### GPO İşlem Sırası:
1. **Local Group Policy** (Yerel politikalar)
2. **Site-linked GPOs** (Site politikaları)
3. **Domain-linked GPOs** (Domain politikaları)
4. **OU-linked GPOs** (OU politikaları) - Alt seviyeden üst seviyeye doğru

> **⚠️ Dikkat:** GPO ayarları **asynchronous** olarak uygulanır. Güncelleştirmeler için `gpupdate /force` komutunu çalıştırın.

---

### Adım 23: GPO'nun OU'ya Bağlanması

#### GPO Bağlama Adımları:

1. Hedef OU (`Istanbul`) üzerinde sağ tık → **Link an Existing GPO**
2. **Select GPO** penceresinde `Security - Password Policy` seçin
3. **OK** butonuna tıklayın

#### GPO Bağlantı Yönetimi:

| Seçenek | Açıklama | Komut |
|---------|----------|-------|
| **Enforced** | Alt OU'lar bu GPO'yu geçersiz kılamaz | `Set-GPLink -Enforced Yes` |
| **Block Inheritance** | Üst seviye GPO'ları devre dışı bırakır | `Set-GPInheritance -IsBlocked 1` |
| **Link Order** | Aynı OU'daki GPO uygulama sırası | `Set-GPLink -Priority` |

```powershell
# GPO'yu OU'ya bağlama
New-GPLink -Name "Security - Password Policy" `
-Target "OU=Istanbul,OU=Selen Holding,DC=serifselen,DC=local" `
-LinkEnabled Yes -Enforced No

# GPO durum kontrolü
Get-GPInheritance -Target "OU=Istanbul,OU=Selen Holding,DC=serifselen,DC=local"
```

---

### Adım 24: Delegated Administration Yapılandırması

#### Yetki Devretme Adımları:

1. OU üzerinde sağ tık → **Delegate Control**
2. **Delegation of Control Wizard** başlatılır
3. **Users or Groups** ekranında yetkilendirilecek grubu seçin (örn: `Istanbul Admins`)
4. **Tasks to Delegate** ekranında:
   - Create, delete, and manage user accounts
   - Reset user passwords and force password change at next logon
   - Modify the membership of a group

#### Yetkilendirme Seviyeleri:

| Seviye | Açıklama | Örnek |
|--------|----------|-------|
| **Full Control** | Tüm nesneler üzerinde tam yetki | Domain Admins |
| **Special Permissions** | Özel izinler (Create/Delete) | OU Yöneticileri |
| **Read/Write** | Okuma/yazma yetkisi | Destek personeli |

```powershell
# OU yönetimi için yetki devretme
$ou = "OU=Istanbul,OU=Selen Holding,DC=serifselen,DC=local"
$group = Get-ADGroup "Istanbul Admins"
$acl = Get-Acl "AD:\$ou"
$identity = [System.Security.Principal.IdentityReference] $group.SID
$adRights = [System.DirectoryServices.ActiveDirectoryRights] "GenericAll"
$type = [System.Security.AccessControl.AccessControlType] "Allow"
$inheritanceType = [System.DirectoryServices.ActiveDirectorySecurityInheritance] "All"
$ace = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $identity, $adRights, $type, $inheritanceType
$acl.AddAccessRule($ace)
Set-Acl -AclObject $acl "AD:\$ou"
```

---

## 🔧 Kurulum Sonrası Öneriler

### 1. Active Directory Altyapısı
- **Forest ve Domain Fonksiyon Seviyelerini** Windows Server 2025 olarak yükseltin
- **AD Recycle Bin** özelliğini etkinleştirin
- **Active Directory Schema** yöneticisini yükleyin
- **Sites and Services** yapılandırması yapın

### 2. Kimlik ve Erişim Yönetimi
- **Fine-Grained Password Policies** oluşturun
- **AD Federation Services (AD FS)** dağıtın
- **Microsoft Identity Manager (MIM)** ile kimlik yönetimi sağlayın
- **Privileged Access Management (PAM)** uygulayın

### 3. Güvenlik ve Denetim
- **Advanced Audit Policy** yapılandırın
- **Credential Guard** ve **Device Guard** özelliklerini etkinleştirin
- **SIEM entegrasyonu** sağlayın (Azure Sentinel, Splunk vb.)
- **Event Forwarding** ile merkezi log yönetimi

### 4. Performans ve Ölçeklenebilirlik
- **Global Catalog** sunucularını çoğaltın
- **Read-Only Domain Controllers (RODC)** dağıtın
- **DNS Load Balancing** yapılandırın
- **AD Sites** ile coğrafi çoğaltma yönetimi

### 5. Yedekleme ve Kurtarma
- **System State Backup** rutini oluşturun
- **AD DS Snapshot** alın
- **Authoritative Restore** prosedürleri hazırlayın
- **Disaster Recovery** senaryolarını test edin

---

## 💡 En İyi Uygulamalar (Best Practices)

### OU Tasarımı:
- **Maksimum 10 seviye** OU derinliği önerilir
- **Türkçe karakterler** kullanmayın
- **Açıklayıcı isimler** kullanın (IT_Dept yerine IT)
- **OU isimlendirme standartı** oluşturun

### Grup Yönetimi:
- **AGDLP stratejisini** uygulayın:
  ```
  Accounts (Kullanıcılar)
  ↓
  Global Groups (Departman grupları)
  ↓
  Domain Local Groups (Kaynak grupları)
  ↓
  Permissions (İzinler)
  ```
- **Universal Group** kullanımını minimum seviyede tutun
- **Nested Groups** ile yönetim karmaşıklığını azaltın

### GPO Yönetimi:
- **GPO isimlendirme standardı** oluşturun:
  ```
  [Kapsam] - [Kategori] - [Açıklama]
  Örn: DOMAIN - Security - Password Policy
       IST - Software - Office 365 Deployment
  ```
- **GPO'ları test ortamında** doğrulayın
- **GPO yedekleri** alın (`Backup-GPO` cmdlet'i)
- **GPO raporları** düzenli olarak oluşturun

### Güvenlik:
- **Least Privilege** ilkesini uygulayın
- **AdminSDHolder** korumasını etkinleştirin
- **LAPS (Local Administrator Password Solution)** dağıtın
- **Just-In-Time (JIT) erişim** sağlayın

---

## 🖥️ Yaygın PowerShell Komutları

### Active Directory Modülü Yüklemesi:
```powershell
# RSAT: Active Directory Domain Services Tools yükleme
Add-WindowsFeature RSAT-AD-PowerShell

# Modülü içe aktarma
Import-Module ActiveDirectory
```

### Kullanıcı Yönetimi:
```powershell
# Toplu kullanıcı oluşturma
Import-Csv "C:\Users.csv" | ForEach-Object {
    New-ADUser -Name $_.Name -GivenName $_.FirstName -Surname $_.LastName `
    -UserPrincipalName $_.UPN -SamAccountName $_.SamAccountName `
    -Path $_.OU -Enabled $true -AccountPassword (ConvertTo-SecureString $_.Password -AsPlainText -Force) `
    -ChangePasswordAtLogon $true
}

# Pasif kullanıcıları listeleme
Search-ADAccount -AccountInactive -UsersOnly -TimeSpan "90" | 
Select-Object Name, LastLogonDate, DistinguishedName
```

### OU Yönetimi:
```powershell
# OU yapısını CSV'den oluşturma
Import-Csv "C:\OU_Structure.csv" | ForEach-Object {
    if (!(Get-ADOrganizationalUnit -Filter "Name -eq '$($_.Name)'" -SearchBase $_.ParentPath -ErrorAction SilentlyContinue)) {
        New-ADOrganizationalUnit -Name $_.Name -Path $_.ParentPath -ProtectedFromAccidentalDeletion $true
    }
}

# OU'ların GPO bağlantılarını listeleme
Get-GPInheritance -Target "OU=Istanbul,OU=Selen Holding,DC=serifselen,DC=local" | 
Select-Object -ExpandProperty GpoLinks | 
Format-Table DisplayName, Enabled, Enforced
```

### GPO Yönetimi:
```powershell
# Tüm GPO'ları HTML raporu olarak dışa aktarma
Get-GPOReport -All -ReportType Html -Path "C:\GPO_Report.html"

# Belirli bir GPO'nun ayarlarını listeleme
Get-GPOReport -Name "Security - Password Policy" -ReportType Xml | 
Select-String -Pattern "<q1:PasswordSettings>"

# GPO çakışmalarını çözme
Get-GPO -All | Sort-Object -Property DisplayName | ForEach-Object {
    $gpo = $_
    $links = Get-GPLink -Guid $gpo.Id
    if ($links.Count -gt 1) {
        Write-Host "GPO '$($gpo.DisplayName)' birden fazla OU'ya bağlı:"
        $links | Format-Table Target, GpoId, Enabled
    }
}
```

### Denetim ve Raporlama:
```powershell
# Güvenlik etkinliklerini filtreleme
Get-WinEvent -LogName "Security" -MaxEvents 100 | 
Where-Object {$_.Id -eq 4624 -or $_.Id -eq 4625} | 
Format-Table TimeCreated, Id, Message -AutoSize

# AD replikasyon durumunu kontrol etme
Get-ADReplicationPartnerMetadata -Target "DOMAIN" | 
Select-Object Server, LastReplicationAttempt, LastReplicationSuccess, ConsecutiveFailures
```

---

## 📜 Doküman Bilgileri

| Özellik | Değer |
|---------|-------|
| **Yazar** | Serif SELEN |
| **Son Güncelleme** | 15 Kasım 2025 |
| **Platform** | VMware Workstation Pro 17 |
| **İşletim Sistemi** | Windows Server 2025 Standard Evaluation |
| **Etki Alanı Adı** | `serifselen.local` |
| **Forest Fonksiyon Seviyesi** | Windows Server 2025 |
| **Domain Fonksiyon Seviyesi** | Windows Server 2025 |
| **Lisans** | Evaluation (180 gün) |
| **Test Ortamı** | Tek DC, Tek Bölge |

> **⚠️ Uyarı:** Bu doküman **eğitim ve test ortamları** için hazırlanmıştır. Üretim sistemlerinde lisanslı yazılımlar ve resmi Microsoft belgeleri kullanılmalıdır.

> **📞 Destek İçin:** [serif.selen@outlook.com](mailto:serif.selen@outlook.com)  
> **🔗 GitHub Repository:** [https://github.com/serifselen/Active-Directory-ve-DNS-Kurulum](https://github.com/serifselen/Active-Directory-ve-DNS-Kurulum)

```markdown
[![Creative Commons License](https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-nc-sa/4.0/)
This work is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License.
```