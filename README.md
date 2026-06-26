# Theme TKKP for Moodle 4.5

**TKKP** adalah tema Moodle modern berbasis [Boost](https://docs.moodle.org/en/Boost_theme) (Bootstrap 5) yang dirancang untuk tampilan bersih, aksesibel, dan mudah dikustomisasi.

## Fitur Utama

- **Berbasis Boost** — mewarisi semua fitur inti Moodle 4.5 Boost (responsive, drawer navigasi, dark mode ready).
- **Accessibility Bar** — toolbar aksesibilitas untuk mengatur ukuran font dan warna situs, memudahkan pengguna dengan kebutuhan visual khusus.
- **Font OpenDyslexic** — dukungan font khusus untuk pengguna disleksia.
- **Custom Login Page** — halaman login dengan background image yang dapat dikonfigurasi.
- **Brand Color** — warna utama, warna menu sekunder, dan font dapat diatur dari admin tema tanpa menyentuh kode.
- **Template Override** — override template Mustache untuk navbar, footer, drawer, course card, user menu, dan lainnya.
- **SCSS Modular** — stylesheet terstruktur dengan partial per komponen, mudah di-maintain.

## Persyaratan

| Komponen  | Versi                 |
|-----------|-----------------------|
| Moodle    | 4.5 atau lebih baru   |
| PHP       | 8.1+                  |
| Node.js   | 18+ (untuk build dev) |
| npm/Grunt | Untuk kompilasi SCSS  |

## Instalasi

1. Download atau clone repositori ini ke dalam direktori tema Moodle:
   ```
   /path/to/moodle/theme/tkkp/
   ```

2. Login sebagai admin Moodle, buka:
   **Site administration → Appearance → Themes → Theme selector**

3. Pilih tema **TKKP** dan klik **Use theme**.

4. Atur konfigurasi tema di:
   **Site administration → Appearance → Themes → TKKP**

## Konfigurasi

| Pengaturan           | Keterangan                                              |
|----------------------|---------------------------------------------------------|
| `brandcolor`         | Warna utama brand (hex, default: `#0f47ad`)             |
| `secondarymenucolor` | Warna menu sekunder (default: mengikuti brand color)    |
| `fontsite`           | Font utama situs                                        |
| `loginbgimg`         | Gambar background halaman login                         |
| `logo`               | Logo situs                                              |
| `favicon`            | Favicon situs                                           |
| `scss`               | SCSS tambahan (raw SCSS dari admin)                     |
| `scsspre`            | SCSS yang di-prepend sebelum compile                    |

## Pengembangan

### Setup

```bash
# Clone repositori ke direktori tema Moodle
git clone <repo-url> /path/to/moodle/theme/tkkp

# Install dev dependencies
cd /path/to/moodle/theme/tkkp
npm install
```

### Struktur SCSS

```
scss/
├── default.scss          # Entry point, import semua partial
└── tkkp/
    ├── _variables.scss   # Variabel warna & brand — edit di sini untuk theming
    ├── _general.scss
    ├── _navbar.scss
    ├── _footer.scss
    ├── _course.scss
    ├── _login.scss
    ├── _accessibilitybar.scss
    └── ...
```

Untuk menambah style baru:
1. Buat file `scss/tkkp/_nama-komponen.scss`
2. Import di `scss/default.scss`
3. Gunakan variabel dari `_variables.scss`

### Grunt Tasks

```bash
grunt              # Mode watch (auto reload saat file SCSS berubah)
grunt amd          # Compile AMD JavaScript
grunt css          # Lint SCSS & CSS
grunt decache      # Purge Moodle cache
grunt compile      # Compile JS + purge cache
```

### Menambah Template Override

Tempatkan file Mustache di direktori `templates/` sesuai namespace Moodle:

```
templates/
├── core/              # Override template inti Moodle
├── core_course/       # Override template kursus
├── block_myoverview/  # Override blok myoverview
└── ...
```

## Struktur Template

| Template                                    | Keterangan                          |
|---------------------------------------------|-------------------------------------|
| `drawers.mustache`                          | Layout utama dengan sidebar drawer  |
| `navbar.mustache`                           | Navigation bar atas                 |
| `footer.mustache`                           | Footer halaman                      |
| `frontpage.mustache`                        | Layout halaman depan                |
| `login.mustache`                            | Layout halaman login                |
| `course.mustache`                           | Layout halaman kursus               |
| `accessibilitybar.mustache`                 | Toolbar aksesibilitas               |
| `core/full_header.mustache`                 | Override header utama               |
| `core/loginform.mustache`                   | Override form login                 |
| `block_myoverview/view-cards.mustache`      | Override tampilan card kursus       |

## Lisensi

Tema ini dirilis di bawah lisensi [GNU General Public License v3.0 atau lebih baru](LICENSE.md).

## Author

**Yohan Naftali** — [yohanli.com](https://yohanli.com)

---

*Kompatibel dengan Moodle 4.5. Dikembangkan berdasarkan tema Boost dengan inspirasi dari tema Moove.*
