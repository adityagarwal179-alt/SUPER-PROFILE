# Affiliate Hub: GitHub Sync Setup (free, no backend)

## Kaise kaam karta hai
- Admin panel mein Save karte hi page `data.json` ko GitHub Contents API se aapki repo mein commit karta hai.
- Public page har load par `data.json` padhta hai, isliye sab visitors ko updated data dikhta hai.
- GitHub Pages ko rebuild mein ~30-90 second lagte hain.

## Steps
1. Repo mein `index.html` upload karein (isi file ka naam `index.html` rakhein).
2. GitHub > Settings > Developer settings > Personal access tokens > **Fine-grained tokens** > Generate new token.
   - Repository access: **Only select repositories** > sirf yehi repo
   - Permissions > Repository > **Contents: Read and write**
   - Expiration: jitna chahein (phir renew karna hoga)
3. Page kholen > Admin Login (password wahi purana) > **GitHub Sync**.
   - Owner, repo, branch (usually `main`) bharein, token paste karein.
   - **Test connection** dabayein, phir **Save**.
4. Ab koi bhi offer/profile Save karein. Status "Synced" dikhega.

Token sirf us browser ke localStorage mein rehta hai, file ya repo mein kabhi nahi jaata. Dusre device par ek baar token dobara daalna hoga.

## Zaroori suraksha note
Static site mein admin password check browser mein hota hai, isliye koi bhi source dekh sakta hai. Maine password ko plain text se SHA-256 hash mein badal diya hai, lekin ye sirf dikhawa-level protection hai. **Asli suraksha GitHub token hai**: bina token ke koi bhi repo mein kuch save nahi kar sakta. Purana password ab bhi public file history mein tha, isliye naya password rakhna behtar hai.

Naya password set karne ke liye browser console mein chalayein:
`crypto.subtle.digest("SHA-256",new TextEncoder().encode("NAYA_PASSWORD")).then(b=>console.log([...new Uint8Array(b)].map(x=>x.toString(16).padStart(2,"0")).join("")))`
aur output ko `ADMIN_HASH` mein paste karein.

## Analytics
Analytics abhi bhi sirf us browser ki hoti hai. Sab visitors ki live analytics ke liye free Firebase Realtime Database ka URL `FIREBASE_URL` mein daalein.
