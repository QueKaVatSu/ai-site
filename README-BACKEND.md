# AI Coding Assistant – Backend Proxy (Free)

Bu sürümde istemci tarafında **token/model sorma yok**. Frontend, `/api/generate` endpoint'ine istek atar.
Aşağıdaki iki ücretsiz seçenekten biriyle dağıtabilirsin:

## Seçenek A — Vercel (ücretsiz katman)
1. Bu klasörü bir Git deposuna push et.
2. Vercel'de yeni proje oluştur → bu repo.
3. **Environment Variables** ekle:
   - `HF_TOKEN` = Hugging Face Read token'ınız (hf_...)
   - (opsiyonel) `HF_MODEL` = `HuggingFaceH4/zephyr-7b-beta`
4. Deploy et. Vercel `vercel.json` sayesinde `/api/generate` çalışır.
5. Frontend (builder.html) otomatik `/api/generate`'e POST atar.

## Seçenek B — Cloudflare Workers (ücretsiz)
1. Cloudflare hesabında **Workers & Pages** → **Create Worker**.
2. Bu repo dosyalarını yükle / bağla.
3. **Vars** ekle:
   - `HF_TOKEN` (Secret)
   - `HF_MODEL` (Text) = `HuggingFaceH4/zephyr-7b-beta`
4. `wrangler.toml` bu repo kökünde olmalı. Deploy et.
5. Worker URL'niz `https://<worker>.workers.dev` olur; frontend'de `/api/generate` çağrısını bu URL'e yönlendirmek için builder.js içinde endpoint'i değiştirin.

## Güvenlik
- Token **sadece sunucu ortam değişkenlerinde** tutulur, istemci tarafında görünmez.
- İstersen rate-limit / CORS domain kısıtı ekleyebilirsin.



---

## Hızlı dağıtım (env'siz)
Bu pakette HF token backend koduna gömülüdür; Vercel veya Cloudflare Workers'a ek ENV tanımlamadan deploy edebilirsin.

- **Vercel:** Projeyi import et → Deploy (vercel.json rota tanımlı).  
- **Cloudflare Workers:** Worker oluştur → bu repo dosyalarını yükle/deploy et.  
  Frontend `/api/generate` yerine Worker URL'ini kullanmak istersen `assets/js/builder.js` içindeki endpoint'i değiştir.

> Not: Üretimde gizli anahtarları env değişkenleriyle tutman önerilir.
