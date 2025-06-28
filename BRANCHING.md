# Git Branch Strategy Rehberi

Bu belge, QrMenu projesinde kullanılacak olan Git dal (branch) stratejisini tanımlar. Amaç, düzenli ve sürdürülebilir bir geliştirme süreci sağlamaktır.

---

## 🔱 Ana Dallar

### `main`
- Üretimde (canlıda) olan kararlı kodu içerir.
- Sadece test edilmiş, yayınlanmaya hazır kodlar bu dala alınır.
- Genellikle `release` veya `hotfix` dallarından merge edilir.

### `develop`
- Aktif geliştirme dalıdır.
- Tüm `feature` ve `bugfix` dalları buraya merge edilir.
- Yayına alınmadan önce buradan `release` dalı çıkarılır.

---

## 🌿 Geçici Dallar

### `feature/*`
- Yeni özellik geliştirmeleri için kullanılır.
- `develop` dalından çıkarılır.
- Geliştirme tamamlandığında tekrar `develop` dalına merge edilir.

**Örnekler:**
- `feature/qr-code-generator`
- `feature/menu-customization`

---

### `bugfix/*`
- Geliştirme ortamındaki hataları düzeltmek için kullanılır.
- `develop` dalından çıkarılır, `develop` dalına merge edilir.

**Örnekler:**
- `bugfix/qr-code-not-generating`
- `bugfix/font-dropdown-crash`

---

### `hotfix/*`
- Yayındaki (production) acil durum düzeltmeleri için kullanılır.
- `main` dalından çıkarılır, hem `main` hem `develop` dallarına merge edilir.

**Örnekler:**
- `hotfix/fix-404-on-menu`
- `hotfix/remove-debug-code`

---

### `release/*`
- Yayın öncesi hazırlık dalıdır.
- `develop` dalından çıkarılır, son testler ve minik düzenlemeler burada yapılır.
- Daha sonra `main` ve `develop` dallarına merge edilir.
- Genellikle `tag` ile sürüm numarası verilir.

**Örnekler:**
- `release/v1.0.0`

---

## 🔄 Pull Request (PR) Süreci

1. Her yeni branch, ilgili ana daldan (genellikle `develop`) oluşturulur.
2. Geliştirme tamamlandığında GitHub üzerinden bir PR (pull request) açılır.
3. PR açıklamasında yapılan değişiklikler özetlenir.
4. Kod gözden geçirilir, test edilir ve merge edilir.

---

## 🧹 Branch Silme Politikası

- Merge edilen `feature/`, `bugfix/`, `release/` ve `hotfix/` dalları hem lokalde hem uzak depoda silinmelidir.
- Lokal: `git branch -d feature/...`
- Uzak: `git push origin --delete feature/...`

---

## 🧠 İyi Uygulamalar

- Anlamlı branch isimleri kullan.
- Her bir commit küçük ve anlamlı olsun.
- PR açıklamalarını açık ve detaylı yaz.
- `main` dalını doğrudan değiştirme.
- `develop` dalını sık sık `main`'den güncel tut.

---

## 🧪 Örnek Akış: Yeni Özellik Ekleme

```bash
git checkout develop
git pull origin develop
git checkout -b feature/menu-customization

# Geliştirme...
git add .
git commit -m "feat: Menü özelleştirme modülü eklendi"
git push -u origin feature/menu-customization

# GitHub'da PR → develop
