# 📺 IS4-TV — QBCore Television System

> FiveM sunucunuz için gelişmiş televizyon sistemi. YouTube, Twitch, Kick, MP4 ve daha fazlasını destekler.

---

## ⚙️ Gereksinimler

| Bağımlılık | Açıklama |
|---|---|
| `qb-core` | Ana framework |
| `ox_lib` | Bildirim & UI kütüphanesi |
| `oxmysql` | Veritabanı bağlantısı |
| `ox_target` | Hedefleme sistemi |

---

## 🚀 Kurulum (QBCore)

### 1. Klasörü Yerleştir
```
resources/
└── is4-tv/   ← klasörü buraya koy
```

### 2. SQL Dosyasını Çalıştır
`sql_QBCORE.sql` dosyasını veritabanına import et.

### 3. server.cfg'ye Ekle
```cfg
ensure is4-tv
```

### 4. QBCore Items Ekle
`qb-core/shared/items.lua` dosyasına şunları ekle:

```lua
['tvremote']  = {['name'] = 'tvremote',  ['label'] = 'TV Kumandası',   ['weight'] = 500,  ['type'] = 'item', ['image'] = 'tvremote.png',  ['unique'] = false, ['useable'] = true, ['shouldClose'] = true, ['combinable'] = nil, ['description'] = 'TV Kumandası'},
['vehicletv'] = {['name'] = 'vehicletv', ['label'] = 'Araç TV Kiti',   ['weight'] = 1000, ['type'] = 'item', ['image'] = 'vehicletv.png', ['unique'] = false, ['useable'] = true, ['shouldClose'] = true, ['combinable'] = nil, ['description'] = 'Araç için TV kurulum kiti'},
```

### 5. config.lua Ayarları

Tüm önemli ayarlar `config.lua` içinde bulunur. Temel ayarlar:

```lua
Config.Framework            = "qbcore"     -- Framework (değiştirme)
Config.Targettype           = "oxtarget"   -- Hedefleme sistemi
Config.TvForItem            = true         -- Item ile TV açma
Config.TvForCommand         = true         -- Komut ile TV açma (/tv)
Config.EnableImagesForTv    = true         -- Resim desteği
Config.EnableWebsitesForTv  = true         -- Web sitesi desteği
Config.TelevisionWebhook    = false        -- Discord webhook (isteğe bağlı)
```

---

## 🎮 Komutlar

| Komut | Açıklama |
|---|---|
| `/tv` | Yakındaki TV'yi kontrol et |
| `/yayinmodu` | Yayıncı modunu aç/kapat (TV seslerini kapatır) |
| `/getnearbytv [objectname]` | Yakındaki TV koordinatlarını F8 konsoluna yaz |
| `/createcustomtv` | Özel 3D ekran oluştur *(sadece dev sunucusu)* |
| `/tvcreator` | Araç TV offset menüsü *(sadece dev sunucusu)* |

---

## 📡 Desteklenen Platformlar

| Platform | Destekleniyor |
|---|---|
| YouTube | ✅ |
| Twitch | ✅ |
| Kick | ✅ |
| Streamable | ✅ |
| Facebook | ✅ |
| Dailymotion | ✅ |
| Vimeo | ✅ |
| SoundCloud | ✅ |
| Bilibili | ✅ |
| MP4 / MP3 | ✅ |
| Resimler (PNG/GIF/JPG) | ✅ |
| Web Siteleri | ✅ |

---

## 🔔 Bildirim Sistemi

Varsayılan olarak `ox_lib` kullanılmaktadır. Farklı bir sistem kullanmak istersen `config.lua` dosyasının en altındaki `Notify()` fonksiyonunu değiştir:

```lua
function Notify(text)
    -- ox_lib (varsayılan)
    exports.ox_lib:notify({
        title = 'IS4 TV',
        description = text,
        type = 'inform',
        duration = 5000
    })
end
```

---

## 📡 Server Export'ları

```lua
-- TV'yi başlat
exports['is4-tv']:StartTelevision(tvcoords, tvtypeid, volume, routingbucket, controldisabled)

-- TV'de video oynat
exports['is4-tv']:PlayVideoOnTelevision(tvcoords, routingbucket, volume, url)

-- TV sesini değiştir
exports['is4-tv']:ChangeVolumeTelevision(tvcoords, volume, routingbucket)

-- TV'yi durdur
exports['is4-tv']:StopTelevision(tvcoords, routingbucket)
```

---

## 🚗 Araç TV Sistemi

Araç içi TV sistemi için `config.lua` içindeki şu ayarları etkinleştir:

```lua
Config.VehicleTelevision = true                    -- Araç TV sistemi
Config.VehicleTelevisionForEveryVehicle = false    -- Tüm araçlar için (false = listedekiler için)
Config.VehicleTelevisionItem = true                -- Item ile kurulum gerektir
```

Araç offset ayarlamak için dev sunucusunda:
```lua
Config.VehicleTelevisionOffSetsCreator = true      -- /tvcreator komutunu etkinleştirir
```

---

## 🔒 İzin Sistemi

Belirli TV konumlarını izin ile kısıtlamak için:

```lua
Config.TelevisionPermissions = true

Config.TelevisionPermissionsLocations = {
    {
        coords = vector3(320.12, 248.66, 86.56),
        acepermissionsforusecontrolmenu = {enable = true, permission = "is4tv.cinema"},
        jobpermissionsforusecontrolmenu = {enable = false, jobname = "cinema"},
    },
}
```

---

## 🆘 Destek

Sorun yaşarsan sunucu Discord'undan destek alabilirsin.

---

*IS4 Development — QBCore TV System v1.0.0*
