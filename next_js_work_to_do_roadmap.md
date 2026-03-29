PHase 1-2 practicle...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 1: Core Concepts & Rendering Evolution → Level 1.1: React vs Next.js - The "Meta-Framework" Concept [🟢 Beginner]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
React ek UI library hai — sirf screen dikhana. Next.js ek framework hai jo React ke upar routing, SSR, aur tooling provide karta hai.

2. 💥 Why? (Production Impact)
- Pure React project mein SEO bekar hota hai — Google bot ko khaali HTML dikhta hai.
- Routing ke liye extra library (`react-router-dom`) install karni padti hai.
- Next.js in sabko built-in deta hai, plus performance optimizations.

3. 🎯 Practical Tasks (The Mission)

Task 1: Compare initial HTML output between React (CRA) and Next.js
The Logic: React ka default HTML sirf `<div id="root"></div>` bhejta hai, baaki JS se render hota hai. Next.js server pe HTML generate karta hai. Tujhe dono tools se ek naya project create karna hai aur "View Page Source" (Ctrl+U) mein fark dekhna hai.

Task 2: Identify where routing logic lives
The Logic: React mein tum `react-router-dom` ka `<Routes>` aur `<Route>` component manually likhte ho. Next.js mein routing file-system based hai — folder structure hi URL decide karta hai. Tujhe ek Next.js project mein `app/about/page.tsx` banana hai aur check karna ki `/about` route automatically kaam karta hai ya nahi.

Task 3: Find what "Meta-Framework" means in practice
The Logic: Meta-framework ka matlab — Next.js React ko wrap karta hai aur additional capabilities (SSR, SSG, API routes) deta hai. Tujhe Next.js documentation mein "Features" section padhna hai aur 3 cheezein list karni hai jo pure React mein nahi hoti.

🔥 THE COMBO TASK:
Ek naya Next.js project bana (`npx create-next-app` wala command yaad hai?), usme `app/test/page.tsx` bana, usme ek simple `<h1>` daal. Fir `npm run dev` se server start kar, browser mein `/test` open kar, right-click → "View Page Source". Jo HTML dikhta hai, usme tera `<h1>` tag dikhna chahiye. Ab same cheez ek pure React project (Vite wala) mein kar ke compare kar. Dono ke source code ka fark likh.

4. ✅ Definition of Done (Verification — "Kaise pata chalega success hua?")
- Next.js ke page source mein tera `<h1>` tag directly dikhta hai (without any `#root` placeholder).
- React (CRA/Vite) ke page source mein sirf `<div id="root"></div>` dikhta hai, actual content JS ke through aata hai.
- Tune apne notes mein likha ki Next.js 3 built-in features provide karta hai (e.g., routing, SSR, API routes).

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords is level mein:**
- **`create-next-app`** : CLI tool jo boilerplate banata hai. Internal logic — ye npm registry se latest template fetch karta hai aur dependencies install karta hai. Miss kiya toh manually setup karna padega jo time-consuming hai.
- **File-system routing** : Next.js `app/` folder ke andar jo folder aur `page.tsx` hota hai, wahi URL path ban jata hai. Internal — server build time par folder structure scan karta hai aur route mappings generate karta hai.
- **View Page Source** : Ye browser feature hai jo raw HTML dikhata hai. Next.js SSR/SSG ki wajah se yahan content dikhta hai, jo SEO ke liye critical hai. Agar yahan content nahi dikhta, toh Google bot use index nahi karega.

