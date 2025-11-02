# Active Directory ve DNS Kurulum Rehberi

## Windows Server 2025 Üzerinde AD DS ve DNS Kurulumu

Bu rehber, **Windows Server 2025 Standard Evaluation** sistemine **Active Directory Domain Services (AD DS)** ve **DNS Server** rollerinin adım adım kurulumunu anlatır. Kurulum işlemleri **Server Manager** aracılığıyla yapılır.

---

## 📘 Adım 1: Server Manager Ana Ekranı

Windows Server ilk açıldığında otomatik olarak **Server Manager** ekranı gelir. Sol tarafta **Dashboard**, **Local Server**, **All Servers**, **File and Storage Services** sekmeleri görünür.

📷 *Görsel: Server Manager ana ekranı (Images/01.png)*

Buradan “**Add roles and features**” seçeneğini tıklayarak kuruluma başlıyoruz.

---

## ⚙️ Adım 2: Add Roles and Features Wizard Başlatma

Açılan sihirbaz penceresinde **Before You Begin** ekranı gelir. “**Next**” diyerek devam edilir.

Bu ekran, sunucunun doğru şekilde yapılandırıldığından emin olmanız gerektiğini hatırlatır:

* Statik IP adresi atanmalı,
* Sunucu adı değiştirilmiş olmalı,
* Yönetici hesabı kullanılmalıdır.

📷 *Görsel: Add Roles and Features Wizard (Images/02.png)*

---

## 🧩 Adım 3: Kurulum Türü Seçimi

“**Installation Type**” ekranında **Role-based or feature-based installation** seçeneği işaretlenir.

📷 *Görsel: Role-based or feature-based installation (Images/03.png)*

---

## 🖥️ Adım 4: Hedef Sunucu Seçimi

“**Server Selection**” ekranında kurulumu yapmak istediğiniz sunucuyu seçin. Genellikle bu, yerel sunucudur.

📷 *Görsel: Server Selection (Images/04.png)*

---

## 🏗️ Adım 5: Active Directory Domain Services Rolü Seçimi

“**Server Roles**” ekranında **Active Directory Domain Services** ve **DNS Server** kutucuklarını işaretleyin. Gerekli bağımlılıklar otomatik olarak eklenecektir.

📷 *Görsel: Role Selection (Images/05.png)*

---

## 🌐 Adım 6: Deployment Configuration – Yeni Orman Oluşturma

Kurulum tamamlandıktan sonra, Server Manager’da sağ üstte sarı bir bildirim simgesi belirir. Bu bildirime tıklayarak “**Promote this server to a domain controller**” seçeneğine girilir.

**Deployment Configuration** ekranında:

* **Add a new forest** seçeneği seçilir.
* Yeni bir domain adı (örneğin `dogus.local`) girilir.

📷 *Görsel: New Forest Creation (Images/06.png)*

---

## 🧱 Adım 7: Domain Controller Seçenekleri

Bu adımda Forest ve Domain Functional Level ayarları belirlenir. **Windows Server 2025** varsayılan olarak en yüksek seviyeyi seçer.

Ek olarak:

* **Domain Name System (DNS) server** işaretli kalır.
* **Global Catalog (GC)** varsayılan olarak aktif gelir.
* DSRM (Directory Services Restore Mode) şifresi belirlenir.

📷 *Görsel: DC Options (Images/07.png)*

---

## 🧩 Adım 8: Ön Koşul Denetimi

Kurulumdan önce sistem gerekli kontrolleri yapar. Eğer bir uyarı varsa (“delegation” gibi) göz ardı edilebilir, ancak **hata** varsa düzeltilmelidir.

📷 *Görsel: Prerequisites Check (Images/08.png)*

---

## 🔄 Adım 9: Kurulum İlerleme Durumu

Tüm ön koşullar tamamlandıktan sonra kurulum başlar. Sunucu kurulum sonunda otomatik olarak yeniden başlatılır.

📷 *Görsel: Installation Progress (Images/09.png)*

---

## ⚠️ Adım 10: Post-deployment Yapılandırma Uyarısı

Yeniden başlatma sonrası, Server Manager üzerinde Active Directory ve DNS rollerinin başarıyla yüklendiği görülür.

📷 *Görsel: Roles Installed (Images/10.png)*

---

## 🪟 Adım 11: Windows Tools ve Active Directory Araçlarına Erişim

**Start > Windows Tools** altından aşağıdaki araçlara erişim sağlanır:

* Active Directory Users and Computers
* DNS Manager
* Group Policy Management

📷 *Görsel: Windows Tools listesi (Images/11.png)*

---

## 👥 Adım 12: Active Directory Users and Computers Arayüzü

