# Active Directory Yapılandırması - Bölüm 2: OU, Kullanıcı, Grup ve GPO Yönetimi

**Windows Server 2025 - Active Directory Domain Services**

Bu rehber, **Active Directory Domain Services** kurulumu tamamlanmış bir ortamda **Organizational Unit (OU)**, **kullanıcı**, **grup oluşturma** ve **Group Policy Object (GPO)** yapılandırmasını adım adım açıklar.

---

## 📋 Önceki Adımların Özeti

- ✅ **Active Directory Domain Services** kurulumu tamamlandı
- ✅ **DNS Server** rolü yapılandırıldı  
- ✅ **serifselen.local** domaini oluşturuldu
- ✅ **Domain Controller** promosyonu başarıyla tamamlandı

---

## 🎯 Bu Bölümde Yapılacaklar

1. [Organizational Unit (OU) Yapısı Oluşturma](#1-organizational-unit-ou-yapısı-oluşturma)
2. [Grup Oluşturma ve Yapılandırma](#2-grup-oluşturma-ve-yapılandırma)
3. [Kullanıcı Hesapları Oluşturma](#3-kullanıcı-hesapları-oluşturma)
4. [Kullanıcıları Gruplara Ekleme](#4-kullanıcıları-gruplara-ekleme)
5. [Group Policy Object (GPO) Oluşturma ve Yapılandırma](#5-group-policy-object-gpo-oluşturma-ve-yapılandırma)

---

## 1. Organizational Unit (OU) Yapısı Oluşturma

### 1.1 Ana OU Oluşturma

![Adım 4](4.png)

**Active Directory Users and Computers** konsolunda:

- **Sağ tık** → **New** → **Organizational Unit**
- **Name**: `Selen Holding`
- ✅ **Protect container from accidental deletion**
- **Create in**: `serifselen.local/`

> 🏢 **Selen Holding** şirketimizin ana organizasyon birimidir.

### 1.2 Alt OU'lar Oluşturma

![Adım 5](5.png)

**Selen Holding** altında şube OU'su oluşturma:

- **Selen Holding** → **Sağ tık** → **New** → **Organizational Unit**
- **Name**: `istanbul`
- ✅ **Protect container from accidental deletion**
- **Create in**: `serifselen.local/Selen Holding`

### 1.3 Departman OU'ları Oluşturma

![Adım 6](6.png)

**istanbul** OU'su altında departman yapısı:

- **Groups** OU → Finance, HR, IT grupları için
- **Users** OU → Finance, HR, IT kullanıcıları için
- **Computers** OU → Şube bilgisayarları için
- **Servers** OU → Şube sunucuları için

> 📊 **Örnek OU Yapısı:**
> ```
> serifselen.local
> └── Selen Holding
>     └── istanbul
>         ├── Groups
>         │   ├── Finance
>         │   ├── HR
>         │   └── IT
>         ├── Users
>         │   ├── Finance
>         │   ├── HR
>         │   └── IT
>         ├── Computers
>         └── Servers
> ```

---

## 2. Grup Oluşturma ve Yapılandırma

### 2.1 Grup Oluşturma

![Adım 7](7.png)

**Finance** grubu oluşturma:

- **Groups/Finance** OU → **Sağ tık** → **New** → **Group**
- **Group name**: `Finance`
- **Group scope**: `Global`
- **Group type**: `Security`

### 2.2 Grup Özelliklerini Yapılandırma

![Adım 8](8.png)

**Finance** grubu özellikleri:

- **Description**: `Finance Department Users`
- **E-mail**: `finance@serifselen.local`
- **Group scope**: `Global` (varsayılan)
- **Group type**: `Security` (varsayılan)

> 👥 **Grup Scope Açıklamaları:**
> - **Domain Local**: Kaynaklara erişim izinleri için
> - **Global**: Kullanıcıları gruplandırmak için
> - **Universal**: Çok domainli ortamlar için

---

## 3. Kullanıcı Hesapları Oluşturma

### 3.1 Kullanıcı Bilgilerini Girme

![Adım 9](9.png)

**Finance** kullanıcısı oluşturma:

- **Users/Finance** OU → **Sağ tık** → **New** → **User**
- **First name**: `Seif`
- **Last name**: `SELEN`
- **Full name**: `Seif SELEN` (otomatik)
- **User logon name**: `seifselen@serifselen.local`

### 3.2 Şifre ve Hesap Ayarları

![Adım 10](10.png)

**Password** ve **Account Options**:

- **Password**: `********` (güçlü şifre)
- **Confirm password**: `********`
- ✅ **User must change password at next logon**
- ❌ **User cannot change password**
- ❌ **Password never expires**
- ❌ **Account is disabled**

> 🔐 **Güvenlik En İyi Uygulamaları:**
> - İlk girişte şifre değiştirme zorunluluğu
> - Kompleks şifre politikaları
> - Düzenli şifre değişimi

---

## 4. Kullanıcıları Gruplara Ekleme

### 4.1 Grup Üyelikleri Yönetimi

![Adım 11](11.png)

**Finance** grubu üye ekleme:

- **Finance** grup → **Sağ tık** → **Properties** → **Members** tab
- **Add** butonuna tıklayın

### 4.2 Kullanıcı Seçimi

![Adım 12](12.png)

**Kullanıcı ekleme** dialog penceresi:

- **Select this object type**: `Users`
- **From this location**: `serifselen.local`
- **Enter the object names**: `seifselen`
- **Check Names** → **OK**

> ✅ Kullanıcı adı altı çizili görünürse doğrulama başarılı demektir.

---

## 5. Group Policy Object (GPO) Oluşturma ve Yapılandırma

### 5.1 Yeni GPO Oluşturma

![Adım 13](13.png)

**Group Policy Management** konsolunda:

- **Group Policy Objects** → **Sağ tık** → **New**
- **Name**: `Serifselen-All-GPOs`
- **Source Starter GPO**: `(none)`

### 5.2 GPO Düzenleme

![Adım 14](14.png)

**GPO Editor** ile politikaları yapılandırma:

- **Serifselen-All-GPOs** → **Sağ tık** → **Edit**
- **Computer Configuration** → Policies
- **User Configuration** → Policies

### 5.3 Örnek GPO Ayarları

**Finance Departmanı için Özel Politikalar:**

```powershell
# Computer Configuration Policies
- Password Policy
- Account Lockout Policy
- Audit Policy

# User Configuration Policies
- Desktop Restrictions
- Printer Mapping
- Drive Mappings
- Internet Explorer Settings
```

---

## 🏗️ Tamamlanan Active Directory Yapısı

### OU Hiyerarşisi:
```
serifselen.local
└── Selen Holding (OU)
    └── istanbul (OU)
        ├── Groups (OU)
        │   ├── Finance (Security Group - Global)
        │   ├── HR (Security Group - Global)
        │   └── IT (Security Group - Global)
        ├── Users (OU)
        │   ├── Finance (OU)
        │   │   └── Seif SELEN (User)
        │   ├── HR (OU)
        │   └── IT (OU)
        ├── Computers (OU)
        └── Servers (OU)
```

### Grup Üyelikleri:
- **Finance Grubu**: Seif SELEN
- **HR Grubu**: (Sonraki adımda oluşturulacak)
- **IT Grubu**: (Sonraki adımda oluşturulacak)

### GPO Yapılandırması:
- **Serifselen-All-GPOs**: Tüm domain için temel politikalar
- **Finance-GPO**: Finance departmanına özel politikalar (sonraki adım)

---

## 🔄 Sonraki Adımlar için Öneriler

1. **Diğer Departmanları Tamamlama**
   - HR ve IT departmanları için OU, grup ve kullanıcı oluşturma

2. **Gelişmiş GPO Yapılandırması**
   - Departman bazlı özel GPO'lar
   - Güvenlik filtreleme ve WMI filtreleme

3. **Grup Üyelikleri Optimizasyonu**
   - Nesting grupları (grupları gruplara ekleme)
   - Resource grupları oluşturma

4. **Backup ve Recovery Planı**
   - GPO backup'ları alma
   - Active Directory sistem durumu yedekleme

---

## 📊 Kontrol Listesi

- [x] Ana OU yapısı oluşturuldu (Selen Holding)
- [x] Şube OU'su oluşturuldu (istanbul)
- [x] Departman OU'ları oluşturuldu (Groups, Users, Computers, Servers)
- [x] Finance grubu oluşturuldu ve yapılandırıldı
- [x] Örnek kullanıcı oluşturuldu (Seif SELEN)
- [x] Kullanıcı gruba eklendi
- [x] Temel GPO oluşturuldu

---

> 🎯 **Önemli Not:** Bu yapılandırma, **test ortamı** için hazırlanmıştır. Üretim ortamında güvenlik politikaları, yetkilendirme modelleri ve erişim kontrolleri daha detaylı planlanmalıdır.