**Hint snippet (sirf samajhne ke liye — type karna khud):**
```bash
# Next.js project mein page source check karne ka tareeqa:
# Browser mein page kholo → Right click → "View Page Source"
# Ctrl+F karke apne <h1> ka text search karo.
```
**Miss kiya toh kya hoga?** Agar tu pure React ko Next.js samajh ke deploy karega, toh website Google search mein nahi aayegi — SEO dead.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 1: Core Concepts & Rendering Evolution → Level 1.2: CSR vs SSR vs SSG vs ISR [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Rendering decide karta hai ki HTML kab aur kahan banega. CSR = browser mein, SSR = har request par server pe, SSG = build time pe ek baar, ISR = time interval par background mein update.

2. 💥 Why? (Production Impact)
- CSR: Slow initial load, bad SEO — but cheap server costs.
- SSR: Always fresh data, but server load high — use for user-specific pages (cart, dashboard).
- SSG: Blazing fast, but data stale — use for blogs, docs.
- ISR: Best of both — fast + periodic fresh.

3. 🎯 Practical Tasks (The Mission)

Task 1: Simulate CSR by disabling JavaScript in browser
The Logic: CSR wali site JS band karne par completely blank ho jati hai. Tujhe browser dev tools mein "Disable JavaScript" ka option dhundhna hai, phir kisi popular React site (e.g., old Twitter) aur Next.js site (e.g., vercel.com) pe jaake fark dekhna.

Task 2: Identify SSR behavior using `cache: 'no-store'`
The Logic: Next.js App Router mein default fetching `force-cache` (SSG) hota hai. Agar `cache: 'no-store'` use karega, toh har request server se fresh data aayega (SSR). Tujhe ek API route banana hai jo current timestamp return kare, aur page mein us timestamp ko dikhana hai with `no-store`. Refresh karne par timestamp change hona chahiye.

Task 3: Observe SSG with `force-cache`
The Logic: Build time pe (`npm run build`) Next.js static pages generate karta hai. Tujhe ek page banana hai jo random number return kare lekin `force-cache` use kare. Build karke `next start` se run kar. Multiple refreshs par same number aana chahiye.

Task 4: Implement ISR using `next: { revalidate: 10 }`
The Logic: ISR mein pehle stale cache dikhata hai, phir background mein revalidate hota hai. Tujhe ek page banana hai jisme `fetch` ke andar `next: { revalidate: 10 }` use karna hai. 10 seconds ke andar refresh karne par same data dikhega, 10 seconds baad naya data aayega.

🔥 THE COMBO TASK:
E-commerce product page bana. Maan le product price API se aati hai jo har 5 minute mein change hoti hai (flash sale). Tujhe `revalidate: 300` (5 min) ka ISR implement karna hai. Pehle page load kar, price note kar. 5 minute baad refresh kar — price update hona chahiye bina full rebuild ke. Fir terminal mein `next build` ke output mein dek ki us page ke liye static file generate hui ya nahi.

4. ✅ Definition of Done (Verification)
- SSR page: Har refresh pe timestamp change hota hai.
- SSG page: Build ke baad har refresh pe same random number aata hai (browser cache clear karne ke baad bhi).
- ISR page: 10 seconds ke andar same data, 10 seconds baad naya data (background update, pehle purana dikhega phir agle request pe naya).
- Tune build output mein static pages ki list dekhi.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords:**
- **`cache: 'no-store'`** : Fetch API ka flag. Internal — response headers mein `Cache-Control: no-store` add karta hai, server ko force karta hai ki har request pe naya data laaye. Miss kiya toh stale data dikhega jo real-time apps ke liye dangerous hai.
- **`force-cache`** : Default behavior. Internal — response ko build time ya first request pe cache kar leta hai, baad ki requests cache se serve hoti hain.
- **`next: { revalidate: seconds }`** : ISR ka magic. Internal — page serve karte time check karta hai ki last revalidate time se zyada ho gaya? Agar haan, toh background mein naya generate karta hai, par user ko stale version dikhata hai (fast response). Miss kiya toh static site kabhi update nahi hogi.
- **`npm run build` output** : Terminal mein likha hota hai "○ (Static)" ya "λ (Server)". Ye batata hai kaunsa rendering mode use hua.

**Hint snippet (sirf samajhne ke liye):**
```ts
// SSR wala page example (syntax hint, exact code nahi copy karna)
export default async function Page() {
  const res = await fetch('https://api.time.com', { cache: 'no-store' });
  const data = await res.json();
  return <div>{data.now}</div>;
}
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 1: Core Concepts & Rendering Evolution → Level 1.3: RSC (React Server Components) – The Conceptual Shift [🔴 Advanced]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
React Server Components sirf server pe execute hote hain, unka JavaScript browser tak nahi pahunchta. Zero bundle size, direct database access.

2. 💥 Why? (Production Impact)
- Pehle React ka saara JS client pe download hota tha → heavy bundle.
- RSC se non-interactive parts server pe reh jate hain → page load time kam.
- Server components directly database ya file system access kar sakte hain — backend logic frontend mein.

3. 🎯 Practical Tasks (The Mission)

Task 1: Identify which components are Server by default
The Logic: Next.js App Router mein har component default Server Component hai, jab tak top pe `"use client"` nahi likhte. Tujhe ek naya component banake usme `console.log` daalna hai. Terminal mein log dikhega (server side), browser console mein nahi. Isse confirm ho jayega.

Task 2: Try to use `useState` in a Server Component
The Logic: Server components React hooks (useState, useEffect) support nahi karte. Tujhe ek file bina `"use client"` ke bana, usme `useState` import kar aur use kar. Next.js error dega — exact error message note kar.

Task 3: Create a Client Component with `"use client"`
The Logic: Ek alag component file bana, sabse pehli line mein `"use client"` likh. Usme `useState` se ek counter implement kar. Is component ko apne Server Component page mein import kar. Browser console mein check kar ki JS download hua ya nahi (Network tab mein .js file).

Task 4: Pass data from Server Component to Client Component
The Logic: Server component database se data fetch kar sakta hai (maan le ek products array). Us data ko props ke through client component mein bhej. Client component sirf display karega — usme fetching logic nahi. Tujhe aisa pattern implement karna hai.

🔥 THE COMBO TASK:
Ek product listing page bana. Server component mein `fetch` se products la (mock API use kar). Fir ek "Add to Cart" button bana jo ek Client component hai. Button click karne par console log kare "Added". Dhyan rakh: Button ko product ID prop pass karna Server component se. Is pattern mein fetching server pe hoti hai, interactivity client pe. Execute kar aur Network tab mein dek ki product list ka JS bundle size zero hai ya nahi.

4. ✅ Definition of Done (Verification)
- Server component ka `console.log` terminal mein dikhta hai, browser console mein nahi.
- `useState` wala component bina `"use client"` ke error deta hai: "You're importing a component that needs useState. Add 'use client'."
- Client component ka JS file Network tab mein dikhta hai (e.g., `page.js` chunk).
- Product list HTML source mein visible hai, lekin "Add to Cart" button click karne par console message aata hai.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords:**
- **`"use client"`** : Directive jo React ko batati hai ki ye component client boundary hai. Internal — is directive ke baad ka poora subtree client pe render hoga aur uska JS bundle browser bheja jayega. Miss kiya toh hooks use nahi kar sakte.
- **RSC Payload** : Server components ka output — ye ek special JSON-like format hota hai jisme HTML aur placeholders hote hain. Client is payload ko parse karta hai aur tree reconstruct karta hai.
- **Zero bundle size** : Server component ka code kabhi browser tak nahi aata. Internal — webpack/ Turbopack build time par un components ko exclude kar deta hai client bundle se. Miss kiya toh (sab kuch client bana diya) performance barbaad.
- **Async Server Component** : Server components `async` ho sakte hain, direct `await` fetch kar sakte hain. Internal — React server renderer async components ko resolve karta hai before sending payload.

**Hint snippet (sirf samajhne ke liye):**
```tsx
// Server component (no "use client")
export default async function ProductList() {
  const products = await fetch('https://api.products.com').then(r => r.json());
  return <div>{products.map(p => <ProductCard key={p.id} product={p} />)}</div>
}
// Client component
"use client";
export function AddToCartButton({ id }) { 
  return <button onClick={() => console.log(id)}>Add</button> 
}
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 1: Core Concepts & Rendering Evolution → Level 1.4: Next.js 15/16 Specifics – Turbopack, Compiler, Caching [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Turbopack (Rust-based bundler) Webpack ki jagah le raha hai — 10x faster dev startup. React 19 Compiler automatic memoization karta hai (no manual `useMemo`). File-system caching build artifacts ko store karta hai.

2. 💥 Why? (Production Impact)
- Purane projects mein `npm run dev` mein 3-5 second lagte the. Turbopack se under 200ms.
- `useMemo` aur `useCallback` likhna bhool jane se app slow hoti thi. Ab compiler khud optimise karta hai.
- Server restart (e.g., config change) pe purana cache reuse hota hai, fast recovery.

3. 🎯 Practical Tasks (The Mission)

Task 1: Enable Turbopack in your Next.js project
The Logic: `package.json` ki `"dev"` script mein `--turbo` flag add karna hai. Phir `npm run dev` run kar. Terminal mein dekha "ready in XXms" — compare karega bina turbo ke kitna time lagta tha (pehle project delete karke naya banake bina turbo check kar sakta hai). 

Task 2: Verify React Compiler is working (automatic memoization)
The Logic: Next.js 15+ mein React Compiler experimental hai, but default on hai kuch versions mein. Tujhe ek component banana hai jisme ek child component pure props leta hai (no state change). Parent re-render hota rahega (e.g., with `useState` timer). Compiler automatic memoization ki wajah se child unnecessary re-render nahi hoga. `console.log` in child se check kar.

Task 3: Observe file-system caching during dev server restart
The Logic: `next dev` run kar, phir `next.config.ts` mein kuch change kar (e.g., ek comment add). Server restart hoga. Second time restart fast hota hai kyunki `.next/cache` folder mein artifacts store ho gaye. Tujhe `.next/cache` folder explore karna hai aur dekna hai kaunsi files bani.

Task 4: Compare build times with and without Turbopack (for production)
The Logic: Turbopack abhi production build (`next build`) mein bhi stable hai (Next.js 16). Tujhe do baar build karni hai — ek baar normal, ek baar `--turbo` flag ke saath? Actually Turbopack build ke liye alag flag hota hai `next build --turbo`. Time difference measure kar.

🔥 THE COMBO TASK:
Ek large component tree bana (10 nested components). Har component mein ek expensive calculation daal (e.g., fibonacci(30) recursively). React Compiler automatically memoize karega. Tujhe React DevTools "Profiler" use karna hai to measure render times. Fir React Compiler disable karne ka tareeqa dhundh (next.config.ts mein `compiler: { reactCompiler: false }`) aur phir compare kar. Output: Profiler screenshots ya numbers.

4. ✅ Definition of Done (Verification)
- `npm run dev --turbo` chalane par terminal "ready in <200ms" dikhata hai.
- Child component ka console.log parent re-render hone par nahi aata (compiler magic).
- `.next/cache` folder exists aur usme files hain.
- Build time with turbo < build time without turbo (at least 20% faster).

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords:**
- **`--turbo` flag** : Next.js CLI flag jo Turbopack bundler enable karta hai. Internal — Rust-based incremental computation engine, sirf changed files process hoti hain. Miss kiya toh Webpack use hoga, slow.
- **React Compiler** : Build-time tool jo code ka analysis karta hai aur automatically `useMemo`/`useCallback` insert karta hai. Internal — ek custom Babel plugin jo dependencies track karta hai. Miss kiya toh developer ko manually memoize karna padega, chances of mistakes high.
- **`.next/cache` folder** : Build artifacts, webpack cache, font optimization cache. Internal — Next.js file-system cache use karta hai taaki rebuilds fast ho. Miss kiya (e.g., cache delete kar diya) toh full rebuild hoga.
- **Fast Refresh** : Turbopack ke saath HMR (Hot Module Replacement) bahut fast hota hai. Internal — websocket connection pe updated module inject hota hai without losing component state.

**Hint snippet (sirf samajhne ke liye):**
```json
// package.json
"scripts": {
  "dev": "next dev --turbo",
  "build": "next build --turbo"
}
```
```js
// next.config.ts me compiler disable karna
const nextConfig = {
  experimental: {
    reactCompiler: false
  }
}
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🏁 MODULE 1 RECAP — Tera Status Report
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
**Siksha Summary:**
- ✅ React vs Next.js ka real difference — page source dekh ke pehchan sakta hai ab tu.
- ✅ 4 rendering strategies (CSR, SSR, SSG, ISR) ko implement kar ke samajh liya.
- ✅ RSC ka zero-bundle-size magic — server component aur client component ka separation clear hai.
- ✅ Next.js 15/16 ke latest tools (Turbopack, Compiler) se dev speed boost.

**Guru-ji's Warning:**
"Check kar le bhai! Kya tujhe yeh sab bina cheat sheet ke karna aa gaya hai? Level 1.3 mein RSC ka async fetch aur client component mein prop passing — agar dubara karega toh bina error ke hoga? Agar ek bhi cheez mein doubt hai, toh chup chaap peeche ja aur wapas execute kar. Aage badhne ka koi fayda nahi agar basics hile hue hain!"

---
--- ⏸️ OUTPUT LIMIT APPROACHING. Type 'CONTINUE' to get the next part (Module 2: Project Setup).
✅ Completed so far : Level 1.1, 1.2, 1.3, 1.4 (Module 1 complete)
⏳ Remaining       : Module 2 (Levels 2.1, 2.2, 2.3) and Module 3 (Levels 3.1 to 3.8)
📊 Progress        : 4 Levels done / 15 Levels total | Module 1 of 3

========================================================================================


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 2: Project Setup → Level 2.1: Initialization – `npx create-next-app` [🟢 Beginner]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
`create-next-app` Vercel ka official CLI hai jo ek command mein Next.js project boilerplate generate karta hai — TypeScript, Tailwind, ESLint, App Router sab pre-configured.

2. 💥 Why? (Production Impact)
- Manual setup mein version mismatches aur config errors aate hain.
- `create-next-app` sab dependencies ko compatible versions mein install karta hai.
- Industry standard — har professional project yahi se start hota hai.

3. 🎯 Practical Tasks (The Mission)

Task 1: Run the create-next-app command with specific choices
The Logic: CLI tumse kuch questions poochta hai. Tujhe `npx create-next-app@latest` chalana hai aur ye answers select karne hain: TypeScript = Yes, ESLint = Yes, Tailwind CSS = Yes, `src/` directory = Yes, App Router = Yes, import alias default = No. Terminal ka exact output observe kar.

Task 2: Verify the generated folder structure
The Logic: Project banne ke baad `cd` kar aur `ls` (or `dir` on Windows) se dekh. `package.json` mein dependencies list hai — check kar ki `next`, `react`, `react-dom`, `tailwindcss`, `typescript` sab present hain. `src/` folder exist karta hai ya nahi? (Yes, tu ne select kiya tha).

Task 3: Start the dev server and visit the default page
The Logic: `npm run dev` se server start. Browser mein `http://localhost:3000` khol. Default Next.js welcome page dikhta hai (tailwind-styled). `src/app/page.tsx` ko modify kar ke "Hello CTF" likh. Browser automatically refresh hona chahiye (Fast Refresh).

Task 4: Understand what each generated file does
The Logic: Project root mein `next.config.ts` — ye Next.js server config. `tsconfig.json` — TypeScript config. `postcss.config.js` — Tailwind ke liye. `src/app/layout.tsx` — root layout. Tujhe har file ke ek line explanation apne words mein likhni hai.

🔥 THE COMBO TASK:
Ek naya project `my-ctf-app` naam se bana (agar pehle se hai toh delete kar). Sahi answers select kar. Phir us project mein `src/app/guru/page.tsx` bana, usme ek `<h1>` daal "Guru-ji ka CTF". Ab `npm run build` command chala. Build ke baad terminal mein `next start` se production server run kar. `/guru` route visit kar. Production build mein static page generate hua ya server? Build output mein `○` (static) ya `λ` (server) ka symbol dekha? Note kar.

4. ✅ Definition of Done (Verification)
- Terminal mein "Success! Created my-ctf-app" jaisa message dikha.
- `src/` folder exists and usme `app/` hai.
- `npm run dev` chalne ke baad browser `localhost:3000` pe content dikha.
- Build output mein `/guru` page ke liye `○` ya `λ` ka symbol pahchan liya.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords:**
- **`npx`** : Node package execute — bina globally install kiye package chalata hai. Internal — npm registry se package download karta hai temporary cache mein. Miss kiya toh globally install karna padega jo version conflicts create kar sakta hai.
- **`create-next-app`** : Ye ek npm package hai jo template repository clone karta hai. Internal — degit (GitHub template downloader) use karta hai. Flags jaise `--ts`, `--tailwind` direct options provide karte hain.
- **`src/` directory** : Source code ko config files se alag rakhne ke liye. Internal — Next.js automatically `src/` ko root treat karta hai. Miss kiya toh `app/` root mein aayega, config files ke saath mix ho jayega.
- **`npm run dev` vs `next start`** : Dev server mein hot reload aur source maps hote hain. Production server mein minified code aur caching hoti hai. Internal — dev mode mein webpack/ Turbopack watch mode mein chalta hai.

**Hint snippet (sirf samajhne ke liye — exact command nahi dena, lekin bata raha hoon):**
Tujhe `npx create-next-app@latest my-app` run karna hai. Options select karte waqt arrow keys se navigate aur Enter se confirm.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 2: Project Setup → Level 2.2: Folder Structure Strategy (Production Grade) [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
`src/` ke andar: `app/` sirf routing ke liye, `components/` (further `ui/` and `features/`), `lib/` (utilities, API clients), `types/` (TypeScript interfaces), `utils/` (helper functions).

2. 💥 Why? (Production Impact)
- Bina structure ke project bada hone par files kho jati hain — "spaghetti code".
- Clean structure se team collaboration aasan hota hai.
- `components/ui` mein reusable dumb components, `features` mein smart business-logic components.

3. 🎯 Practical Tasks (The Mission)

Task 1: Create the recommended folder structure inside `src/`
The Logic: Terminal mein `src/` ke andar ye folders bana: `components`, `lib`, `types`, `utils`. Phir `components` ke andar do aur folders: `ui` aur `features`. Commands: `mkdir`, `cd` use karne honge. Exact syntax nahi bata raha — figure out kar.

Task 2: Create a reusable Button component in `components/ui/Button.tsx`
The Logic: Button ek "dumb" component hai — sirf props leta hai (children, onClick, variant). Isme koi API call ya complex logic nahi. TypeScript mein interface define kar `ButtonProps`. Default export karna mat bhool.

Task 3: Create a feature component `ProductCard` in `components/features/ProductCard.tsx`
The Logic: Ye component thoda smart hai — accept product object as prop, display name, price, and a "Buy" button (jo imported Button component use kare). Isme logic ho sakta hai — e.g., price format karna.

Task 4: Move a utility function to `utils/formatPrice.ts`
The Logic: Ek function likh `formatPrice(price: number): string` jo `$123.45` format mein return kare. Export karo. Phir `ProductCard` mein import karke use karo.

🔥 THE COMBO TASK:
`src/app/page.tsx` mein teen ProductCard components render kar, alag-alag products ke saath. Button click karne par console log "Added to cart" karna hai (client component banane ki zaroorat hai — ya fir product card ko client banao? Socho). Folder structure maintain karte hue implement kar. Production-grade structure ready hai — ab tu bata ki `lib/` folder mein kya rakhega? (Hint: database connection, API client setup)

4. ✅ Definition of Done (Verification)
- `tree src/` command (or `ls -R` on Mac/Linux) se folder structure visible hai.
- `Button.tsx` successfully imported in `ProductCard.tsx` without relative path hell (use `@/components/ui/Button`).
- `formatPrice` function kaam kar raha hai — price properly formatted.
- Page render ho raha hai with 3 product cards.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords:**
- **Path alias `@/`** : `tsconfig.json` mein define hota hai `"paths": { "@/*": ["src/*"] }`. Internal — TypeScript compiler aur Next.js resolver is alias ko expand karta hai. Miss kiya toh imports `../../../` jaise honge jo refactor karna mushkil.
- **Dumb vs Smart components** : Dumb (ui/) sirf props render karte hain, koi side effects nahi. Smart (features/) business logic, API calls, state manage karte hain. Internal — smart components dumb components ko compose karte hain.
- **`lib/` folder** : Third-party configurations (e.g., `prisma.ts`, `axios.ts`). Ye components se alag isliye rakhte hain taaki ek jagah change karo toh sab jagah effect ho. Miss kiya toh config logic components mein fail jayegi — duplication.
- **Barrel exports** : `components/ui/index.ts` mein sab components re-export kar sakte ho. Internal — index file import paths ko shorten karta hai.

**Hint snippet (sirf samajhne ke liye):**
```ts
// src/components/ui/Button.tsx
interface ButtonProps { children: React.ReactNode; onClick?: () => void; variant?: 'primary' | 'secondary'; }
export default function Button({ children, onClick, variant = 'primary' }: ButtonProps) { ... }
```
Tujhe khud type karna hai — copy mat kar.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 2: Project Setup → Level 2.3: Configuration – `next.config.ts` + `tsconfig` Path Aliases [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
`next.config.ts` Next.js server ko configure karta hai — images domains, rewrites, headers. `tsconfig.json` TypeScript compiler aur path aliases set karta hai.

2. 💥 Why? (Production Impact)
- External images ke liye `remotePatterns` set karna mandatory hai — nahi kiya toh `<Image>` component fail ho jayega.
- Rewrites CORS issues solve karte hain bina backend change kiye.
- Path aliases imports clean rakhte hain.

3. 🎯 Practical Tasks (The Mission)

Task 1: Add an external image domain to `next.config.ts`
The Logic: Maan le tu `unsplash.com` ki images use karega. `next.config.ts` mein `images.remotePatterns` array mein ek object add karo with `protocol: 'https'` aur `hostname: 'images.unsplash.com'`. Config change karne ke baad server restart karna mat bhoolna.

Task 2: Create a rewrite rule to proxy an external API
The Logic: Tujhe ek API call karni hai `https://jsonplaceholder.typicode.com/posts` par lekin CORS error aata hai. `next.config.ts` mein `async rewrites()` function export kar. Ek rule banao: `source: '/api/posts'` ko `destination: 'https://jsonplaceholder.typicode.com/posts'` par map karo. Ab `/api/posts` fetch karega toh CORS nahi aayega.

Task 3: Verify path aliases are working
The Logic: Already `@/*` se `src/*` map hota hai. Tujhe ek naya alias add karna hai: `@components/*` ko `src/components/*` map karo. `tsconfig.json` mein `paths` ke andar `"@components/*": ["src/components/*"]` add kar. Phir kisi component mein `import Button from '@components/ui/Button'` use kar — kaam karna chahiye.

Task 4: Understand environment variables
The Logic: `.env.local` file bana aur usme `NEXT_PUBLIC_API_URL=http://localhost:3000/api` likh. `NEXT_PUBLIC_` prefix wali variables browser mein exposed hoti hain. Bina prefix wali sirf server side pe available hoti hain. Ek page mein `console.log(process.env.NEXT_PUBLIC_API_URL)` daal — terminal aur browser console dono mein check kar.

🔥 THE COMBO TASK:
Ek image component bana jo unsplash se random image dikhaye (use `https://images.unsplash.com/photo-...` koi bhi ID). `next.config.ts` mein domain allow karna mat bhoolna. Agar error aata hai "hostname not configured" toh tu jaanta hai kya karna hai. Phir ek rewrite rule bana jo `/api/hello` ko external API `https://api.github.com` pe map kare. Fetch `/api/hello` se data laake page mein dikha. Saath mein environment variable use kar API URL dynamic bana.

4. ✅ Definition of Done (Verification)
- Unsplash image render ho rahi hai without "Invalid src prop" error.
- `/api/posts` fetch karne par JSON data aata hai (browser console mein check kar).
- `@components/ui/Button` import kaam kar raha hai.
- `.env.local` variable browser console mein visible hai.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords:**
- **`remotePatterns`** : Security feature — sirf explicitly allowed domains se images load hoti hain. Internal — Next.js image optimization pipeline domain whitelist check karti hai. Miss kiya toh production mein images break ho jayengi.
- **Rewrites** : URL masking — browser ko lagta hai API same origin se aa rahi hai, par server proxy kar deta hai. Internal — `next.config.ts` rewrite rules HTTP middleware ki tarah kaam karte hain. Miss kiya toh CORS errors ya external API keys expose ho sakti hain.
- **Path aliases** : TypeScript compiler option. Internal — module resolution phase mein alias expand hote hain. Multiple aliases allowed — e.g., `@ui/*`, `@lib/*`. Miss kiya toh relative imports `../../../../` se bachna mushkil.
- **`NEXT_PUBLIC_` prefix** : Webpack define plugin inlines these variables at build time. Internal — `process.env.NEXT_PUBLIC_*` ko build time par actual value replace kar diya jata hai. Bina prefix wale sirf Node.js environment mein available hote hain. Miss kiya (prefix nahi lagaya client pe use karne ki koshish ki) toh value `undefined` aayegi.

**Hint snippet (sirf samajhne ke liye):**
```ts
// next.config.ts
const nextConfig = {
  images: { remotePatterns: [{ protocol: 'https', hostname: 'images.unsplash.com' }] },
  async rewrites() { return [{ source: '/api/posts', destination: 'https://jsonplaceholder.typicode.com/posts' }]; }
};
```
```json
// tsconfig.json paths addition
"paths": { "@/*": ["src/*"], "@components/*": ["src/components/*"] }
```
Server restart mandatory after config changes!

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🏁 MODULE 2 RECAP — Tera Status Report
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
**Siksha Summary:**
- ✅ `create-next-app` se professional boilerplate generate karna aa gaya.
- ✅ Production-grade folder structure (components/ui, features, lib, utils) clear hai.
- ✅ `next.config.ts` mein images, rewrites configure karna seekh liya.
- ✅ Path aliases aur environment variables ka concept pakda.

**Guru-ji's Warning:**
"Check kar le bhai! Level 2.3 mein rewrite rule banate time `source` aur `destination` ka format sahi tha? Agar external image domain add karna bhool gaya toh image nahi aayegi. Ek baar apna `next.config.ts` bina dekhe likh ke dikha. Phir aage badhte hain!"

---
--- ⏸️ OUTPUT LIMIT APPROACHING. Type 'CONTINUE' for Module 3 (Routing — 8 levels).
✅ Completed so far : Levels 1.1–1.4, 2.1–2.3 (Module 1 and 2 complete = 7 levels)
⏳ Remaining       : Module 3 (Levels 3.1 to 3.8) — Routing & Navigation
📊 Progress        : 7 Levels done / 15 Levels total | Module 2 of 3

**Type 'CONTINUE'** — main Module 3 ka pehla half (Levels 3.1 to 3.4) next response mein dunga.

Chal bhai, aagye hum Module 3 mein — Routing & Navigation. Ab tak tune project setup aur rendering concepts pakde hain. Ab Next.js ki jaan (App Router) ko practical tareeke se todte hain. Pehle 4 levels ek saath de raha hoon. Dhyan se kar, har level ke tasks terminal aur code editor mein execute kar.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 3: Routing & Navigation → Level 3.1: Basic Routes – page.tsx, layout.tsx, template.tsx [🟢 Beginner]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
`app/` folder ke andar jo folder hoga, wahi URL path banega. Har folder mein `page.tsx` = us route ka UI. `layout.tsx` = surrounding UI (navbar, footer) jo nested routes ke saath persist karta hai. `template.tsx` = layout jaisa but re-mount hota hai navigation par.

2. 💥 Why? (Production Impact)
- Bina routing library ke complex nested layouts bana sakte ho.
- Layouts state preserve karte hain (e.g., search input value page change hone par bhi rahega).
- Templates useful for enter/exit animations.

3. 🎯 Practical Tasks (The Mission)

Task 1: Create three routes: `/`, `/about`, `/contact`
The Logic: `app/page.tsx` pehle se hai. `app/about/page.tsx` bana aur `app/contact/page.tsx` bana. Har page mein alag heading daal. Server start kar aur browser mein teeno URLs visit kar.

Task 2: Create a root layout that wraps all pages with a navbar
The Logic: `app/layout.tsx` mein ek `<nav>` element add kar with links (use normal `<a>` tags abhi). Dekh ki navbar har page par dikhta hai. `children` prop ke aas-paas navbar rakh.

Task 3: Create a nested layout inside a route group (e.g., `/dashboard/settings` with sidebar)
The Logic: `app/dashboard/layout.tsx` bana jisme ek sidebar ho (`<aside>Dashboard Links</aside>`) aur `children`. Phir `app/dashboard/settings/page.tsx` bana. Jab `/dashboard/settings` pe jaoge, sidebar aur settings content dono dikhne chahiye, lekin root layout ka navbar bhi hona chahiye (nested layouts combine hote hain).

Task 4: Understand the difference between layout and template
The Logic: `app/template-example/layout.tsx` bana jisme `console.log('Layout render')`. `app/template-example/template.tsx` bana jisme `console.log('Template render')`. Phir `app/template-example/page.tsx` bana. Ab `/template-example` visit kar aur phir kisi doosre page (e.g., `/about`) jaakar wapas aao. Console mein dekho — layout sirf ek baar log hoga, template har baar log hoga (re-mount).

🔥 THE COMBO TASK:
Ek e-commerce layout bana. Root layout mein `<header>` with logo and cart icon. `app/products/layout.tsx` mein ek category sidebar (e.g., Electronics, Fashion). `app/products/page.tsx` mein all products list. `app/products/electronics/page.tsx` mein sirf electronics. Jab electronics page pe jaao, toh sidebar + products content dikhna chahiye, aur root layout ka header bhi. Verify ki sidebar state (jaise selected category highlight) page change hone par preserve hoti hai ya nahi.

4. ✅ Definition of Done (Verification)
- `/about`, `/contact` pages apna alag content dikhate hain.
- Navbar har page par dikhta hai.
- `/dashboard/settings` par sidebar + settings content dono dikhte hain.
- Template re-mount behaviour console logs se confirm.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords:**
- **`page.tsx`** : Special file — export default React component. Internal — Next.js router filesystem scanner is file ko route ka entry point maanta hai. Miss kiya toh folder URL route nahi banega, 404 aayega.
- **`layout.tsx`** : Shared UI wrapper. Internal — layout tree merge hota hai; child layout parent layout ke `children` slot mein render hota hai. State preserve hoti hai kyunki layout unmount nahi hota navigation par.
- **`template.tsx`** : Layout jaisa but har navigation par re-mount hota hai. Internal — React key change hota hai, isliye component re-instantiate hota hai. Use for animations, `useEffect` jo har visit pe run hona chahiye.
- **Nested layouts** : Multiple `layout.tsx` files at different folder levels. Internal — React component composition; root layout provides `<html>`, child layouts provide nested UI.

**Hint snippet (sirf samajhne ke liye):**
```tsx
// app/layout.tsx
export default function RootLayout({ children }) {
  return (<html><body><nav>Navbar</nav>{children}</body></html>);
}
// app/dashboard/layout.tsx
export default function DashboardLayout({ children }) {
  return (<div><aside>Sidebar</aside><main>{children}</main></div>);
}
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 3: Routing & Navigation → Level 3.2: Linking – `<Link>` Component & Prefetching Strategies [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
`<Link href="/path">` Next.js ka built-in component hai jo client-side navigation karta hai (page reload nahi hota). Prefetching — jab link viewport mein aata hai, Next.js background mein destination page ka code aur data download kar leta hai.

2. 💥 Why? (Production Impact)
- `<a>` tag se full page reload hota hai — slow, app feel khatam.
- Prefetching se click karne par page instantly load hota hai.
- Mobile users ke liye better UX.

3. 🎯 Practical Tasks (The Mission)

Task 1: Replace `<a>` tags with `<Link>` in navbar
The Logic: Pehle wale navbar mein `<a href="/about">` tha. Use `import Link from 'next/link'` karke `<Link href="/about">` se replace kar. Browser network tab mein click karne par dek — page reload nahi hoga, sirf fetch request hogi (prefetch already ho chuki hogi).

Task 2: Observe prefetching in action
The Logic: Network tab open kar (Preserve log enable kar). Page load karte hi dek — `/about` ki request background mein chali jayegi bina click kiye (kyunki link viewport mein hai). `next/link` default prefetch hota hai. Isse page click pe instant load hota hai.

Task 3: Disable prefetching for a specific link
The Logic: `<Link href="/heavy-page" prefetch={false}>` use kar. Page reload kar aur network tab mein dek — `/heavy-page` ki request background mein nahi aayegi. Click karne par tab load hogi.

Task 4: Use `replace` prop instead of `push`
The Logic: `<Link href="/login" replace>` — ye browser history mein current entry replace kar deta hai, nayi nahi push karta. Matlab user back button press karega toh login se pehle wale page pe nahi jayega (helpful after login). Implement karke back button behavior check kar.

🔥 THE COMBO TASK:
Ek product listing page bana jisme 20 products hain, har product ka `<Link href="/product/[id]">` hai. Network throttling (Slow 3G) enable kar browser dev tools mein. Page load kar aur scroll kar. Dekh ki prefetch kaise kaam kar raha hai — jo links viewport mein aa rahe hain, unki requests background mein ja rahi hain. Phir ek link click kar — page instantly load hona chahiye (ya thoda wait if prefetch complete nahi hua). Fir `prefetch={false}` add kar ek product mein aur compare kar.

4. ✅ Definition of Done (Verification)
- Navbar links click karne par page reload nahi hota (browser refresh icon nahi blink karta).
- Network tab mein page load ke time extra requests dikhti hain prefetch ke liye.
- `prefetch={false}` wale link ki request background mein nahi aati.
- `replace` wale link ke baad back button expected behaviour dikhata hai.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords:**
- **`next/link`** : React component jo internally `React.createElement('a')` generate karta hai aur click handler attach karta hai. Internal — client-side navigation via `pushState` history API. Miss kiya toh `<a>` use karega, full reload.
- **Prefetching** : Default behaviour (production mein). Internal — link viewport mein aate hi `requestIdleCallback` se destination page ke `page.js` chunk aur data (JSON) fetch hota hai. Miss kiya toh click par latency aayegi.
- **`prefetch={false}`** : Use for rarely visited links ya bandwidth-sensitive users. Miss kiya (disable nahi kiya heavy page pe) toh unnecessary bandwidth waste.
- **`replace` prop** : `router.replace` instead of `router.push`. Internal — history stack mein current entry overwrite hoti hai. Useful for login redirects, form submission ke baad back button avoid karne ke liye.

**Hint snippet (sirf samajhne ke liye):**
```tsx
import Link from 'next/link';
<Link href="/about" prefetch={false} replace>About</Link>
```
Tujhe navbar mein teeno links `Link` se replace karne hain aur prefetch behaviour network tab mein observe karna hai.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 3: Routing & Navigation → Level 3.3: Programmatic Navigation – useRouter, redirect, permanentRedirect [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Programmatic navigation = code se page change karna, user click ke bina. `useRouter` hook (client components), `redirect()` function (server components/server actions), `permanentRedirect()` for SEO (308 status).

2. 💥 Why? (Production Impact)
- Form submit hone ke baad user ko success page pe bhejna.
- Unauthorized user ko login page pe redirect karna.
- SEO-friendly permanent redirects (e.g., old product URL to new).

3. 🎯 Practical Tasks (The Mission)

Task 1: Use `useRouter` in a client component to navigate after button click
The Logic: Ek client component bana (`"use client"`) jisme ek button ho. onClick mein `router.push('/dashboard')` call kar. `import { useRouter } from 'next/navigation'` se. Jab button click karega, `/dashboard` pe chala jaana chahiye.

Task 2: Use `router.back()` to implement a "Go Back" button
The Logic: Ek page mein back button banao jo `router.back()` call kare. Browser history mein peeche wala page load hoga. `router.forward()` bhi hai but kam use hota hai.

Task 3: Use `redirect()` in a Server Component for auth check
The Logic: `app/dashboard/page.tsx` (server component) mein check karo — maan lo ek cookie `isLoggedIn` nahi hai. Agar nahi toh `redirect('/login')` call kar. `import { redirect } from 'next/navigation'`. Redirect ke baad ka code execute nahi hoga. Browser automatically login page pe chala jayega.

Task 4: Implement a permanent redirect for a deprecated route
The Logic: `app/old-products/page.tsx` banao. Usme `permanentRedirect('/products')` call kar. Jab user `/old-products` visit karega, permanent redirect (HTTP 308) hoga. Browser cache kar lega aur SEO search engines update kar denge. `permanentRedirect` import same jagah se.

🔥 THE COMBO TASK:
Ek login form bana (client component) jo email/password leta hai. Submit par API call kare (mock: agar email contains "user" toh success). Success par `router.push('/dashboard')`, failure par alert dikhaye. Phir dashboard page (server component) pe check kare ki login hua ya nahi (e.g., localStorage ya cookie check). Agar nahi hua toh `redirect('/login')`. Execute kar — flow test kar. Saath mein `/old-products` permanent redirect implement kar aur browser dev tools network tab mein 308 status code dekh.

4. ✅ Definition of Done (Verification)
- Button click karne par navigation hota hai without full reload.
- Back button navigation kaam karta hai.
- Bina login ke dashboard pe jaane ki koshish karne par redirect ho jata hai.
- `/old-products` visit karne par network tab mein status code 308 dikhta hai, aur URL `/products` pe change ho jata hai.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords:**
- **`useRouter`** : React hook for client-side navigation. Internal — context provider se router instance milta hai jo history API methods expose karta hai (`push`, `replace`, `back`, `forward`). Miss kiya toh `window.location` use karna padega jo full reload karega.
- **`redirect()`** : Server function jo `NEXT_REDIRECT` error throw karta hai. Internal — Next.js middleware catches this error and sends 307 response with Location header. Miss kiya (redirect nahi kiya) toh unauthorized user secure page dekh lega.
- **`permanentRedirect()`** : Same as redirect but 308 status. Internal — search engines index new URL and transfer SEO ranking. Miss kiya toh temporary redirect (307) use hoga, SEO juice transfer nahi hoga.
- **Client vs Server navigation** : Client (`useRouter`) — fast, no network round trip for HTML. Server (`redirect`) — full round trip, but can be used in server components and server actions.

**Hint snippet (sirf samajhne ke liye):**
```tsx
// Client component
"use client";
import { useRouter } from 'next/navigation';
const router = useRouter();
router.push('/dashboard');

// Server component
import { redirect } from 'next/navigation';
if (!loggedIn) redirect('/login');
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 3: Routing & Navigation → Level 3.4: Dynamic Routes – `[productId]` (Next.js 15 async params) [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Folder naam square brackets `[param]` mein wrap karne se dynamic segment ban jaata hai. URL mein jo bhi aayega, wo param variable mein page component ko milega. **Next.js 15 mein params Promise hai** — `await params` karna padega.

2. 💥 Why? (Production Impact)
- Thousands of products ke liye alag page nahi bana sakte — dynamic route ek hi page hai jo saare products handle karta hai.
- SEO friendly — `/product/iphone-15` search engines ko specific page lagta hai.

3. 🎯 Practical Tasks (The Mission)

Task 1: Create a dynamic route folder `app/products/[productId]/`
The Logic: `mkdir -p app/products/[productId]` (ya manually folder bana). Usme `page.tsx` bana. Export default async function component jo `params` prop receive kare. Type `{ params: Promise<{ productId: string }> }`. Await karke `productId` nikaal aur display kare `<h1>Product: {productId}</h1>`.

Task 2: Test the dynamic route with different URLs
The Logic: Server start kar. Browser mein `/products/abc`, `/products/123`, `/products/macbook` visit kar. Har baar same page render hoga, lekin text change hoga.

Task 3: Fetch product data based on dynamic param
The Logic: Ek mock products object bana (e.g., `{ 'abc': { name: 'Product A' }, '123': { name: 'Product B' } }`). Page mein param ke hisaab se data fetch kar (direct object lookup). Agar product exist nahi karta toh "Not Found" dikha.

Task 4: Generate static params using `generateStaticParams`
The Logic: Dynamic route page mein `export async function generateStaticParams()` bana. Ye function array return kare `[{ productId: 'abc' }, { productId: '123' }]`. Build command (`npm run build`) chala. Build output mein dek — `/products/abc` aur `/products/123` static pages generate ho gaye. `/products/xyz` dynamic remain karega (fallback).

🔥 THE COMBO TASK:
Ek e-commerce product detail page bana. Product data API se fetch karo (mock: `fetch('https://fakestoreapi.com/products/' + productId)`). Next.js 15 mein async params ka use karte hue productId await karo. Loading state handle kar (optional — `loading.tsx` bana). Error handling bhi kar (try-catch ya `error.tsx`). Phir `generateStaticParams` implement kar — pehle 10 products ke IDs fetch karo (API call) aur unke liye static pages generate karo. Build karo aur verify ki static pages ban gaye.

4. ✅ Definition of Done (Verification)
- `/products/any-string` page render hota hai aur URL ka last part screen par dikhta hai.
- Product exist karta hai toh details dikhti hai, nahi toh "Not Found" message.
- Build output mein static pages (`○`) dikhte hain for provided IDs.
- Dynamic route bina param ke 404 deta hai ( `/products` alone should 404 unless you have separate page).

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords:**
- **`[param]` folder** : Dynamic segment syntax. Internal — router matches any segment except those starting with `_` or `.`. Matched value is captured and passed as param.
- **`params` Promise (Next.js 15)** : Breaking change from Next.js 13/14. Internal — async params allow for incremental adoption of new caching and rendering patterns. Miss kiya `await` toh value Promise object hi rahega, string nahi.
- **`generateStaticParams`** : For static generation with dynamic routes. Internal — function runs at build time, params array determines which pages are pre-rendered as static HTML. Others are generated on-demand (SSR or fallback). Miss kiya toh sab requests dynamic generate honge (slower, no static optimization).
- **`notFound()` function** : Call `notFound()` from `next/navigation` in server component to show 404 page. Internal — throws `NEXT_NOT_FOUND` error, caught by error boundary.

**Hint snippet (sirf samajhne ke liye):**
```tsx
// app/products/[productId]/page.tsx
export default async function ProductPage({ params }: { params: Promise<{ productId: string }> }) {
  const { productId } = await params;
  const res = await fetch(`https://fakestoreapi.com/products/${productId}`);
  const product = await res.json();
  return <div>{product.title}</div>;
}
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🏁 MODULE 3 RECAP (Half) — Tera Status Report
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
**Siksha Summary (Levels 3.1–3.4):**
- ✅ Basic routing: `page.tsx`, `layout.tsx`, `template.tsx` — nested layouts clear hai.
- ✅ `<Link>` component aur prefetching — network tab mein dekh liya hoga.
- ✅ Programmatic navigation — `useRouter` (client) aur `redirect` (server) dono use kar liye.
- ✅ Dynamic routes with Next.js 15 async params — product page bana liya.

**Guru-ji's Warning:**
"Level 3.4 mein `generateStaticParams` implement kiya tha? Agar nahi kiya toh wapas jaake kar. Static generation hi Next.js ki asli power hai. Aadhe module mein hi itna seekh liya — baaki 4 levels aur bhi advanced hain (Catch-all, Route Groups, Parallel, Intercepting). Type 'CONTINUE' to conquer the rest of Module 3!"

---
--- ⏸️ OUTPUT LIMIT APPROACHING. Type 'CONTINUE' to get the remaining Module 3 levels (3.5 to 3.8).
✅ Completed so far : Levels 1.1–1.4, 2.1–2.3, 3.1–3.4 (11 levels done)
⏳ Remaining       : Module 3 Levels 3.5 (Catch-all), 3.6 (Route Groups), 3.7 (Parallel Routes), 3.8 (Intercepting Routes)
📊 Progress        : 11 Levels done / 15 Levels total | Module 3 of 3 (half done)

Chal bhai, aakhiri sprint hai! Module 3 ke baaki 4 levels — ye hain asli advanced routing ke gems. Catch-all se leke Intercepting routes tak, sab kuch ek saath. Dhyan se padh, terminal khol ke rakh. Copy-paste nahi, khud type karna. Let's go!

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 3: Routing & Navigation → Level 3.5: Catch-all Segments – `[...slug]` & Optional Catch-all [🔴 Advanced]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
`[...slug]` ek catch-all dynamic route hai jo URL ke ek se zyada segments capture karta hai aur unhe array mein deta hai. `[[...slug]]` optional catch-all hai jo root route (`/shop`) ko bhi match karta hai.

2. 💥 Why? (Production Impact)
- E-commerce category filters: `/shop/men/shoes/nike` — number of segments variable.
- Documentation: `/docs/getting-started/installation` — kitne bhi levels ho sakte hain.
- Optional catch-all: same page root aur deep paths dono handle kare.

3. 🎯 Practical Tasks (The Mission)

Task 1: Create a catch-all route `app/shop/[...slug]/page.tsx`
The Logic: Folder name `[...slug]` banana hai (three dots + brackets). Page component mein `params` ko await karo. `slug` ek array hoga (e.g., `['men', 'shoes', 'nike']`). Array ko render karo as list ya breadcrumb.

Task 2: Test with different URL depths
The Logic: Browser mein `/shop/men`, `/shop/men/shoes`, `/shop/men/shoes/nike` visit kar. Har baar same page render hoga, par array length alag hogi. Console mein `params.slug` print karo.

Task 3: Implement breadcrumb navigation from slug array
The Logic: Slug array se dynamic breadcrumb banao. Example: `['men', 'shoes']` → `Home / Men / Shoes`. Har breadcrumb link should point to appropriate category level. `map` function use karo.

Task 4: Create optional catch-all `app/docs/[[...slug]]/page.tsx`
The Logic: Double brackets `[[...slug]]` folder banao. Is page mein check karo: agar `slug` undefined hai toh root docs page dikhao, agar array hai toh nested content dikhao. `/docs` aur `/docs/getting-started` dono same page handle karega.

🔥 THE COMBO TASK:
Ek complete category filter page banao. URL `/category/electronics/phones/samsung` catch-all se array milega `['electronics','phones','samsung']`. Tujhe ek mock product database banana hai (JS object with nested categories). Array ke hisaab se products filter karke dikhane hain. Agar last segment (e.g., 'samsung') se match karta hai toh sirf woh brand ke phones dikhao. Breadcrumb banao jisme har level clickable ho. Agar koi category empty ho toh "No products" message dikhao. Saath mein optional catch-all banao `/category` (bina kuch segment) pe all categories show karo.

4. ✅ Definition of Done (Verification)
- `/shop/men/shoes` par array `['men','shoes']` render hota hai.
- Breadcrumb links click karne par correct URL navigate hota hai.
- `/docs` (optional catch-all) pe content dikhta hai, `/docs/guide/setup` pe bhi dikhta hai.
- Category filter page array ke hisaab sahi products dikhata hai.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords:**
- **`[...slug]`** : Catch-all segment. Internal — router matches one or more segments, groups them as array. Miss kiya (single bracket use kiya) toh sirf ek segment milega, extra segments 404 denge.
- **`[[...slug]]`** : Optional catch-all. Internal — matches zero or more segments. Undefined case handle karna padega. Useful for root + nested same component.
- **Array to path conversion** : `slug.join('/')` se original path milega, `slug.slice(0, -1)` se parent path milega. Internal — no special API, manual array manipulation.
- **Breadcrumb from slug** : `slug.map((segment, idx) => ({ name: segment, path: '/' + slug.slice(0, idx+1).join('/') }))`. Yeh pattern production mein use hota hai.

**Hint snippet (sirf samajhne ke liye):**
```tsx
// app/shop/[...slug]/page.tsx
export default async function CategoryPage({ params }: { params: Promise<{ slug: string[] }> }) {
  const { slug } = await params;
  const breadcrumbs = slug.map((s, i) => ({ name: s, path: '/' + slug.slice(0, i+1).join('/') }));
  return <div>{/* render breadcrumbs and products */}</div>;
}
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 3: Routing & Navigation → Level 3.6: Route Groups – `(auth)` for Invisible Organization [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Parentheses `(folderName)` se folder URL path mein include nahi hota. Sirf code organization aur layout grouping ke liye.

2. 💥 Why? (Production Impact)
- Different layouts for different sections: public pages (navbar+footer), auth pages (plain), dashboard (sidebar).
- URL clean rakhte hue code modular rakho.
- Multiple root layouts possible (chahe different `<html>` structures ho).

3. 🎯 Practical Tasks (The Mission)

Task 1: Create a route group `(auth)` with login and register pages
The Logic: `app/(auth)/login/page.tsx` aur `app/(auth)/register/page.tsx` banao. URLs `/login` aur `/register` hone chahiye, NOT `/auth/login`. Verify by visiting.

Task 2: Add a separate layout for the `(auth)` group
The Logic: `app/(auth)/layout.tsx` banao. Is layout mein koi navbar nahi, sirf centered card. Root `app/layout.tsx` ka navbar `(auth)` pages pe nahi aana chahiye — kyunki route group ka layout root layout ko replace nahi karta, actually nested hota hai. Dhyan: Next.js mein route group layout root layout ke `children` mein aata hai. Agar nahi chahte navbar, toh root layout mein conditional logic lagana padega ya separate root layout bana (advanced). Is level ke liye bas confirm kar ki `(auth)/layout.tsx` apna extra wrapper add kar raha hai.

Task 3: Create another group `(marketing)` for landing pages
The Logic: `app/(marketing)/about/page.tsx` aur `app/(marketing)/pricing/page.tsx`. Inka URL `/about` aur `/pricing` hona chahiye. Marketing group ka alag layout bana jisme fancy hero section ho.

Task 4: Understand that route groups don't affect URL but affect layout nesting
The Logic: Root layout mein `<h1>Main Site</h1>` daalo. `(marketing)/layout.tsx` mein `<h2>Marketing Section</h2>` daalo. `/about` visit karne par dono dikhenge (nested). `(auth)/layout.tsx` mein `<h2>Auth Section</h2>` daalo. `/login` pe dono dikhenge? Root layout ka navbar dikhega? Socho. Next.js mein multiple root layouts kaise banaye? (Hint: Root layout ko delete karke har group apna layout bana sakta hai but that's advanced.)

🔥 THE COMBO TASK:
E-commerce site banao jisme teen sections ho:
1. `(public)` — home, about, contact — navbar+footer layout.
2. `(auth)` — login, register — simple centered card layout (no navbar).
3. `(dashboard)` — profile, orders — sidebar layout.
Har section ka alag layout banao. URLs clean rakhni hai: `/`, `/about`, `/login`, `/register`, `/dashboard/profile`. `(dashboard)/layout.tsx` mein sidebar aur `children`. Is project ko implement karo. Ek chunauti: Root layout mein navbar kaise hatoge auth pages se? Tujhe root layout se navbar hata kar har group ke layout mein navbar dalna padega, ya conditional logic use karni padegi (`pathname` check). Try both approaches.

4. ✅ Definition of Done (Verification)
- `/login` aur `/register` URLs work, no `/auth` in URL.
- `/about` aur `/pricing` URLs work.
- Auth pages ka layout navbar nahi dikhata (if you removed from root).
- Dashboard pages sidebar dikhati hai.
- Folder structure clean hai groups mein.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords:**
- **`(folder)`** : Route group. Internal — during routing, parenthesized segments are ignored for URL matching but retained for layout hierarchy. Miss kiya toh URL mein folder name aayega.
- **Layout group isolation** : Different groups can have different layouts. Internal — layout tree merges based on actual URL path, not group names. Groups only affect which layout files are considered.
- **Multiple root layouts** : By removing `app/layout.tsx` and putting layouts inside groups, you can have completely different `<html>` structures. Internal — Next.js treats first layout it finds as root. Rare but powerful.
- **Shared layouts across groups** : Agar do groups same layout chahte ho, toh layout ko ek common folder mein rakh kar import kar sakte ho.

**Hint snippet (sirf samajhne ke liye):**
```tsx
// app/(auth)/layout.tsx
export default function AuthLayout({ children }) {
  return <div className="auth-container">{children}</div>;
}
// app/(marketing)/layout.tsx
export default function MarketingLayout({ children }) {
  return <><HeroSection />{children}</>;
}
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 3: Routing & Navigation → Level 3.7: Parallel Routes – `@modal` for Independent Slots [🔴 Advanced]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Parallel routes = ek hi layout mein multiple pages ek saath (parallel). `@folder` syntax se named slots banate hain, jo layout ko props ke roop mein milte hain.

2. 💥 Why? (Production Impact)
- Dashboard: `@analytics`, `@users`, `@sales` — independent loading, error states.
- Modals: feed ke upar modal dikhana, peeche feed active rakhna.
- Conditional rendering based on URL or user role.

3. 🎯 Practical Tasks (The Mission)

Task 1: Create a layout with two parallel slots `@feed` and `@trending`
The Logic: `app/@feed/page.tsx` aur `app/@trending/page.tsx` banao. `app/layout.tsx` mein props mein `feed` aur `trending` add karo. Unhe side-by-side render karo. URL kya hoga? Parallel routes URL mein appear nahi hote directly, lekin unke andar ke nested routes ho sakte hain. Basic case: sirf default page render hoga.

Task 2: Add default.tsx to each slot to handle hard reloads
The Logic: `app/@feed/default.tsx` aur `app/@trending/default.tsx` banao. Ye files tab render hoti hain jab slot ke liye koi specific page match nahi hota (e.g., user directly `/` visit kare). `default.tsx` mein fallback UI dalo (e.g., "No feed available").

Task 3: Make one slot conditionally render based on URL using route groups
The Logic: Parallel routes often combine with route groups. Example: `app/(dashboard)/@analytics/page.tsx` and `app/(dashboard)/@analytics/sales/page.tsx`. Jab user `/dashboard` pe ho, analytics slot show karega overview. Jab `/dashboard/sales` pe ho, wohi slot sales data dikhayega. Implement karo: `app/(dashboard)/layout.tsx` jisme `@analytics` slot ho.

Task 4: Understand slot navigation: how to change slot content without changing main page
The Logic: Parallel route ka page change karne ke liye, tumhe URL navigate karna hoga jo us slot ke path ko represent kare. Example: `/dashboard` shows default. `/dashboard/analytics/sales` se `@analytics` slot sales page dikhayega, main page (children) same rahega. Try karo: ek link banao jo sirf slot update kare.

🔥 THE COMBO TASK:
Ek admin dashboard banao jisme do parallel slots: `@recentOrders` aur `@statistics`. Main area (`children`) mein welcome message ho. Jab user `/dashboard` pe ho, dono slots default data dikhayein. Jab user `/dashboard/orders` pe navigate kare, `@recentOrders` slot updated orders list dikhaye, statistics slot same rahe. Jab `/dashboard/stats` pe jaye, statistics slot update ho. Iske liye nested routes banane padenge: `app/dashboard/@recentOrders/orders/page.tsx` etc. Implement karo. Hard refresh (F5) pe `default.tsx` ensure karo ki 404 na aaye. Is exercise mein parallel routes ki real power samajh aayegi.

4. ✅ Definition of Done (Verification)
- Layout mein `feed` aur `trending` props side-by-side render ho rahe hain.
- Hard refresh karne par `default.tsx` render hota hai (404 nahi aata).
- Dashboard mein `/dashboard` aur `/dashboard/orders` alag slot content dikhata hai.
- Parallel routes ke andar loading states add karne ke liye `loading.tsx` bana sakte ho.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords:**
- **`@slot`** : Named parallel route. Internal — layout receives these as props. Each slot has its own routing tree independent of `children`. Miss kiya toh slot ignored, no error.
- **`default.tsx`** : Fallback for slot when no matching route. Internal — Next.js renders default when current URL doesn't match any page inside slot. Miss kiya aur user hard refresh kare toh 404.
- **Slot navigation** : URL changes can affect multiple slots simultaneously. Internal — each slot matches its own segment from URL. Complex but powerful for dashboards.
- **Parallel + Intercepting** : Ye dono milke modal pattern banate hain (next level).

**Hint snippet (sirf samajhne ke liye):**
```tsx
// app/layout.tsx
export default function Layout({ children, feed, trending }) {
  return (<div><main>{children}</main><aside>{feed}</aside><aside>{trending}</aside></div>);
}
// app/@feed/default.tsx
export default function Default() { return <div>Default Feed</div>; }
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 3: Routing & Navigation → Level 3.8: Intercepting Routes – `(.)product` (Instagram-style Modals) [🔴 Advanced]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Intercepting routes allow you to load a route from another part of your app within the current layout (as modal), but when accessed directly (or shared URL), it shows the full page. Syntax: `(.)` for same level, `(..)` for one level up, `(..)(..)` for two levels, `(...)` for root.

2. 💥 Why? (Production Impact)
- Instagram, Pinterest, Reddit style: feed pe click → modal, direct link → full page.
- Preserve scroll position and context.
- Shareable URLs that work both ways.

3. 🎯 Practical Tasks (The Mission)

Task 1: Setup basic feed and product page
The Logic: `app/feed/page.tsx` (product listing) aur `app/product/[id]/page.tsx` (full page) banao. Feed mein `Link` components use karo.

Task 2: Create a parallel route slot for modal `@modal`
The Logic: `app/feed/@modal/default.tsx` banao (return null). `app/feed/layout.tsx` mein `modal` prop accept karo aur render karo.

Task 3: Create the intercepting route `app/feed/@modal/(.)product/[id]/page.tsx`
The Logic: Parentheses dot `(.)` means intercept routes at same level. Folder name `(.)product` banao, phir `[id]/page.tsx`. Is page mein modal-style UI banao (absolute positioning, background blur, close button). Ensure URL becomes `/product/[id]` when modal opens.

Task 4: Implement close functionality
The Logic: Modal mein close button ya backdrop click par `router.back()` use karo. `'use client'` directive lagana padega.

🔥 THE COMBO TASK:
Instagram clone jaisa feature banao. Feed page mein product cards ki grid ho. Har card click karne par modal khule (URL `/product/123`). Modal mein product details, close button. Background feed blur ho. Agar user direct URL `/product/123` type kare ya refresh kare, toh full product page dikhe (bina modal, bina feed). Iske liye: 
- `app/feed/page.tsx` — grid of links.
- `app/feed/layout.tsx` — children + modal slot.
- `app/feed/@modal/(.)product/[id]/page.tsx` — modal UI.
- `app/product/[id]/page.tsx` — full page UI.
- Modal close: `router.back()` se feed pe wapas.
- Hard refresh on modal URL should show full product page (check that `@modal` slot's default.tsx returns null, and main `product/[id]/page.tsx` renders).

Is combo task mein intercepting routes + parallel routes dono use honge. Implement karo aur test karo. Bahut maza aayega.

4. ✅ Definition of Done (Verification)
- Feed pe click karne par modal khulta hai, URL `/product/id` ho jata hai.
- Modal close karne par URL wapas `/feed` ho jata hai, feed scroll position wahi rahta hai.
- Direct URL `/product/id` browser mein type karne par full page khulta hai (modal nahi).
- Refresh on modal URL ke baad full page dikhta hai.
- Build successful (no duplicate route warnings).

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
**Core keywords:**
- **`(.)` intercept** : Same level interception. Internal — router compares current URL with intercepted route pattern during client navigation. If match and parallel slot exists, renders slot content instead of full page.
- **`(..)` intercept** : One level up. Internal — `../` directory traversal syntax. Use when modal route is one segment above current.
- **`(...)` intercept** : Root level. Internal — absolute path from app root. Useful for intercepting routes from anywhere.
- **Modal pattern** : Parallel slot (`@modal`) + intercepting route (`(.)product`) + `default.tsx` fallback. Internal — client navigation triggers intercept, server navigation (direct/hard reload) bypasses.

**Hint snippet (sirf samajhne ke liye):**
```tsx
// app/feed/layout.tsx
export default function FeedLayout({ children, modal }) {
  return (<>{children}{modal}</>);
}
// app/feed/@modal/(.)product/[id]/page.tsx
'use client';
import { useRouter } from 'next/navigation';
export default function ModalProduct({ params }) {
  const router = useRouter();
  return (<div className="modal"><button onClick={() => router.back()}>Close</button>Product {params.id}</div>);
}
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🏁 MODULE 3 RECAP (Complete) — Tera Final Status Report
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
**Siksha Summary (Levels 3.5–3.8):**
- ✅ Catch-all routes `[...slug]` aur optional catch-all — category filters aur docs ke liye ready.
- ✅ Route groups `(auth)` — URL clean rakhna aur layouts isolate karna aa gaya.
- ✅ Parallel routes `@slot` — dashboard mein independent sections banane ka gyan ho gaya.
- ✅ Intercepting routes `(.)` — Instagram jaisa modal pattern master kar liya.

**Guru-ji's Final Warning:**
"Bhai, 15 levels complete! Tune Next.js 15/16 ke core concepts, production-grade setup, aur advanced routing (parallel + intercepting) sab practical kar liya. Ab bina dekhe ek naya project bana — jisme route groups, dynamic routes, catch-all, parallel slots, aur intercepting modal ho. Agar woh bina error ke ban gaya, toh tu ab senior engineer level pe hai. Agar koi level skip kiya hai, toh wapas jaake kar. Ye shortcut nahi, mastery chahiye!"

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎉 ALL 15 LEVELS COMPLETED! 🎉
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

**Total Progress:** 15/15 Levels | 3/3 Modules | ~12 hours of hardcore CTF

**What's Next, Shishya?**
- Type `REVIEW` — main teri sabse common mistakes bataunga.
- Type `QUIZ` — 5 questions dunga test karne ke liye (bina notes ke answer kar).
- Type `CAPSTONE` — ek real-world project (e-commerce dashboard with modal product view) dunga jo saare concepts mix karega.

Bata, aage kya karna hai?

========================================================================================