Bu araç, kullanıcılar, bilgisayarlar, gruplar ve Organizational Unit (OU) yapısını yönetmek için kullanılır.

📷 *Görsel: ADUC ana ekranı (Images/12.png)*

---

## 🗂️ Adım 13: Yeni Öğe Oluşturma Menüsü

**Domain adınız** üzerinde sağ tıklayıp “**New > Organizational Unit**” seçeneğini seçin.

📷 *Görsel: OU oluşturma menüsü (Images/13.png)*

---

## 🏢 Adım 14: İlk Organizational Unit (OU) Oluşturma

Örneğin “**DogusUsers**” adlı bir OU oluşturun. Bu OU içinde departman bazlı alt OU’lar oluşturulacaktır.

📷 *Görsel: OU oluşturuldu (Images/14.png)*

---

## 🧩 Adım 15: Alt Organizational Unit Oluşturma

“DogusUsers” altında örneğin “**IT**, **HR**, **Finance**, **Students**” alt OU’larını oluşturun.

📷 *Görsel: Alt OU yapısı (Images/15.png)*

---

## 🏗️ Adım 16: Detaylı OU Yapısı ve Departman Organizasyonu

Tam OU yapısı örneği:

```
dogus.local
 ├── DogusUsers
 │   ├── IT
 │   ├── HR
 │   ├── Finance
 │   └── Students
 ├── DogusComputers
 └── DogusGroups
```

📷 *Görsel: OU Tree (Images/16.png)*

---

## 👤 Adım 17-18: Güvenlik Grubu Oluşturma

**DogusGroups** OU’su üzerinde sağ tıklayıp “**New > Group**” seçeneğini seçin.

Grup tipi: **Security**, Kapsam: **Global** olarak ayarlanır.
Örnek grup: `ITAdmins`

📷 *Görsel: Grup oluşturma ekranı (Images/17.png)*

---

## 🙍‍♂️ Adım 19-21: Kullanıcı Hesabı Oluşturma

Her departman altına kullanıcılar eklenir:

* Sağ tık → **New > User**
* Ad, Soyad ve Kullanıcı Adı girilir.
* Şifre oluşturulur.
* “User must change password at next logon” işaretli kalabilir.

📷 *Görsel: Yeni kullanıcı oluşturma (Images/18.png)*

---

## 👥 Adım 22-23: Gruba Üye Ekleme

Kullanıcıyı gruba eklemek için:

* Grubu aç → **Members** sekmesi → **Add...**
* Kullanıcı adını girip doğrulayın.

📷 *Görsel: Group Membership ekranı (Images/19.png)*

---

## 🧭 Adım 24: Group Policy Management Konsolu

**Windows Tools > Group Policy Management** aracılığıyla grup ilkeleri (GPO) yönetilir.
Yeni bir GPO oluşturmak için:

* OU üzerine sağ tık → **Create a GPO in this domain, and Link it here...**

📷 *Görsel: GPO oluşturma (Images/20.png)*

---

## 💡 Kurulum Sonrası Öneriler

* DNS kayıtlarını `nslookup` ile test edin.
* GPO’ları düzenleyip temel güvenlik ayarlarını uygulayın.
* `repadmin /replsummary` komutu ile replikasyon durumunu kontrol edin.

---

## 🧠 En İyi Uygulamalar

* Her departman için ayrı OU yapısı oluşturun.
* Servis hesaplarını ayrı bir OU’da yönetin.
* GPO’ları **test** OU’sunda denemeden prod ortamına taşımayın.
* Kullanıcı şifre politikalarını merkezî GPO ile yönetin.

---

## 💻 Yaygın PowerShell Komutları

```powershell
# Yeni kullanıcı oluşturma
New-ADUser -Name "Ahmet Yılmaz" -SamAccountName ayilmaz -Path "OU=IT,OU=DogusUsers,DC=dogus,DC=local" -AccountPassword (Read-Host -AsSecureString "Şifre") -Enabled $true

# Kullanıcıyı gruba ekleme
Add-ADGroupMember -Identity "ITAdmins" -Members "ayilmaz"

# OU oluşturma
New-ADOrganizationalUnit -Name "Finance" -Path "OU=DogusUsers,DC=dogus,DC=local"

# Domain ve forest seviyelerini listeleme
Get-ADForest | Select ForestMode
Get-ADDomain | Select DomainMode
```

---

## 📄 Doküman Bilgileri

**Hazırlayan:** Şerif Selen
**Sürüm:** 1.2 (Kasım 2025)
**Platform:** Windows Server 2025 Standard Eval
**Amaç:** AD DS + DNS kurulumu ve temel yapılandırma rehberi
