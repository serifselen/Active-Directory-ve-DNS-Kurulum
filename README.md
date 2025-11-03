# Active Directory ve DNS Kurulum Rehberi  
## Windows Server 2025 Üzerinde AD DS ve DNS Kurulumu

Bu rehber, Windows Server 2025 Standard Evaluation sistemine Active Directory Domain Services (AD DS) ve DNS Server rollerinin nasıl kurulacağını adım adım açıklar. Kurulum, Server Manager aracılığıyla gerçekleştirilir.

---

## 📑 İçindekiler

- [Ön Gereksinimler ve Hazırlık](#ön-gereksinimler-ve-hazırlık)
- [AD DS Kurulum Adımları](#-ad-ds-kurulum-adımları)
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
- [Active Directory Yönetimi](#-active-directory-yönetimi)
  - [Adım 11: Windows Tools ve Active Directory Araçlarına Erişim](#adım-11-windows-tools-ve-active-directory-araclarına-erişim)
  - [Adım 12: Active Directory Users and Computers Arayüzü](#adım-12-active-directory-users-and-computers-arayüzü)
  - [Adım 13: Yeni Öğe Oluşturma Menüsü](#adım-13-yeni-öğe-oluşturma-menüsü)
  - [Adım 14: İlk Organizational Unit (OU) Oluşturma](#adım-14-i̇lk-organizational-unit-ou-oluşturma)
  - [Adım 15: Alt Organizational Unit Oluşturma](#adım-15-alt-organizational-unit-oluşturma)
  - [Adım 16: Detaylı OU Yapısı ve Departman Organizasyonu](#adım-16-detaylı-ou-yapısı-ve-departman-organizasyonu)
  - [Adım 17-18: Güvenlik Grubu Oluşturma](#adım-17-18-güvenlik-grubu-oluşturma)
  - [Adım 19-21: Kullanıcı Hesabı Oluşturma](#adım-19-21-kullanıcı-hesabı-oluşturma)
  - [Adım 22-23: Gruba Üye Ekleme](#adım-22-23-gruba-üye-ekleme)
  - [Adım 24: Group Policy Management Konsolu](#adım-24-group-policy-management-konsolu)
- [DNS Kayıt Oluşturma](#-dns-kayıt-oluşturma)
  - [Adım 25: DNS Manager'a Erişim](#adım-25-dns-managera-erişim)
  - [Adım 26: Yeni Host (A) Kaydı Oluşturma](#adım-26-yeni-host-a-kaydı-oluşturma)
  - [Adım 27: Host Kayıt Bilgilerini Girme](#adım-27-host-kayıt-bilgilerini-girme)
  - [Adım 28: Oluşturulan DNS Kaydını Doğrulama](#adım-28-oluşturulan-dns-kaydını-doğrulama)
- [Kurulum Sonrası Öneriler](#-kurulum-sonrası-öneriler)
- [En İyi Uygulamalar](#-en-i̇yi-uygulamalar)
- [PowerShell ile Otomasyon](#-powershell-ile-otomasyon)
- [Sık Karşılaşılan Sorunlar ve Çözümler](#-sık-karşılaşılan-sorunlar-ve-çözümler)
- [Güvenlik ve Denetim](#-güvenlik-ve-denetim)
- [Doküman Bilgileri](#-doküman-bilgileri)

---

## 🔰 Ön Gereksinimler ve Hazırlık

### Sistem Gereksinimleri
- **İşletim Sistemi**: Windows Server 2025 Standard/Datacenter
- **Bellek**: Minimum 4 GB (Önerilen 8+ GB)
- **Depolama**: Minimum 32 GB boş alan
- **Ağ**: Statik IP adresi ve DNS yapılandırması

### Ağ Yapılandırması
```powershell
# Statik IP ayarlama
New-NetIPAddress -IPAddress "192.168.31.100" -PrefixLength 24 -DefaultGateway "192.168.31.1" -InterfaceAlias "Ethernet"

# DNS sunucusu ayarlama
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses "127.0.0.1"

# Sunucu ismini ayarlama
Rename-Computer -NewName "DOMAIN" -Restart
```

### Güvenlik Hazırlıkları
- Yönetici şifresi karmaşıklığı
- Windows Update'lerin tamamlanması
- Güvenlik duvarı port kontrolleri

---

## 🖥️ AD DS Kurulum Adımları

### Adım 1: Server Manager Ana Ekranı

![Adım 1](Images/1.png)

**Teknik Detaylar:**
- Server Core kurulumunda PowerShell veya sconfig kullanılır
- GUI modunda Server Manager otomatik başlar
- Rol bazlı kurulum için temel arayüz

✅ AD DS kurulumuna başlamak için **"Add roles and features"** bağlantısına tıklayın.

**PowerShell Alternatifi:**
```powershell
# Server Manager'ı PowerShell'den başlatma
servermanager
```

---

### Adım 2: "Add Roles and Features Wizard" Başlatma

![Adım 2](Images/2.png)

**Kritik Ön Kontroller:**
- ✅ Statik IP yapılandırması doğrulanmalı
- ✅ DNS çözümlemesi test edilmeli
- ✅ Güncel Windows Update'ler kontrol edilmeli

**Teknik Doğrulama Komutları:**
```powershell
# IP yapılandırmasını kontrol et
Get-NetIPConfiguration

# DNS çözümlemesini test et
Test-NetConnection -ComputerName "www.microsoft.com" -Port 80

# Windows Update durumunu kontrol et
Get-WindowsUpdateLog
```

💡 Bu sayfa yalnızca bilgilendiricidir. **Next** butonuna tıklayarak devam edin.

---

### Adım 3: Kurulum Türü Seçimi

![Adım 3](Images/3.png)

**Kurulum Türleri Detayı:**
- **Role-based or feature-based installation**: Lokal veya remote sunucuya rol ekleme
- **Remote Desktop Services installation**: RDS farm dağıtımı için

✅ **"Role-based or feature-based installation"** seçeneğini işaretleyin.  
**Next** butonuna tıklayın.

**PowerShell ile Rol Ekleme:**
```powershell
# AD DS rolünü PowerShell ile ekleme
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```

---

### Adım 4: Hedef Sunucu Seçimi

![Adım 4](Images/4.png)

**Sunucu Seçim Teknik Detayları:**
- **Server Pool**: Mevcut yönetilen sunucular listesi
- **Offline Sunucular**: Erişilemeyen sunucular gri görünür
- **IPv6 Desteği**: Windows Server 2025 IPv6'yı tam destekler

✅ Kurulum yapılacak sunucu zaten seçili gelir. Doğru sunucuyu seçtiğinizden emin olduktan sonra **Next** butonuna tıklayın.

**Sunucu Bilgilerini Doğrulama:**
```powershell
# Sunucu bilgilerini görüntüleme
Get-ComputerInfo | Select-Object WindowsProductName, WindowsVersion, CsDomain
```

---

### Adım 5: Active Directory Domain Services Rolü Seçimi

![Adım 5](Images/5.png)

**Yüklenen Bileşenler:**
- **AD DS Services**: Çekirdek Active Directory hizmetleri
- **AD DS Tools**: Yönetim araçları
- **Group Policy Management**: GPO yönetim konsolu
- **AD PowerShell Module**: PowerShell modülleri

**Teknik Özellikler:**
- **NTDS.dit**: Active Directory veritabanı dosyası
- **SYSVOL**: Grup İlkesi ve script paylaşımı
- **LDAP**: Lightweight Directory Access Protocol

✅ **"Include management tools (if applicable)"** seçeneği otomatik işaretlenir.  
Açılan pencerede **Add Features** butonuna tıklayıp **Next** butonuna geçin.

---

### Adım 6: Deployment Configuration – Yeni Orman Oluşturma

![Adım 6](Images/6.png)

**Orman Seçenekleri Teknik Detay:**
- **Add a new forest**: İlk Domain Controller, yeni orman
- **Add a domain to an existing forest**: Mevcut ormana domain ekleme
- **Add a domain controller to an existing domain**: Mevcut domain'e DC ekleme

**DNS Entegrasyonu:**
- DNS sunucusu otomatik olarak yüklenir
- DNS bölgesi otomatik oluşturulur
- SRV kayıtları otomatik kaydedilir

⚠️ **Domain Name Best Practices:**
- İç namespace için .local kullanın
- Dış erişim için registered domain kullanın
- Kısa ve anlamlı isimler seçin

**PowerShell ile Domain Promotion:**
```powershell
# AD DS deployment configuration
Install-ADDSForest -DomainName "serifselen.local" -DomainNetbiosName "SERIFSELEN" -InstallDns -NoRebootOnCompletion
```

---

### Adım 7: Domain Controller Seçenekleri

![Adım 7](Images/7.png)

**Functional Level Seçenekleri:**
- **Forest Functional Level**: Tüm domain'lerdeki DC'lerin minimum OS seviyesi
- **Domain Functional Level**: Belirli domain'deki DC'lerin minimum OS seviyesi

**Teknik Özellikler:**
- **DNS Server**: AD tümleşik DNS bölgesi
- **Global Catalog**: Çok domain'li aramalar için
- **Read Only Domain Controller (RODC)**: Şube ofisler için

🔒 **DSRM Password Requirements:**
- Domain şifre politikasından bağımsız
- Karmaşık şifre zorunluluğu var
- Güvenli şifre yönetimi önemli

**Functional Level Karşılaştırması:**
| Seviye | Özellikler | Geriye Dönük Uyumluluk |
|--------|------------|------------------------|
| **WS2025** | Tüm yeni özellikler | Sadece WS2025 DC'ler |
| **WS2016** | AES, RODC geliştirmeleri | WS2012R2+ |
| **WS2012R2** | Temel özellikler | WS2008R2+ |

---

### Adım 8: Ön Koşul Denetimi

![Adım 8](Images/8.png)

**Ön Koşul Kontrol Listesi:**
- ✅ DNS resolver cache temizleme
- ✅ NetBIOS isim çakışması kontrolü
- ✅ TCP/IP yapılandırması doğrulama
- ✅ Güvenlik politikası uyumluluğu

**Sık Karşılaşılan Uyarılar:**
- **"DNS delegation"**: Yeni orman için normal
- **"Weak password"**: DSRM şifresi kontrolü
- **"Time synchronization"**: PDC emulator rolü

⚠️ "A delegation for this DNS server cannot be created…" uyarısı, mevcut bir DNS altyapısı yoksa **ihmal edilebilir**.  
**Install** butonuna tıklayarak kurulumu başlatın.

**Ön Koşul PowerShell Scripti:**
```powershell
# Ön koşul kontrolleri
Test-ADDSDomainControllerInstallation -DomainName "serifselen.local" -InstallDns -NoGlobalCatalog:$false
```

---

### Adım 9: Kurulum İlerleme Durumu

![Adım 9](Images/9.png)

**Kurulum Aşamaları:**
1. **Binary Copy**: AD DS binary dosyalarının kopyalanması
2. **Schema Update**: Active Directory şemasının güncellenmesi
3. **Configuration Partition**: Yapılandırma bölümü oluşturma
4. **Domain Partition**: Domain bölümü oluşturma
5. **SYSVOL Creation**: SYSVOL paylaşımının oluşturulması
6. **DNS Zone Creation**: AD-integrated DNS bölgesi oluşturma

**Teknik Dosya Konumları:**
- **NTDS.dit**: `%SystemRoot%\NTDS\NTDS.dit`
- **SYSVOL**: `%SystemRoot%\SYSVOL\`
- **Log Files**: `%SystemRoot%\NTDS\`
- **Database**: `%SystemRoot%\NTDS\`

🔄 Kurulum tamamlandığında sunucu **otomatik olarak yeniden başlatılır**.

---

### Adım 10: Post-deployment Yapılandırma Uyarısı

![Adım 10](Images/10.png)

**Post-installation Tasks:**
- DNS kayıtlarının doğrulanması
- SYSVOL replikasyonunun kontrolü
- Zaman servisinin yapılandırılması
- Güvenlik duvarı kurallarının kontrolü

**Doğrulama Komutları:**
```powershell
# DC rolünü doğrula
Get-ADDomainController -Identity $env:COMPUTERNAME

# DNS kayıtlarını kontrol et
Get-DnsServerResourceRecord -ZoneName "serifselen.local" -RRType SRV

# SYSVOL durumunu kontrol et
Dcdiag /test:netlogons /test:services /test:sysvol
```

✅ Bu uyarı, AD DS yapılandırmasının tamamlanmadığını gösterir.  
Bağlantıya tıklayarak yapılandırmayı tamamlayabilir veya komut satırından `dcpromo` ile devam edebilirsiniz.

---

## 🎉 Kurulum Tamamlandı!

Sunucunuz artık **serifselen.local** etki alanında bir **Domain Controller** olarak çalışmaktadır. **DNS Server** hizmeti de otomatik olarak yapılandırılmıştır.

**Doğrulama Testleri:**
```powershell
# Temel sistem sağlık kontrolü
Dcdiag /s:$env:COMPUTERNAME /q

# DNS çözümleme testi
Resolve-DnsName "serifselen.local"

# LDAP bağlantı testi
Get-ADDomain -Server $env:COMPUTERNAME
```

---

## 📂 Active Directory Yönetimi

### Adım 11: Windows Tools ve Active Directory Araçlarına Erişim

![Adım 11](Images/11.png)

**RSAT (Remote Server Administration Tools) Bileşenleri:**
- **Active Directory Administrative Center**: Modern AD yönetim arayüzü
- **Active Directory Users and Computers**: Geleneksel AD yönetimi
- **Active Directory Domains and Trusts**: Domain trust ilişkileri
- **Active Directory Sites and Services**: Replikasyon topolojisi
- **Group Policy Management**: Merkezi politika yönetimi

**PowerShell Modülleri:**
```powershell
# Active Directory modülünü yükle
Import-Module ActiveDirectory

# Kullanılabilir AD cmdlet'lerini listele
Get-Command -Module ActiveDirectory

# AD modülü versiyon bilgisi
Get-Module ActiveDirectory | Select-Object Version, Path
```

✅ **Active Directory Users and Computers** seçeneğine tıklayarak devam edin.

---

### Adım 12: Active Directory Users and Computers Arayüzü

![Adım 12](Images/12.png)

**Varsayılan Container'ların Teknik Analizi:**

| Container | Amaç | Önemli Nesneler |
|-----------|------|-----------------|
| **Builtin** | Yerleşik güvenlik grupları | Administrators, Users, Backup Operators |
| **Computers** | Domain'e katılan bilgisayarlar | İş istasyonları, üye sunucular |
| **Domain Controllers** | Domain Controller'lar | Tüm DC bilgisayar hesapları |
| **Users** | Varsayılan kullanıcı/gruplar | Domain Users, Domain Admins |

**Advanced Features Görünümü:**
- **View > Advanced Features**: Sistem nesnelerini göster
- **LostAndFound**: Silinmiş/çakışan nesneler
- **Program Data**: Uygulama veri nesneleri
- **NTDS Quotas**: LDAP query limitleri

💡 Bu varsayılan container'lar silinemez ve taşınamaz. Yeni organizasyon yapısı için **Organizational Unit (OU)** oluşturmanız önerilir.

---

### Adım 13: Yeni Öğe Oluşturma Menüsü

![Adım 13](Images/13.png)

**Nesne Türleri ve Özellikleri:**

| Nesne Türü | ObjectClass | Kullanım Amacı |
|------------|-------------|----------------|
| **Organizational Unit** | organizationalUnit | Mantıksal gruplama, GPO uygulama |
| **Group** | group | Güvenlik grupları, izin yönetimi |
| **User** | user | Kullanıcı kimlik bilgileri |
| **Computer** | computer | Bilgisayar kimlik bilgileri |
| **Contact** | contact | E-posta kişileri |

**PowerShell ile Nesne Oluşturma:**
```powershell
# Çoklu OU oluşturma
$OUs = @("IT", "Finance", "HR", "Sales")
foreach ($OU in $OUs) {
    New-ADOrganizationalUnit -Name $OU -Path "DC=serifselen,DC=local" -ProtectedFromAccidentalDeletion $true
}
```

✅ Yeni bir organizasyon yapısı oluşturmak için **New > Organizational Unit** seçeneğini kullanın.

---

### Adım 14: İlk Organizational Unit (OU) Oluşturma

![Adım 14](Images/14.png)

**OU Teknik Özellikleri:**
- **Distinguished Name**: `OU=Selen Holding,DC=serifselen,DC=local`
- **ObjectGUID**: Benzersiz tanımlayıcı
- **WhenCreated**: Oluşturulma zaman damgası
- **WhenChanged**: Değiştirilme zaman damgası

**Güvenlik Ayarları:**
- **Inheritance**: Üst containerdan miras alma
- **Permissions**: Özel izinler atanabilir
- **Ownership**: Nesne sahipliği

🔒 **"Protect container from accidental deletion"** seçeneği:
- OU'nun yanlışlıkla silinmesini önler
- **Üretim ortamlarında mutlaka işaretlenmelidir**
- Advanced Features açıkken OU Properties > Object sekmesinden yönetilebilir

**PowerShell ile Korumalı OU:**
```powershell
# OU oluşturma ve koruma
New-ADOrganizationalUnit -Name "Selen Holding" -Path "DC=serifselen,DC=local"
Set-ADOrganizationalUnit -Identity "OU=Selen Holding,DC=serifselen,DC=local" -ProtectedFromAccidentalDeletion $true
```

✅ OU adını girin, koruma seçeneğini işaretleyin ve **OK** butonuna tıklayın.

---

### Adım 15: Alt Organizational Unit Oluşturma

![Adım 15](Images/15.png)

**OU Hiyerarşisi Best Practices:**
- **Maksimum OU Derinliği**: 10-15 seviye (performans için)
- **Adlandırma Standardı**: Türkçe karakter kullanmama
- **Delegation Model**: Yönetim delegasyonu için tasarım

**Teknik Yapı:**
```
DN: OU=Ankara,OU=Selen Holding,DC=serifselen,DC=local
├── Canonical Name: serifselen.local/Selen Holding/Ankara
├── Object Category: organizationalUnit
└── AdminSDHolder: Güvenlik miras alma kontrolü
```

🗂️ **Hiyerarşik Yapı Mantığı:**
```
Şirket (Selen Holding)
  └── Lokasyon (Ankara, Istanbul, İzmir)
      └── Departman (IT, Finance, HR)
          └── Kaynak Tipi (Users, Computers, Groups)
```

**PowerShell ile Hiyerarşik OU:**
```powershell
# Hiyerarşik OU yapısı oluşturma
$Locations = @("Ankara", "Istanbul", "Izmir")
$Departments = @("IT", "Finance", "HR", "Sales")

foreach ($Location in $Locations) {
    $LocationOU = New-ADOrganizationalUnit -Name $Location -Path "OU=Selen Holding,DC=serifselen,DC=local" -PassThru
    
    foreach ($Dept in $Departments) {
        $DeptOU = New-ADOrganizationalUnit -Name $Dept -Path $LocationOU.DistinguishedName -PassThru
        
        # Alt OU'lar oluştur
        New-ADOrganizationalUnit -Name "Users" -Path $DeptOU.DistinguishedName
        New-ADOrganizationalUnit -Name "Computers" -Path $DeptOU.DistinguishedName
        New-ADOrganizationalUnit -Name "Groups" -Path $DeptOU.DistinguishedName
    }
}
```

✅ Alt OU adını girin ve **OK** butonuna tıklayın.

---

### Adım 16: Detaylı OU Yapısı ve Departman Organizasyonu

![Adım 16](Images/16.png)

**Gelişmiş OU Tasarımı:**
```
Selen Holding
├── Ankara
│   ├── Computers
│   ├── Servers
│   ├── Users
│   │   ├── Finance
│   │   ├── HR
│   │   └── IT
│   └── Groups
├── Istanbul
│   ├── Computers
│   ├── Servers  
│   ├── Users
│   └── Groups
└── Izmir
```

**OU Tasarım Prensipleri:**
- **Coğrafi Tasarım**: Lokasyon bazlı yönetim
- **Organizasyonel Tasarım**: Departman bazlı yapı
- **Fonksiyonel Tasarım**: Rol bazlı organizasyon
- **Karma Tasarım**: Çok boyutlu yapı

**PowerShell ile OU Raporlama:**
```powershell
# OU yapısını raporla
Get-ADOrganizationalUnit -Filter * -Properties ProtectedFromAccidentalDeletion | 
Select-Object Name, DistinguishedName, ProtectedFromAccidentalDeletion |
Export-Csv -Path "C:\OU_Structure_Report.csv" -NoTypeInformation
```

---

### Adım 17-18: Güvenlik Grubu Oluşturma

![Adım 17](Images/17.png)
![Adım 18](Images/18.png)

**Grup Türleri ve Kapsamları:**

| Grup Türü | Security ID | Kullanım Senaryosu |
|-----------|-------------|-------------------|
| **Domain Local** | S-1-5-21-domain-* | Lokal kaynak izinleri |
| **Global** | S-1-5-21-domain-* | Kullanıcı/grup organizasyonu |
| **Universal** | S-1-5-21-domain-* | Cross-domain gruplama |

**Grup Özellikleri:**
- **groupType**: GROUP_TYPE_SECURITY_ENABLED (0x80000000)
- **sAMAccountType**: SAM_GROUP_OBJECT (0x10000000)
- **objectSid**: Güvenlik tanımlayıcısı

**PowerShell ile Grup Yönetimi:**
```powershell
# Güvenlik grubu oluşturma
New-ADGroup -Name "Finance" -GroupScope Global -GroupCategory Security `
-Path "OU=Groups,OU=Ankara,OU=Selen Holding,DC=serifselen,DC=local" `
-Description "Finance department security group" `
-DisplayName "Finance Department" -ManagedBy "CN=Serif SELEN,OU=Users,OU=Finance,OU=Ankara,OU=Selen Holding,DC=serifselen,DC=local"

# Grup üyelik raporu
Get-ADGroup -Filter * -Properties Members | 
Select-Object Name, GroupScope, GroupCategory, @{Name="MemberCount";Expression={$_.Members.Count}}
```

---

### Adım 19-21: Kullanıcı Hesabı Oluşturma

![Adım 19](Images/19.png)
![Adım 20](Images/20.png)
![Adım 21](Images/21.png)

**Kullanıcı Hesap Özellikleri:**
- **userAccountControl**: Hesap ayarları (NORMAL_ACCOUNT = 0x200)
- **pwdLastSet**: Son şifre değişikliği
- **lastLogon**: Son oturum açma
- **badPwdCount**: Başarısız giriş sayacı

**Şifre Politikaları:**
```powershell
# Şifre politikasını görüntüle
Get-ADDefaultDomainPasswordPolicy

# Karmaşık şifre politikası ayarla
Set-ADDefaultDomainPasswordPolicy -ComplexityEnabled $true -MinPasswordLength 12 -MaxPasswordAge 90.00:00:00
```

**PowerShell ile Toplu Kullanıcı Oluşturma:**
```powershell
# CSV'den kullanıcı içe aktarma
$Users = Import-Csv -Path "C:\UserList.csv"

foreach ($User in $Users) {
    $SecurePassword = ConvertTo-SecureString $User.Password -AsPlainText -Force
    
    New-ADUser -Name "$($User.FirstName) $($User.LastName)" `
        -GivenName $User.FirstName `
        -Surname $User.LastName `
        -SamAccountName $User.SamAccountName `
        -UserPrincipalName "$($User.SamAccountName)@serifselen.local" `
        -Path "OU=$($User.Department),OU=Users,OU=$($User.Location),OU=Selen Holding,DC=serifselen,DC=local" `
        -AccountPassword $SecurePassword `
        -Enabled $true `
        -ChangePasswordAtLogon $true `
        -Department $User.Department `
        -Title $User.Title `
        -Office $User.Location
}
```

---

### Adım 22-23: Gruba Üye Ekleme

![Adım 22](Images/22.png)

**Grup Üyelik Yönetimi:**
- **Direct Membership**: Doğrudan üyelik
- **Nested Groups**: Grup içinde grup
- **Dynamic Groups**: Query-based üyelik (AD Premium)

**PowerShell ile Gelişmiş Üyelik Yönetimi:**
```powershell
# Toplu üye ekleme
$Users = Get-ADUser -Filter "Department -eq 'Finance'" -SearchBase "OU=Finance,OU=Users,OU=Ankara,OU=Selen Holding,DC=serifselen,DC=local"
Add-ADGroupMember -Identity "Finance" -Members $Users

# Grup üyelik raporu oluşturma
Get-ADGroup -Filter * | ForEach-Object {
    $Group = $_
    $Members = Get-ADGroupMember -Identity $Group.Name
    
    [PSCustomObject]@{
        GroupName = $Group.Name
        GroupScope = $Group.GroupScope
        MemberCount = $Members.Count
        Members = $Members.Name -join ", "
    }
} | Export-Csv -Path "C:\Group_Membership_Report.csv" -NoTypeInformation
```

✅ Kullanıcı artık Finance grubunun üyesidir.

---

### Adım 24: Group Policy Management Konsolu

![Adım 23](Images/23.png)
![Adım 24](Images/24.png)

**GPO Bileşenleri:**
- **GPC (Group Policy Container)**: AD'de depolanan metadata
- **GPT (Group Policy Template)**: SYSVOL'da depolanan ayarlar
- **Client Side Extension**: İstemci tarafı işleme

**GPO Processing Order:**
1. **Local GPO** → 2. **Site GPO** → 3. **Domain GPO** → 4. **OU GPO**

**PowerShell GPO Yönetimi:**
```powershell
# GPO oluşturma ve bağlama
$GPO = New-GPO -Name "Security - Workstation Policy" -Comment "Baseline security settings for workstations"

# GPO ayarlarını yapılandırma
Set-GPRegistryValue -Name "Security - Workstation Policy" -Key "HKLM\SOFTWARE\Policies\Microsoft\WindowsFirewall\DomainProfile" -ValueName "EnableFirewall" -Type DWord -Value 1
Set-GPRegistryValue -Name "Security - Workstation Policy" -Key "HKLM\SOFTWARE\Policies\Microsoft\Windows\PowerShell" -ValueName "ExecutionPolicy" -Type String -Value "RemoteSigned"

# GPO bağlama
New-GPLink -Name "Security - Workstation Policy" -Target "OU=Computers,OU=Ankara,OU=Selen Holding,DC=serifselen,DC=local" -LinkEnabled Yes

# GPO backup alımı
Backup-GPO -Name "Security - Workstation Policy" -Path "C:\GPOBackup"
```

---

## 🌐 DNS Kayıt Oluşturma

### Adım 25: DNS Manager'a Erişim

![DNS Manager](Images/25.png)

**DNS Manager Arayüzü:**
- Sol panelde `Forward Lookup Zones` altında `serifselen.local` bölgesi bulunur.
- Sağ panelde mevcut DNS kayıtları listelenir.
- DNS sunucusu, AD DS kurulumu sırasında otomatik olarak kurulmuştur.

✅ DNS Manager'ı açmak için **Start > Administrative Tools > DNS** yolunu takip edin veya Server Manager üzerinden `Tools > DNS` seçeneğini kullanın.

---

### Adım 26: Yeni Host (A) Kaydı Oluşturma

![New Host Menu](Images/26.png)

**Yeni Kayıt Oluşturma:**
1. `serifselen.local` bölgesine sağ tıklayın.
2. **New Host (A or AAAA)...** seçeneğini seçin.

✅ Bu işlem, belirtilen ana bilgisayar adına bir IP adresi eşleme oluşturur.

---

### Adım 27: Host Kayıt Bilgilerini Girme

![New Host Dialog](Images/27.png)

**Kayıt Detayları:**
- **Name**: `web` (Ana bilgisayar adı)
- **Fully qualified domain name (FQDN)**: `web.serifselen.local` (Otomatik oluşturulur)
- **IP address**: `192.168.31.200` (Hedef sunucunun IP adresi)
- **Create associated pointer (PTR) record**: Kutu işaretlenmelidir (Ters DNS çözümlemesi için)

✅ Tüm bilgileri girdikten sonra **Add Host** butonuna tıklayın.

---

### Adım 28: Oluşturulan DNS Kaydını Doğrulama

![DNS Records](Images/25.png)

**Kayıt Doğrulama:**
- `serifselen.local` bölgesi altında yeni `Host (A)` kaydı (`web`) listelenir.
- IP adresi `192.168.31.200` olarak görünür.
- Kayıt tipi `static` olarak işaretlenmiştir.

✅ DNS kaydı başarıyla oluşturuldu. Artık `web.serifselen.local` adıyla bu IP adresine erişilebilir.

---

## 🔧 Kurulum Sonrası Öneriler

### 1. Sistem Sağlık Kontrolleri
```powershell
# DCDiag ile kapsamlı test
Dcdiag /s:$env:COMPUTERNAME /v /c /e

# Replikasyon durumunu kontrol et
Repadmin /replsummary

# DNS sağlık kontrolü
Dcdiag /test:dns /v
```

### 2. Yedekleme Stratejisi
```powershell
# System State yedekleme
wbadmin start systemstatebackup -backupTarget:D:

# AD yedekleme (Windows Server Backup)
Install-WindowsFeature -Name Windows-Server-Backup
```

### 3. Monitoring ve Logging
```powershell
# Event log yapılandırması
wevtutil sl "Directory Service" /ms:1024000000
wevtutil sl "DNS Server" /ms:512000000

# Performans sayaçları
Get-Counter "\Directory Services(*)\*" -SampleInterval 60 -MaxSamples 10
```

---

## 💡 En İyi Uygulamalar

### Güvenlik Temelleri
```powershell
# Admin hesaplarını koruma
Get-ADUser -Filter "AdminCount -eq 1" | Set-ADUser -Replace @{adminCount=0}

# Guest hesabını devre dışı bırakma
Disable-ADAccount -Identity "Guest"

# Default Administrator'ı yeniden adlandırma
Rename-LocalUser -Name "Administrator" -NewName "SRV_Admin"
```

### Backup ve Recovery
```powershell
# Active Directory Recycle Bin'ı etkinleştirme
Enable-ADOptionalFeature -Identity "Recycle Bin Feature" -Scope ForestOrConfigurationSet -Target "serifselen.local"
```

---

## 🖥️ PowerShell ile Otomasyon

### Toplu İşlemler
```powershell
# Toplu kullanıcı oluşturma
1..50 | ForEach-Object {
    $UserNumber = $_.ToString("00")
    New-ADUser -Name "TestUser$UserNumber" -SamAccountName "testuser$UserNumber" -AccountPassword (ConvertTo-SecureString "TempP@ss123!" -AsPlainText -Force) -Enabled $true
}

# Toplu OU temizleme
Get-ADOrganizationalUnit -Filter * | Where-Object {$_.Name -ne "Domain Controllers"} | Remove-ADOrganizationalUnit -Confirm:$false
```

### Raporlama ve Monitoring
```powershell
# AD sağlık raporu
$Report = @()
$Report += "Active Directory Health Report - $(Get-Date)"
$Report += "=============================================="
$Report += "Domain: $((Get-ADDomain).DNSRoot)"
$Report += "Forest: $((Get-ADForest).Name)"
$Report += "Domain Controllers: $(@(Get-ADDomainController -Filter *).Count)"
$Report += "Total Users: $(@(Get-ADUser -Filter *).Count)"
$Report += "Total Groups: $(@(Get-ADGroup -Filter *).Count)"
$Report += "Total Computers: $(@(Get-ADComputer -Filter *).Count)"

$Report | Out-File "C:\AD_Health_Report.txt"
```

---

## 🛠️ Sık Karşılaşılan Sorunlar ve Çözümler

### DNS Sorunları
```powershell
# DNS kayıtlarını temizleme ve yeniden oluşturma
ipconfig /flushdns
ipconfig /registerdns
net stop netlogon && net start netlogon

# DNS SRV kayıtlarını kontrol etme
nslookup -type=SRV _ldap._tcp.dc._msdcs.serifselen.local
```

### Replikasyon Sorunları
```powershell
# Replikasyon durumunu kontrol etme
Repadmin /showrepl
Repadmin /replsummary

# Replikasyonu zorlama
Repadmin /syncall /A /e /P
```

---

## 🔒 Güvenlik ve Denetim

### Güvenlik Denetimleri
```powershell
# Şifre politikası denetimi
Get-ADDefaultDomainPasswordPolicy | Select-Object ComplexityEnabled, MinPasswordLength, MaxPasswordAge

# Hesap kilitleme politikası
Get-ADDefaultDomainPasswordPolicy | Select-Object LockoutThreshold, LockoutDuration, LockoutObservationWindow

# Domain denetim politikaları
Get-GPO -All | Where-Object {$_.DisplayName -like "*Audit*"} | Select-Object DisplayName, GPOStatus
```

### Log Yapılandırması
```powershell
# AD denetim politikalarını yapılandırma
auditpol /set /category:"Account Management" /success:enable /failure:enable
auditpol /set /category:"Logon/Logoff" /success:enable /failure:enable
```

---

## 📜 Doküman Bilgileri

| Özellik | Değer |
|---------|-------|
| **Yazar** | Serif SELEN |
| **Tarih** | 2 Kasım 2025 |
| **Versiyon** | 2.0 |
| **Platform** | VMware Workstation Pro 17 |
| **İşletim Sistemi** | Windows Server 2025 Standard Evaluation |
| **Etki Alanı Adı** | `serifselen.local` |
| **DNS** | Otomatik olarak kurulmuştur |
| **Lisans** | Evaluation (180 gün) |

**Değişiklik Geçmişi:**
- **v2.0**: PowerShell otomasyon, teknik detaylar, sorun giderme bölümleri eklendi
- **v1.0**: Temel kurulum adımları ve görsel rehber

> ⚠️ Bu doküman eğitim ve test ortamları için hazırlanmıştır. Üretimde lisanslı yazılım ve güvenlik önlemleri kullanılmalıdır.

> 📧 **Destek İçin**: [mserifselen@gmail.com](mailto:mserifselen@gmail.com)  
> 🔗 **GitHub Repository**: [https://github.com/serifselen/Active-Directory-ve-DNS-Kurulum    ]