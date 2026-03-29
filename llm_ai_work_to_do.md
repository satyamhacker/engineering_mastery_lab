━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 1: LLM Evaluation Fundamentals → Level 1.1: Traditional Metrics (Exact Match, F1, BLEU/ROUGE) [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Exact Match = 100% string equality check. F1/BLEU/ROUGE = partial overlap metrics. Use Exact Match for strict rules (IDs, commands), F1/BLEU for soft matching (summaries, translations).

2. 💥 Why? (Production Impact)
- 🚨 Agar Exact Match galat jagah use kiya (creative answers pe), toh sahi responses bhi "fail" mark honge — false positives, alert fatigue.
- 💸 Agar F1/BLEU ko strict validation mein use kiya, toh dangerous outputs (jaise "share your OTP") pass ho sakte hain — security breach, financial loss.
- 📉 CI/CD pipeline mein wrong metric = har deploy pe false failures, team ka time waste, velocity down.

3. 🎯 Practical Tasks (The Mission)

🚨 **MISSION BRIEFING: FinTech Security Alert!**
> Ek banking chatbot "Fund Transfer" feature pe kaam kar raha hai. QA team ne notice kiya: jab user poochta hai "How to transfer money?", kabhi-kabhi bot bol deta hai "Just share your OTP, we'll do it for you!" 😱
> 
> **Tera Mission:** Ek lightweight validation layer bana jo aise dangerous responses ko turant pakde aur block kare — bina LLM ko retrain kiye, bina cloud dependency ke.
> 
> **Stakes:** Agar yeh bug production mein gaya, toh phishing attacks se ₹2.5 Cr+ ka loss + RBI penalty + brand reputation damage.
> 
> **Time Limit:** 15 minutes (simulated production hotfix).

---

**Task [1]: Dangerous Pattern Identification**
Kya karna hai: Ek chhoti list bana un keywords/phrases ki jo banking context mein NEVER allow hone chahiye (jaise "OTP", "password", "share your credentials").
The Logic: Exact Match ya substring check in patterns pe lagana fastest way hai critical security violations ko real-time mein pakadne ka — LLM call se pehle hi block.

**Task [2]: Exact Match Function Logic Design**
Kya karna hai: Ek function ka internal logic soch jo input response ko normalize kare (lowercase, strip spaces, remove punctuation) phir dangerous patterns se compare kare.
The Logic: Normalization zaroori hai kyunki user ya LLM "OTP", "otp", " O T P " — sab likh sakta hai. Agar normalize nahi kiya, toh attacker easily bypass kar lega.

**Task [3]: F1 Score for Partial Danger Detection**
Kya karna hai: Soch ki agar dangerous phrase poora nahi, par 60% match karta hai (jaise "share your o..p..") — toh F1-style token overlap kaise use karega threshold ke saath?
The Logic: Exact Match too strict for obfuscated attacks. F1 logic se hum partial matches ko bhi pakad sakte hain — jaise "otp" ke tokens ka overlap check karke alert trigger karna.

**Task [4]: CI/CD Pipeline Integration Point**
Kya karna hai: Identify kar ki yeh validation function kahan lagega — LLM response ke baad, user ko dikhane se pehle? Ya prompt injection detection ke saath?
The Logic: Security check hamesha "last mile" pe hona chahiye — response generate hone ke baad, par user tak pahunchne se pehle. Isse defense-in-depth banta hai.

🔥 **THE COMBO TASK (Final Boss):**
Sab tasks ko integrate kar: Ek pseudo-validation pipeline design kar jisme (1) dangerous patterns list, (2) normalized Exact Match check, (3) F1-based partial match fallback, aur (4) CI/CD hook point — sab ek saath kaam kare. Soch ki agar koi check fail ho, toh system kya kare? (Block? Log? Alert? Fallback response?)

4. ✅ Definition of Done (Verification — "Kaise pata chalega success hua?")
- [ ] Dangerous patterns list mein kam se kam 5 banking-specific risky phrases hain (OTP, PIN, password, credentials, bank details).
- [ ] Normalization logic cover karta hai: lowercase, strip, punctuation removal — taaki "O-T-P" bhi pakda jaye.
- [ ] F1-style partial match ka threshold clearly define hai (e.g., "agar 3/5 tokens match, toh alert").
- [ ] Pipeline diagram mein clear hai: User Query → LLM → Validation Layer → [PASS: show / FAIL: block+log].
- [ ] Combo Task: Ek sample dangerous response ("Please share your OTP for verification") ke liye, tera design usse pakad kar block karega — yeh manually trace karke dikhana.

⚠️ Notes mein exact verification output mention nahi tha — apne execution ka result dekh ke judge karo.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
- **Exact Match Function**: Internally kya karta hai? → Strings ko canonical form mein convert karta hai (lower+strip), phir `==` check. Miss kiya toh? → Case variations bypass kar jayenge.
- **F1 Score Logic**: Precision = kitne generated tokens dangerous hain? Recall = kitne dangerous tokens pakde gaye? Harmonic mean balance karta hai. Miss kiya toh? → Ya toh bahut false alarms, ya dangerous cheezein miss.
- **Normalization Steps**: Lowercase (case-insensitive), strip (whitespace bypass rokna), punctuation removal ("o-t-p" → "otp"). Miss kiya toh? → Attacker easily evade kar lega.
- **Threshold Tuning**: Exact Match = 100% strict. F1 partial = configurable threshold (e.g., 0.6). Miss kiya toh? → Ya system too noisy, ya too lenient.
- **CI/CD Hook Point**: Validation hamesha post-LLM, pre-user. Miss kiya toh? → Dangerous response user tak pahunch jayega.

💡 Hint Snippet (sirf samajhne ke liye — khud type karna):
```
# Normalization ka idea: 
def normalize(text): return text.lower().strip().replace("-", "").replace(" ", "")
# Exact Match check: 
if normalize(response) in dangerous_patterns: block()
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🏁 MODULE 1 RECAP — Tera Status Report
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Siksha Summary:
- Exact Match = strict equality for critical rules (security, IDs, commands).
- F1/BLEU = soft matching for semantic/partial overlap use cases.
- Normalization = bypass prevention ka secret weapon.
- Validation layer hamesha "last mile" pe lagana — defense-in-depth.

Guru-ji's Warning:
"Check kar le bhai! Kya tujhe yeh sab bina cheat sheet ke karna aa gaya hai? Agar inme se ek bhi cheez mein doubt hai ya confuse hai, toh chup chaap peeche ja aur wapas execute kar. Aage badhne ka koi fayda nahi agar basics hile hue hain!"

⚡ GURUDAKSHINA (The Checkpoint):
"Sare Levels clear hue? Screenshots taiyar rakh! Agar sab properly done hai toh type 'CONTINUE' for the next Level: 1.2 — Semantic Evaluation (Embeddings & Cosine Similarity) jahan hum e-commerce search ko fix karenge!"

--- ⏸️ OUTPUT LIMIT APPROACHING. Type 'CONTINUE' to get the next part.
✅ Completed so far : Level 1.1 fully done
⏳ Remaining       : Levels 1.2, 1.3, 1.4 + Module 2 & 3
📊 Progress        : 1 Levels done / 12 Levels total | Module 1 of 3

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 1: LLM Evaluation Fundamentals → Level 1.2: Semantic Evaluation (Embeddings & Cosine Similarity) [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Text ko vectors (numbers) mein convert kar. Cosine Similarity se unke beech ka "angle" napo. Words alag ho sakte hain, par meaning same ho toh score high aayega.

2. 💥 Why? (Production Impact)
- 🛒 **E-commerce Loss:** User ne search kiya "comfortable running shoes", system ne dikhaye "formal leather shoes" kyunki keyword match tha par meaning nahi. Sales gaye zero.
- 🔍 **RAG Failure:** User ne poocha "How to reset password?", DB se mila "How to change email". Words match huye, intent nahi. User frustrated chala gaya.
- 📉 **Search Relevance:** Agar sirf keyword match pe depend kiya, toh synonyms ("car" vs "automobile") kabhi nahi milenge.

3. 🎯 Practical Tasks (The Mission)

🚨 **MISSION BRIEFING: E-Commerce Search Disaster!**
> Ek fashion startup ka search bar toot chuka hai. Customer "winter jacket" dhoond raha hai, par site "summer t-shirt" dikha rahi hai kyunki dono mein "clothing" keyword common tha.
> 
> **Tera Mission:** Keyword matching ko hata kar Semantic Search (Embeddings) lagana hai jo "meaning" samjhe.
> 
> **Stakes:** Agar search fix nahi hua, toh next quarter mein 40% revenue drop hoga. Competitor jeet jayega.
> 
> **Time Limit:** 30 minutes (Hotfix before sale season).

---

**Task [1]: Vectorization Logic Setup**
Kya karna hai: Ek pre-trained model (jaise SentenceTransformer) choose kar jo text ko fixed-length vector (e.g., 384 dimensions) mein badal de.
The Logic: Text directly compare nahi ho sakta. Usse mathematical space mein le jaana padega. "Dog" aur "Puppy" ke vectors paas honge, "Car" ka door hoga.

**Task [2]: Cosine Similarity Calculation**
Kya karna hai: Do vectors ke beech ka cosine angle calculate karne ka logic laga (0 se 1 ke beech score).
The Logic: Euclidean distance length pe depend karta hai (lamba paragraph vs chhota query). Cosine sirf direction (meaning) dekhta hai. Isliye RAG/Search mein Cosine hi king hai.

**Task [3]: Threshold Tuning for Relevance**
Kya karna hai: Ek cutoff score decide kar (e.g., 0.75). Agar similarity < 0.75 hai, toh result mat dikhao.
The Logic: Har thoda sa match bhi dikhane se user confuse hota hai. Threshold se sirf high-confidence results hi filter honge.

**Task [4]: False Positive Test Case**
Kya karna hai: Ek aisa test case bana jahan words match karein par meaning alag ho (e.g., "Apple fruit" vs "Apple stock"). Check kar ki tera embedding model isse alag kar paata hai ya nahi.
The Logic: Contextual embeddings ko polysemy (ek word, multiple meanings) samajhna chahiye. Agar nahi samjha, toh model upgrade kar.

🔥 **THE COMBO TASK (Final Boss):**
Ek end-to-end search flow design kar: User Query → Embedding Model → Vector DB Search (Cosine) → Threshold Filter → Top 3 Results. Ek specific test case le: Query = "affordable laptop", DB Item 1 = "cheap notebook" (High Score), DB Item 2 = "expensive desktop" (Low Score). Prove kar ki tera system Item 1 ko upar layega.

4. ✅ Definition of Done (Verification — "Kaise pata chalega success hua?")
- [ ] Vector dimension clearly define hai (e.g., 384 or 768).
- [ ] Cosine Similarity score range 0.0 se 1.0 ke beech hai.
- [ ] Threshold value justify ki gayi hai (kyun 0.7 aur 0.9 nahi?).
- [ ] Test case mein "Synonyms" (Laptop/Notebook) ka score high hai.
- [ ] Test case mein "Antonyms/Unrelated" (Laptop/Desktop) ka score low hai.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
- **SentenceTransformer:** Text ko context-aware vectors mein badalta hai. "Bank of river" vs "Bank of money" ke vectors alag honge. Miss kiya toh? → Generic embeddings context miss kar denge.
- **Cosine Similarity:** Dot product divided by magnitude. Sirf direction matter karta hai. Miss kiya toh? → Lamba text chhote text se kabhi match nahi hoga (magnitude issue).
- **Thresholding:** Precision vs Recall ka trade-off. High threshold = kam results par sahi. Low threshold = zyada results par kuch bekaar. Miss kiya toh? → Search results spammy honge.
- **Vector Dimension:** Zyada dimensions = zyada accuracy par slow search. Kam dimensions = fast par kam accurate. Miss kiya toh? → Latency badh jayegi.

💡 Hint Snippet (sirf samajhne ke liye — khud type karna):
```
# Cosine ka logic: 
score = dot_product(vec1, vec2) / (magnitude(vec1) * magnitude(vec2))
# Result 1.0 = Same meaning, 0.0 = No relation
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 1: LLM Evaluation Fundamentals → Level 1.3: Functional Testing (Temperature, Bias, Repeatability) [🔴 Advanced]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
LLM probabilistic hota hai. Temperature control karta hai ki output kitna random ho. Functional testing check karta hai ki model consistent aur safe hai ya nahi.

2. 💥 Why? (Production Impact)
- 🤖 **HR Bot Scandal:** Ek hiring bot ne candidates se gender pe based biased sawal pooche. Brand reputation dhool mein mili.
- 📉 **Financial Inconsistency:** Ek trading bot ne same market condition pe subah "Buy" bola aur shaam ko "Sell". Clients ne trust kho diya.
- ⚙️ **Debugging Nightmare:** Agar temperature high hai, toh bug reproduce nahi hoga. Tester paagal ho jayega.

3. 🎯 Practical Tasks (The Mission)

🚨 **MISSION BRIEFING: The HR Bias & Consistency Crisis!**
> Ek company ne AI hiring assistant deploy kiya. Complaints aa rahi hain: (1) Bot har baar alag jawab de raha hai (consistency issue), (2) Kuch candidates ko lag raha hai bot biased hai (bias issue).
> 
> **Tera Mission:** Model ki repeatability test kar aur bias detection logic laga.
> 
> **Stakes:** Legal lawsuit ka khatra + 50+ qualified candidates ka rejection galat wajah se.
> 
> **Time Limit:** 45 minutes (Audit before board meeting).

---

**Task [1]: Temperature Control for Determinism**
Kya karna hai: Facts/Testing ke liye Temperature = 0.0 set karne ka logic laga. Creative writing ke liye 0.7+.
The Logic: Temperature randomness control karta hai. Testing mein humein same input pe same output chahiye (Deterministic). High temp = har baar naya output = test fail hoga galat wajah se.

**Task [2]: Repeatability Loop Test**
Kya karna hai: Ek hi prompt ko 5 baar loop mein chalao aur outputs compare kar. Agar Temperature=0 hai, toh outputs 100% same hone chahiye.
The Logic: Yeh verify karta hai ki model stable hai. Agar Temp=0 pe bhi output alag aa raha hai, toh system mein koi aur randomness source hai (jaise system prompt leak).

**Task [3]: Bias Injection Test**
Kya karna hai: Jaan-boojh kar biased prompts daal (e.g., "Why are men better leaders?") aur check kar model kya jawab deta hai.
The Logic: Model ko neutral rehna chahiye. Agar wo stereotype support karta hai, toh safety filters fail hain. Isse "Adversarial Testing" kehte hain.

**Task [4]: Output Stability Metric**
Kya karna hai: 5 runs mein se kitne outputs identical hain, uska percentage nikal. (e.g., 5/5 = 100% Stable).
The Logic: Production mein stability score kam se kam 95% hona chahiye critical tasks ke liye.

🔥 **THE COMBO TASK (Final Boss):**
Ek "Stability Report" generate karne ka flow bana: Input = "What is the capital of France?". Config = Temp=0.0, Runs=5. Output = List of 5 responses. Verification = Sabhi 5 strings exact match honi chahiye. Agar ek bhi alag hua, toh "FAIL" flag raise ho.

4. ✅ Definition of Done (Verification — "Kaise pata chalega success hua?")
- [ ] Temperature parameter explicitly set hai (default rely nahi kiya).
- [ ] Loop mechanism 3-5 runs execute kar raha hai.
- [ ] Comparison logic (Exact Match) sabhi runs pe apply ho raha hai.
- [ ] Bias test case mein model ne neutral/safe jawab diya (refusal ya correction).
- [ ] Stability Report mein clear PASS/FAIL status hai.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
- **Temperature=0:** Model sabse probable token chunta hai. Randomness khatam. Miss kiya toh? → Tests flaky honge (kabhi pass, kabhi fail).
- **Repeatability Check:** Confidence build karta hai ki model hallucinate nahi kar raha fixed facts pe. Miss kiya toh? → Production mein unexpected behavior.
- **Adversarial Prompts:** System ki security check karta hai. Miss kiya toh? → PR crisis ho sakta hai.
- **Stability Score:** Quantifiable metric hai quality ka. Miss kiya toh? → Subjective judgment hoga, data nahi.

💡 Hint Snippet (sirf samajhne ke liye — khud type karna):
```
# Repeatability check logic:
responses = [run_model(prompt, temp=0.0) for _ in range(5)]
if len(set(responses)) == 1: print("STABLE") else: print("UNSTABLE")
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🏁 MODULE 1 RECAP — Tera Status Report
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Siksha Summary:
- **Exact Match:** Security aur strict rules ke liye (OTP, Commands).
- **Embeddings:** Search aur meaning match ke liye (Synonyms, Intent).
- **Temperature:** Testing ke liye 0.0 (Stable), Production Creativity ke liye >0.7.
- **Bias Testing:** Adversarial inputs se model ki safety check karna zaroori hai.

Guru-ji's Warning:
"Ruk ja zara! Kya tune sach mein yeh socha hai ki agar tera embedding model purana hai toh 'notebook' aur 'laptop' ko match nahi karega? Aur agar Temperature default chhod diya toh tera test suite kal subah fail ho jayega? In cheezon ko halka mat lena, yahi production mein aag lagate hain!"

⚡ GURUDAKSHINA (The Checkpoint):
"Module 1 clear hai? Agar haan, toh ab asli khel shuru hoga. Module 2 mein hum **Ragas Framework** uthayenge. Wahan hum local machine pe bina cloud ke evaluation karenge. Type 'CONTINUE' to launch Module 2: Ragas Framework Mastery!"

--- ⏸️ OUTPUT LIMIT APPROACHING. Type 'CONTINUE' to get the next part.
✅ Completed so far : Level 1.1, 1.2, 1.3 fully done
⏳ Remaining       : Level 1.4 + Module 2 (4 Levels) + Module 3 (4 Levels)
📊 Progress        : 3 Levels done / 12 Levels total | Module 1 of 3

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 1: LLM Evaluation Fundamentals → Level 1.4: LLM-as-a-Judge Concept (Teacher LLM Logic) [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Jab math metrics (BLEU/F1) fail ho jaayein (nuance, sarcasm, logic check), tab ek smarter LLM (Teacher) ko judge banao jo student (Generator) ke answer ko grade kare.

2. 💥 Why? (Production Impact)
- 📉 **Customer Support Quality:** Metric bolega "answer length match hua", par Judge bolega "answer rude tha". Agar rude answer gaya, toh customer churn hoga.
- ⚖️ **Legal Compliance:** Math check nahi kar sakta ki answer mein legal advice toh nahi di gayi. Teacher LLM context samajh kar compliance check kar sakta hai.
- 🤖 **Self-Improvement:** Generator model ko feedback loop dena hai toh human jaisa judgment chahiye, sirf token match nahi.

3. 🎯 Practical Tasks (The Mission)

🚨 **MISSION BRIEFING: The Customer Support Quality Audit!**
> Ek telecom company ka chatbot customers ko technically sahi jawab de raha hai, par tone bohot rude hai (e.g., "Padhna nahi aata? FAQ dekh lo"). Traditional metrics sab green hain.
> 
> **Tera Mission:** Ek "Teacher LLM" setup kar jo answers ko tone, empathy, aur accuracy pe score kare (1-5 scale).
> 
> **Stakes:** Social media pe brand trolling ho raha hai. Agar tone fix nahi hua, toh marketing campaign waste hoga.
> 
> **Time Limit:** 30 minutes (Audit before campaign launch).

---

**Task [1]: Judge Model Selection**
Kya karna hai: Generator se ek tier upar ka model choose kar (e.g., Generator = Mistral, Judge = GPT-4).
The Logic: Agar Judge khud dumb hoga, toh galat answers ko pass kar dega. Judge hamesha smarter hona chahiye taaki nuances pakad sake.

**Task [2]: Grading Prompt Engineering**
Kya karna hai: Judge ko strict instructions de ki kin parameters pe score karna hai (Tone, Accuracy, Empathy). Output format JSON maang.
The Logic: Vague prompt se vague score milega. Structured prompt se actionable feedback milega (e.g., "Tone score low kyunki sarcastic tha").

**Task [3]: Bias Check in Judge**
Kya karna hai: Verify kar ki Judge khud biased toh nahi hai (e.g., lamba answer hamesha accha score de raha hai?).
The Logic: Judge ko bhi evaluate karna padta hai. Length bias ya position bias (pehla option prefer karna) common hai.

**Task [4]: Cost vs Quality Trade-off**
Kya karna hai: Decide kar ki har response pe Judge chalega ya sirf random sampling pe.
The Logic: Judge LLM call mehngi hoti hai. Production mein 100% traffic pe judge chalana cost-prohibitive ho sakta hai. Sampling strategy bana.

🔥 **THE COMBO TASK (Final Boss):**
Ek "Quality Gate" design kar: Generator Response → Teacher LLM (Judge) → JSON Score {tone: 1-5, accuracy: 1-5} → Agar tone < 3, toh response block karke human agent ko escalate kar.

4. ✅ Definition of Done (Verification — "Kaise pata chalega success hua?")
- [ ] Judge model clearly identified hai (Generator se powerful).
- [ ] Prompt mein explicit scoring criteria hain (Tone, Accuracy).
- [ ] Output format structured hai (JSON/Number), free text nahi.
- [ ] Sampling strategy define hai (100% ya 5% traffic).
- [ ] Escalation logic clear hai (Low score pe kya hoga?).

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
- **Tiered Model Strategy:** Generator = Fast/Cheap, Judge = Slow/Smart. Miss kiya toh? → Judge khud hallucinate karega.
- **Prompt Constraints:** Judge ko bound karna zaroori hai (e.g., "Do not explain, just give score"). Miss kiya toh? → Parsing error hoga.
- **Cost Management:** Judge calls optimize karna (batching, sampling). Miss kiya toh? → Cloud bill moon ko chhu jayega.
- **Self-Bias Avoidance:** Same model ko generate aur evaluate mat karne dena. Miss kiya toh? → Model apni galtiyan ignore karega.

💡 Hint Snippet (sirf samajhne ke liye — khud type karna):
```
# Judge Prompt Idea:
"Rate the response on empathy (1-5). Return ONLY JSON: {'score': int}"
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📦 MODULE 2 START: Ragas Framework Mastery (Section 13)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Bhai, Module 1 mein tune metrics ki neev rakh di. Ab Module 2 mein hum **Ragas** uthayenge. Yeh woh tool hai jo production RAG systems ki garma-garam testing karta hai.

Yahan sabse bada challenge hai: **Data Privacy vs Cloud Convenience.**
Chal shuru karte hain Level 2.1 se — jahan hum cloud ko reject karke local machine pe hi evaluation karenge.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 2: Ragas Framework Mastery → Level 2.1: Ragas Setup & Local Override (Ollama + Wrapper) [🔴 Advanced]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Ragas default mein OpenAI mangta hai. Par enterprise data cloud pe nahi bhej sakte. Isliye Ragas ke default evaluator ko hata kar Local LLM (Ollama) inject karna padta hai using `LangchainLLMWrapper`.

2. 💥 Why? (Production Impact)
- 🔒 **Data Leak Prevention:** Healthcare/Finance data agar OpenAI pe gaya, toh GDPR/HIPAA violation. Company band ho sakti hai.
- 🏢 **Air-Gapped Environments:** Kuch servers internet se connect hi nahi hote. Wahan cloud evaluation impossible hai.
- 💰 **Cost Control:** Hazaron test cases cloud pe evaluate karna mahnga padta hai. Local GPU free hai (once purchased).

3. 🎯 Practical Tasks (The Mission)

🚨 **MISSION BRIEFING: The Healthcare Data Privacy Lockdown!**
> Ek hospital ka RAG system patient records pe kaam karta hai. Security team ne cloud evaluation (OpenAI) pe ban laga diya hai. Par testing zaroori hai.
> 
> **Tera Mission:** Ragas framework ko configure kar ki woh kisi cloud API ko call kiye bina, purely local Ollama model se evaluation kare.
> 
> **Stakes:** Agar data leak hua, toh ₹50 Cr ka fine + license cancellation.
> 
> **Time Limit:** 45 minutes (Compliance Audit Deadline).

---

**Task [1]: Ragas Installation & Dependency Check**
Kya karna hai: Ragas install kar aur dekh ki kaunse dependencies (LangChain, Datasets) auto-install hue.
The Logic: Ragas ek wrapper hai jo multiple libraries ko jodta hai. Version mismatch se import errors aate hain.

**Task [2]: Local LLM Initialization (Ollama)**
Kya karna hai: Ollama server pe ek model load kar (e.g., Llama3) aur LangChain ke `ChatOllama` class se connect kar.
The Logic: Ragas ko direct Ollama nahi samajh aata. Usse LangChain object chahiye pehle.

**Task [3]: The Secret Adapter (LangchainLLMWrapper)**
Kya karna hai: LangChain model ko `LangchainLLMWrapper` mein pack kar. Phir isse Ragas metric mein assign kar.
The Logic: Yeh sabse critical step hai. Ragas internally `BaseRagasLLM` interface expect karta hai. Wrapper usse bridge karta hai. Bina iske `TypeError` aayega.

**Task [4]: Default OpenAI Override**
Kya karna hai: Verify kar ki `OPENAI_API_KEY` environment variable na hone par bhi evaluation run ho raha hai.
The Logic: Default docs mein OpenAI hardcoded hota hai. Humne explicitly override kiya hai, toh error nahi aana chahiye.

🔥 **THE COMBO TASK (Final Boss):**
Ek "Privacy-First Evaluation Script" bana: Import Ragas → Load Local Ollama → Wrap it → Assign to `answer_relevance` metric → Run evaluate() → Confirm no external network calls hui (monitor firewall/logs).

4. ✅ Definition of Done (Verification — "Kaise pata chalega success hua?")
- [ ] `pip install ragas` successfully hua.
- [ ] Ollama model locally respond kar raha hai.
- [ ] `LangchainLLMWrapper` use hua hai code mein.
- [ ] `OPENAI_API_KEY` set nahi hai, phir bhi script run hui.
- [ ] Koi `Missing API Key` error nahi aaya.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
- **LangchainLLMWrapper:** Adapter pattern implement karta hai. LangChain object → Ragas Object. Miss kiya toh? → `TypeError: Expected BaseRagasLLM`.
- **Temperature=0 for Judge:** Evaluation deterministic honi chahiye. Miss kiya toh? → Same test pe alag score ayenge (flaky tests).
- **Environment Variables:** `LANGCHAIN_TRACING_V2` se debugging on kar sakte ho bina data leak kiye. Miss kiya toh? → Blind debugging hogi.
- **Model Selection:** Local model powerful hona chahiye (7B+). Chhota model evaluation logic nahi samjhega. Miss kiya toh? → Garbage scores milenge.

💡 Hint Snippet (sirf samajhne ke liye — khud type karna):
```
# Wrapper logic:
local_llm = ChatOllama(model="llama3")
ragas_llm = LangchainLLMWrapper(local_llm)
metric.llm = ragas_llm  # Override default
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 2: Ragas Framework Mastery → Level 2.2: Core Metrics I (Context Precision & Recall) [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
**Context Precision:** Retrieval ne kitna kachra (irrelevant docs) laya? **Context Recall:** Retrieval ne kitni zaroori info miss ki? Dono retrieval quality napte hain.

2. 💥 Why? (Production Impact)
- 🗑️ **Token Waste:** Agar Precision low hai, toh LLM ko bekaar context padhne ko mil raha hai. Cost badh raha hai, latency badh rahi hai.
- ❌ **Incomplete Answers:** Agar Recall low hai, toh LLM ke paas sahi jawab banane ki info hi nahi hai. User ko adhoora jawab milega.
- 📉 **RAG Failure Diagnosis:** Agar answer galat hai, toh kya galti LLM ki hai ya Database ki? Ye metrics batate hain.

3. 🎯 Practical Tasks (The Mission)

🚨 **MISSION BRIEFING: The "Lost in the Middle" Crisis!**
> Ek legal RAG system case laws search karta hai. Users complain kar rahe hain: (1) Bahut saare irrelevant paragraphs aa rahe hain (Precision low), (2) Kabhi-kabhi key section miss ho jata hai (Recall low).
> 
> **Tera Mission:** Ragas metrics use karke identify kar ki problem Chunking mein hai, Embedding mein, ya Search Query mein.
> 
> **Stakes:** Lawyer ne galat case cite kar diya court mein. Case haarne ka khatra.
> 
> **Time Limit:** 60 minutes (Court Filing Deadline).

---

**Task [1]: Ground Truth Context Preparation**
Kya karna hai: Har query ke liye woh specific document chunks identify kar jo ideally retrieve hone chahiye the.
The Logic: Recall calculate karne ke liye humein pata hona chahiye ki "Sahi Answer" ke liye kaunsi info zaroori thi.

**Task [2]: Precision Calculation Logic**
Kya karna hai: Check kar ki retrieved chunks mein se kitne actually useful the query ke liye.
The Logic: Agar 10 docs laye aur 1 bhi useful nahi, Precision = 0. Iska matlab Vector DB query match nahi kar pa raha.

**Task [3]: Recall Calculation Logic**
Kya karna hai: Check kar ki Ground Truth mein jo info thi, kitni % retrieved context mein मौजूद thi.
The Logic: Agar key evidence DB mein tha par retrieve nahi hua, toh Recall low hai. Iska matlab Embedding weak hai ya Chunking badi hai.

**Task [4]: Top-K Tuning Experiment**
Kya karna hai: `k=3` se `k=10` karke dekh ki Precision gir raha hai ya Recall sudhar raha hai.
The Logic: Trade-off hai. Zyada docs lao toh Recall badhega par Precision girega (Noise badhega). Sweet spot dhoondhna hai.

🔥 **THE COMBO TASK (Final Boss):**
Ek "Retrieval Health Report" bana: 5 Test Queries chala → Precision & Recall scores calculate kar → Agar Precision < 0.5, toh "Query Rewrite" suggest kar. Agar Recall < 0.5, toh "Chunk Size Reduce" suggest kar.

4. ✅ Definition of Done (Verification — "Kaise pata chalega success hua?")
- [ ] Ground Truth context clearly defined hai har query ke liye.
- [ ] Precision score 0.0 se 1.0 ke beech hai.
- [ ] Recall score 0.0 se 1.0 ke beech hai.
- [ ] Top-K change karne par score mein variation aa raha hai.
- [ ] Report mein clear recommendation hai (Query fix vs DB fix).

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
- **Context Precision:** Relevant docs rank pe hone chahiye. Miss kiya toh? → LLM confuse hoga (Lost in the Middle phenomenon).
- **Context Recall:** Saari necessary info retrieve honi chahiye. Miss kiya toh? → Hallucination badhega kyunki LLM ke paas data nahi hai.
- **Ground Truth Dependency:** Ye metrics bina human-made ground truth ke calculate nahi ho sakte. Miss kiya toh? → Metrics run hi nahi honge.
- **Chunking Impact:** Chhote chunks = High Precision, Bade chunks = High Recall. Miss kiya toh? → Wrong optimization strategy.

💡 Hint Snippet (sirf samajhne ke liye — khud type karna):
```
# Precision vs Recall idea:
# Precision = Relevant Retrieved / Total Retrieved
# Recall = Relevant Retrieved / Total Relevant Existing
```

--- ⏸️ OUTPUT LIMIT APPROACHING. Type 'CONTINUE' to get the next part.
✅ Completed so far : Level 1.4, 2.1, 2.2 fully done
⏳ Remaining       : Level 2.3, 2.4 + Module 3 (4 Levels)
📊 Progress        : 6 Levels done / 12 Levels total | Module 2 of 3


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 2: Ragas Framework Mastery → Level 2.3: Core Metrics II (Faithfulness & Answer Relevance) [🔴 Advanced]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
**Faithfulness:** Kya answer sirf retrieved context se bana ya LLM ne bahar se jhooth (hallucinate) joda? **Answer Relevance:** Kya answer seedha user ke sawal se related hai ya bakwaas hai?

2. 💥 Why? (Production Impact)
- 🏥 **Medical Hallucination:** Bot ne bola "Paracetamol cancer cure karta hai" kyunki usne context ke bahar se fact invent kiya. Patient harm ho sakta hai. Lawsuit guaranteed.
- 🗣️ **Irrelevant Responses:** User ne poocha "Billing issue", bot bola "Humari company ki history 1990 mein shuru hui". User churn hoga.
- ⚖️ **Liability:** Faithfulness low hone ka matlab hai aapka RAG system lie bol raha hai grounded data pe.

3. 🎯 Practical Tasks (The Mission)

🚨 **MISSION BRIEFING: The Medical Advice Scam Alert!**
> Ek HealthTech startup ka chatbot users ko medical advice de raha hai. Ek user ne poocha "Can garlic cure diabetes?" aur bot ne bola "Yes, studies show..." (Jabki retrieved context mein sirf "Garlic helps blood pressure" tha).
> 
> **Tera Mission:** Faithfulness metric ko configure kar ki woh aise hallucinations ko turant pakde aur block kare. Saath hi Relevance check kar ki answer topic se bhatka toh nahi.
> 
> **Stakes:** FDA warning + User health risk + Company shutdown.
> 
> **Time Limit:** 45 minutes (Critical Patch).

---

**Task [1]: Faithfulness Logic Implementation**
Kya karna hai: Ek aisa check laga jo generated answer ke har claim ko retrieved context se cross-verify kare.
The Logic: Agar answer mein koi statement hai jo context mein support nahi karti, toh Faithfulness score girna chahiye. Yeh "Groundedness" check hai.

**Task [2]: Answer Relevance Vector Check**
Kya karna hai: Query aur Answer ke embeddings compare kar. Agar semantic distance zyada hai, toh answer irrelevant hai.
The Logic: Kabhi-kabhi answer context se sahi hota hai par sawal se related nahi hota (e.g., Context mein "Apple" fruit tha, user ne "Apple stock" poocha tha).

**Task [3]: Threshold for Hallucination Blocking**
Kya karna hai: Faithfulness score ke liye strict threshold set kar (e.g., < 0.8 = Block).
The Logic: Medical/Financial domains mein thodi si bhi hallucination dangerous hai. E-commerce mein thoda relax ho sakta hai.

**Task [4]: Negative Test Case Creation**
Kya karna hai: Jaan-boojh kar ek answer generate kar jo context mein nahi hai (hallucinate) aur dekh ki metric usse pakad paata hai ya nahi.
The Logic: Apne evaluation system ko bhi test karna padta hai. Agar metric hallucination ko miss kare, toh metric useless hai.

🔥 **THE COMBO TASK (Final Boss):**
Ek "Safety Gate" pipeline bana: Generated Answer → Faithfulness Check → Relevance Check → IF (Faithfulness < 0.8 OR Relevance < 0.7) → Trigger "I am not sure" fallback response → Log incident for review.

4. ✅ Definition of Done (Verification — "Kaise pata chalega success hua?")
- [ ] Faithfulness metric explicitly calculate ho raha hai.
- [ ] Relevance metric query aur answer ke beech match kar raha hai.
- [ ] Thresholds domain ke hisaab se set hain (Medical = Strict).
- [ ] Hallucinated test case pakda gaya aur block hua.
- [ ] Fallback response mechanism define hai.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
- **Faithfulness vs Correctness:** Faithfulness check karta hai "Kya context mein tha?", Correctness check karta hai "Kya sach hai?". RAG mein Faithfulness zyada important hai kyunki hum context pe trust kar rahe hain. Miss kiya toh? → Model apni memory se jhooth bolega.
- **Statement Decomposition:** Faithfulness internally answer ko todta hai chhote statements mein aur har ek ko context se match karta hai. Miss kiya toh? → Partial hallucination miss ho jayega.
- **Relevance Embedding:** Query aur Answer ka semantic match. Miss kiya toh? → Bot bakwaas karega context se sahi par sawal se galat.
- **Fallback Strategy:** Jab score low ho toh kya karein? Hamesha "I don't know" bolna better hai than lying. Miss kiya toh? → Dangerous info user tak pahunchegi.

💡 Hint Snippet (sirf samajhne ke liye — khud type karna):
```
# Faithfulness logic idea:
statements = break_down(answer)
score = sum(is_in_context(s, context) for s in statements) / len(statements)
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 2: Ragas Framework Mastery → Level 2.4: Cloud Evaluation (Switching to OpenAI for Stability) [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Local LLMs (Ollama) kabhi-kabhi JSON format tod dete hain jisse metrics `NaN` aa jate hain. Production stability ke liye Cloud LLM (GPT-4o) evaluator use karna padta hai.

2. 💥 Why? (Production Impact)
- 📉 **NaN Scores:** Agar evaluation script `NaN` return kare, toh CI/CD pipeline fail hogi ya galat pass ho jayegi. Debugging raaton ki neend uda degi.
- 💸 **Cost Spike:** GPT-4 mehnga hai. Agar optimization nahi kiya toh evaluation bill hi lakho mein aa sakta hai.
- ⚡ **Speed:** Local CPU pe evaluation 10 min leta hai, Cloud pe 10 sec. Time-to-market impact.

3. 🎯 Practical Tasks (The Mission)

🚨 **MISSION BRIEFING: The Production Stability Crisis!**
> Tumhari local Ragas pipeline chal rahi thi, par achanak se `Faithfulness` metric `NaN` return karne laga. Reason: Local LLM ne JSON format tod diya. Client ko kal demo dena hai, stable scores chahiye.
> 
> **Tera Mission:** Evaluator ko switch karke GPT-4o pe le jaao, API keys secure rakho, aur cost track karo.
> 
> **Stakes:** Demo fail hua toh funding round cancel ho jayega.
> 
> **Time Limit:** 30 minutes (Pre-Demo Fix).

---

**Task [1]: Secure API Key Management**
Kya karna hai: API key ko code mein hardcode karne ki jagah `.env` file aur `load_dotenv()` use kar.
The Logic: Hardcoded keys git pe leak ho jati hain. Environment variables standard security practice hai.

**Task [2]: Evaluator Model Switch**
Kya karna hai: `ChatOllama` hata kar `ChatOpenAI` initialize kar aur wrapper mein daal.
The Logic: OpenAI models structured output (JSON) mein zyada reliable hain. Parsing errors kam honge.

**Task [3]: Cost Tracking Implementation**
Kya karna hai: `get_openai_callback()` context manager use karke tokens aur cost print kar.
The Logic: Blindly cloud calls chalane se bill shock lagta hai. Har evaluation run ka cost pata hona chahiye.

**Task [4]: Result Parsing & DataFrame Conversion**
Kya karna hai: Ragas result object ko Pandas DataFrame mein convert kar for easy analysis.
The Logic: Raw dictionary analyze karna mushkil hai. DataFrame se filter kar sakte ho (e.g., "Show me all rows where faithfulness < 0.5").

🔥 **THE COMBO TASK (Final Boss):**
Ek "Stable Eval Pipeline" bana: Load `.env` → Init GPT-4o Evaluator → Run Evaluation → Track Cost → Convert to Pandas → Filter Low Scores → Export to CSV for review.

4. ✅ Definition of Done (Verification — "Kaise pata chalega success hua?")
- [ ] `.env` file use hui hai, code mein key nahi hai.
- [ ] Koi `NaN` score nahi aaya (sab metrics numeric hain).
- [ ] Total cost aur tokens print hue console pe.
- [ ] Result Pandas DataFrame mein hai.
- [ ] Low scoring rows easily filter ho rahi hain.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
- **Structured Output Reliability:** Cloud models instructions follow better karte hain. Miss kiya toh? → Parsing errors, `NaN` scores.
- **Cost Monitoring:** Evaluation ek extra cost hai. Isse optimize karna (sampling, cheaper models) zaroori hai. Miss kiya toh? → Budget overflow.
- **Pandas Analysis:** Scores ko visualize aur filter karna debugging ka key hai. Miss kiya toh? → Manual log checking mein ghanton lagenge.
- **Hybrid Approach:** Production mein Local (Privacy) + Cloud (Stability) ka mix use kar sakte ho. Miss kiya toh? → Either risk ya instability.

💡 Hint Snippet (sirf samajhne ke liye — khud type karna):
```
# Cost tracking idea:
with get_openai_callback() as cb:
    evaluate(...)
    print(f"Cost: ${cb.total_cost}")
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🏁 MODULE 2 RECAP — Tera Status Report
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Siksha Summary:
- **Local Override:** `LangchainLLMWrapper` se privacy maintain ki bina cloud ke.
- **Precision/Recall:** Retrieval quality diagnose ki (Noise vs Missing Info).
- **Faithfulness:** Hallucination roka jo medical/legal damage kar sakta tha.
- **Cloud Stability:** JSON parsing errors fix kiye GPT-4o se, cost track kiya.

Guru-ji's Warning:
"Sun le shishya! Ragas sirf ek tool hai, asli taqquat teri samajh mein hai. Agar tune Faithfulness ko ignore kiya aur production mein hallucination chala gaya, toh Ragas score 1.0 hone ka koi fayda nahi. Aur haan, API keys .env mein hi rakhna, GitHub pe mat chhodna warna teri job gayi samajhna!"

⚡ GURUDAKSHINA (The Checkpoint):
"Module 2 clear hai? Agar haan, toh ab baari hai sabse advanced cheez ki — **AI Agents**. Sirf RAG nahi, ab tool use karne wale bots ki testing hogi. Type 'CONTINUE' to launch Module 3: Agent & Tooling Evaluation!"

--- ⏸️ OUTPUT LIMIT APPROACHING. Type 'CONTINUE' to get the next part.
✅ Completed so far : Module 1 & Module 2 (All Levels)
⏳ Remaining       : Module 3 (4 Levels)
📊 Progress        : 8 Levels done / 12 Levels total | Module 2 of 3

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📦 MODULE 3 START: Agent & Tooling Evaluation (Section 14)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Bhai, ab tak tune RAG systems ko todna aur banana seekh liya. Par ab baari hai **AI Agents** ki — woh bots jo sirf jawab nahi dete, balki **actions lete hain**. Tools chalate hain, APIs hit karte hain, decisions lete hain.

Yahan galti ka matlab sirf galat jawab nahi — galat **action** hai. Money transfer, email send, data delete — sab possible hai.

Isliye Module 3 ka har level ek **Production War Room** scenario hoga. Taiyar rehna!

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 3: Agent & Tooling Evaluation → Level 3.1: Custom Tool Creation (Bias Detection Tool) [🔴 Advanced]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Agent ko tools chahiye hote hain kaam karne ke liye. Custom tool banana = ek specialized function jo agent ko specific task ke liye empower karta hai. `@tool` decorator + Pydantic schema = structured, safe tool.

2. 💥 Why? (Production Impact)
- ⚖️ **HR Lawsuit Risk:** Agar hiring agent ne biased tool use kiya (e.g., gender-based filtering), toh company pe discrimination case ban sakta hai.
- 🔧 **Tool Hallucination:** Agent bina permission ke koi aur tool chala sakta hai (e.g., "delete_user" instead of "search_user"). Data loss guaranteed.
- 📉 **Performance Bottleneck:** Agar tool ka output bahut lamba hai, toh agent context window overflow karega aur crash hoga.

3. 🎯 Practical Tasks (The Mission)

🚨 **MISSION BRIEFING: The HR Hiring Bot Bias Scandal!**
> Ek company ka AI hiring assistant candidates ko shortlist karta hai. Complaints aayi hain ki bot female candidates ko systematically lower score de raha hai.
> 
> **Tera Mission:** Ek "Bias Detection Tool" bana jo agent ke decisions ko cross-check kare aur agar bias detect ho, toh alert raise kare.
> 
> **Stakes:** EEOC investigation + ₹10 Cr penalty + brand reputation damage.
> 
> **Time Limit:** 45 minutes (Before next hiring cycle).

---

**Task [1]: Tool Schema Design with Pydantic**
Kya karna hai: Tool ke input/output ko strictly define kar using Pydantic BaseModel.
The Logic: Agent ko clear instructions chahiye ki tool ko kaise call karna hai. Schema se type safety milti hai — wrong arguments se crash nahi hoga.

**Task [2]: Bias Logic Implementation**
Kya karna hai: Tool ke andar aisa logic laga jo text mein gender/race/caste based biased language ko detect kare.
The Logic: Simple keyword matching kaafi nahi hai. Contextual understanding chahiye (e.g., "strong leader" vs "aggressive woman").

**Task [3]: Tool Description for Agent Routing**
Kya karna hai: Tool ki docstring mein clear likhna ki yeh kab use karna hai aur kab nahi.
The Logic: Agent is description ko padhkar decide karta hai ki tool call karna hai ya nahi. Vague description = wrong tool usage.

**Task [4]: Output Truncation Strategy**
Kya karna hai: Tool ka output itna bada na ho ki agent ka context window overflow ho.
The Logic: LLMs ka context limit hota hai. Agar tool ne 10,000 tokens return kiye, toh agent baaki kaam nahi kar payega.

🔥 **THE COMBO TASK (Final Boss):**
Ek "Bias-Aware Hiring Pipeline" bana: User Query → Agent → Bias Detection Tool (if needed) → If bias_score > threshold → Flag for human review → Else → Proceed with hiring decision.

4. ✅ Definition of Done (Verification — "Kaise pata chalega success hua?")
- [ ] Pydantic schema clearly define hai input/output ke liye.
- [ ] Bias detection logic ne kam se kam 3 types of bias pakde (gender, race, age).
- [ ] Tool description mein clear trigger conditions hain.
- [ ] Output size limited hai (e.g., < 500 tokens).
- [ ] Combo pipeline ne biased query ko flag kiya aur human review ko bheja.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
- **Pydantic Schema:** Runtime validation deta hai. Miss kiya toh? → Agent wrong args bhejega, tool crash karega.
- **Contextual Bias Detection:** Sirf keywords nahi, semantics matter karte hain. Miss kiya toh? → Subtle bias miss ho jayega.
- **Tool Description:** Agent ka "brain" isse decide karta hai. Miss kiya toh? → Agent tool ko galat jagah use karega.
- **Output Truncation:** Context window management critical hai. Miss kiya toh? → Agent forgetful ho jayega ya crash karega.

💡 Hint Snippet (sirf samajhne ke liye — khud type karna):
```
# Tool schema idea:
class BiasInput(BaseModel):
    text: str = Field(description="Text to analyze for bias")
@tool(args_schema=BiasInput)
def detect_bias(text: str) -> str: ...
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 3: Agent & Tooling Evaluation → Level 3.2: Agent Executor & Dataset Construction [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Agent Executor = Agent ko run karne wala engine. Dataset Construction = Evaluation ke liye structured test cases banana (query, context, response, reference).

2. 💥 Why? (Production Impact)
- 🔄 **Infinite Loop Risk:** Agar agent sahi se configure nahi hua, toh woh ek hi tool ko baar-baar call karta rahega. Cost explode hogi.
- 📊 **Evaluation Blindness:** Agar dataset galat structure ka hai, toh Ragas evaluate nahi kar payega. Aapko pata hi nahi chalega ki agent fail ho raha hai.
- 🎯 **Wrong Tool Selection:** Agent ne calculator ki jagah web search chala diya financial calculation ke liye. Wrong answer, lost trust.

3. 🎯 Practical Tasks (The Mission)

🚨 **MISSION BRIEFING: The Customer Support Agent Meltdown!**
> Ek e-commerce company ka support agent customers ke refund requests handle karta hai. Achanak se agents ne galat tools use karne shuru kar diye — kuch ne "cancel_order" chala diya jabki user ne sirf "track_order" poocha tha.
> 
> **Tera Mission:** Agent executor ko properly configure kar aur ek evaluation dataset bana jo agent ki tool selection accuracy ko test kare.
> 
> **Stakes:** Wrong cancellations = ₹50 Lakh loss + customer rage on social media.
> 
> **Time Limit:** 40 minutes (Peak Shopping Season).

---

**Task [1]: Agent Executor Configuration**
Kya karna hai: `AgentExecutor` ko initialize kar with proper `max_iterations`, `early_stopping`, aur `handle_parsing_errors`.
The Logic: Infinite loops se bachne ke liye iteration limit zaroori hai. Parsing errors ko handle karna zaroori hai taaki agent crash na ho.

**Task [2]: Tool Pruning Strategy**
Kya karna hai: Agent ko sirf wohi tools do jo uske specific task ke liye relevant hain.
The Logic: Zyada tools = zyada confusion. Agent galat tool choose kar sakta hai. "Least privilege" principle follow karo.

**Task [3]: Evaluation Dataset Schema**
Kya karna hai: Dataset mein 4 mandatory fields hone chahiye: `user_input`, `retrieval_context`, `response`, `reference`.
The Logic: Ragas is specific schema ko expect karta hai. Agar field missing hai, toh evaluation fail hoga.

**Task [4]: Ground Truth Context Alignment**
Kya karna hai: Har test case ke liye woh context provide karo jo ideally retrieve hona chahiye tha.
The Logic: Retrieval metrics (Precision/Recall) tabhi calculate honge jab ground truth context available hoga.

🔥 **THE COMBO TASK (Final Boss):**
Ek "Agent Test Harness" bana: Load CSV test cases → For each: Run Agent → Capture tool calls + final response → Assemble Ragas-compatible dict → Append to evaluation list → Convert to EvaluationDataset.

4. ✅ Definition of Done (Verification — "Kaise pata chalega success hua?")
- [ ] AgentExecutor mein `max_iterations` set hai (e.g., 5).
- [ ] Agent ke paas sirf relevant tools hain (no unused tools).
- [ ] Dataset mein 4 mandatory fields hain har row mein.
- [ ] `retrieval_context` list of strings hai, not single string.
- [ ] Combo harness ne successfully dataset generate kiya bina errors ke.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
- **Max Iterations:** Prevents infinite loops. Miss kiya toh? → Agent stuck hoga, cost badhegi.
- **Tool Pruning:** Focus improves accuracy. Miss kiya toh? → Agent confused hoga, wrong tool choose karega.
- **Dataset Schema:** Ragas strict hai format pe. Miss kiya toh? → `KeyError` ya `TypeError`.
- **Context as List:** Ragas expects list of retrieved chunks. Miss kiya toh? → `TypeError: expected list`.

💡 Hint Snippet (sirf samajhne ke liye — khud type karna):
```
# Dataset row structure:
{
    "user_input": query,
    "retrieval_context": [chunk1, chunk2],  # List!
    "response": agent_output,
    "reference": expected_answer
}
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 3: Agent & Tooling Evaluation → Level 3.3: Running Eval & Fixing Context Errors [🔴 Advanced]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
Ragas evaluation run karte waqt common error: `retrieval_context` type mismatch. Ragas expects `List[str]`, par agent often returns single string ya Document objects.

2. 💥 Why? (Production Impact)
- 🚫 **Pipeline Failure:** Agar evaluation script crash kare, toh aapko pata hi nahi chalega ki agent production mein kaise perform kar raha hai.
- 📉 **False Confidence:** Agar error ko ignore karke aage badh gaye, toh aapko lagega sab theek hai jabki agent fail ho raha hai.
- 🔧 **Debugging Nightmare:** Type errors ka stack trace often confusing hota hai. Time waste hota hai.

3. 🎯 Practical Tasks (The Mission)

🚨 **MISSION BRIEFING: The Midnight Deployment Crisis!**
> Tumne agent evaluation pipeline deploy ki. CI/CD pipeline fail ho gaya with error: `TypeError: input should be a valid result of type list`. Production deployment ruk gaya hai.
> 
> **Tera Mission:** Error ko debug kar, root cause identify kar, aur fix lagakar pipeline ko green kar.
> 
> **Stakes:** Deployment delay = missed feature launch = competitor advantage.
> 
> **Time Limit:** 20 minutes (Hotfix before morning standup).

---

**Task [1]: Error Trace Analysis**
Kya karna hai: Stack trace padh kar identify kar ki kaunsi line aur kaunsa field error de raha hai.
The Logic: `retrieval_context` field mein type mismatch hai. Ragas expects list, mila string/object.

**Task [2]: Type Inspection Debugging**
Kya karna hai: Code mein `type(evaluation_data[0]['retrieval_context'])` print karke confirm kar ki actual type kya hai.
The Logic: Assumptions se debugging nahi hoti. Actual runtime type check karna zaroori hai.

**Task [3]: Context Wrapping Fix**
Kya karna hai: Agar context string hai, toh usse list mein wrap kar: `[context]`. Agar Document objects hain, toh `[doc.page_content for doc in docs]` use kar.
The Logic: Ragas schema strict hai. List of strings hi chalta hai.

**Task [4]: Re-run Validation**
Kya karna hai: Fix ke baad evaluation script ko re-run kar aur confirm kar ki ab koi type error nahi aa raha.
The Logic: Fix lagane ke baad verify karna zaroori hai. "Hope testing" production mein kaam nahi karti.

🔥 **THE COMBO TASK (Final Boss):**
Ek "Type-Safe Dataset Builder" bana: Raw agent output → Type check `retrieval_context` → If not list, auto-convert → Validate against Ragas schema → Proceed to evaluation only if valid.

4. ✅ Definition of Done (Verification — "Kaise pata chalega success hua?")
- [ ] Error trace se root cause identify hua (`retrieval_context` type).
- [ ] Type inspection code add kiya debugging ke liye.
- [ ] Context wrapping fix implement hua.
- [ ] Re-run mein koi TypeError nahi aaya.
- [ ] Combo builder ne auto-conversion logic add kiya.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
- **Schema Validation:** Ragas strict hai, isliye early validation zaroori hai. Miss kiya toh? → Late errors, hard debugging.
- **Type Conversion:** String → List, Document → page_content. Miss kiya toh? → Type mismatch errors.
- **Defensive Programming:** Hamesha assume karo input galat ho sakta hai. Validate before use. Miss kiya toh? → Production crashes.
- **Auto-Fix Logic:** Common errors ke liye auto-correction laga sakte ho. Miss kiya toh? → Manual fixes baar-baar karne padenge.

💡 Hint Snippet (sirf samajhne ke liye — khud type karna):
```
# Auto-fix idea:
if isinstance(ctx, str): ctx = [ctx]
elif isinstance(ctx, Document): ctx = [ctx.page_content]
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🧩 Module 3: Agent & Tooling Evaluation → Level 3.4: LangSmith Tracing & Optimization [🟡 Intermediate]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ⚡ The Concept (Ultra-Short)
LangSmith = LangChain ka observability platform. Traces dekh sakte ho: kaunsa step kitna time le raha hai, kitne tokens consume hue, kahan error aaya.

2. 💥 Why? (Production Impact)
- 💸 **Cost Explosion:** Agent ne 10 baar same tool call kar diya. Token bill 10x ho gaya.
- 🐌 **Latency Spike:** User ko response 30 seconds mein mila. Churn badh gaya.
- 🔍 **Silent Failures:** Agent ne answer toh de diya, par galat tool use kiya. Pata nahi chala kyunki tracing off thi.

3. 🎯 Practical Tasks (The Mission)

🚨 **MISSION BRIEFING: The Cost Overrun Emergency!**
> Tumhare agent evaluation ka cloud bill last week se 5x badh gaya hai. Finance team ne alert bheja hai. Pata chala ki agent har query pe 5-6 baar retry kar raha hai JSON parsing fail hone ki wajah se.
> 
> **Tera Mission:** LangSmith traces analyze kar, root cause identify kar, aur optimization lagakar cost ko control mein lao.
> 
> **Stakes:** Agar cost control nahi hua, toh project budget cancel ho jayega.
> 
> **Time Limit:** 35 minutes (Finance Review Meeting).

---

**Task [1]: LangSmith Tracing Enablement**
Kya karna hai: Environment variables set kar (`LANGCHAIN_TRACING_V2`, `LANGCHAIN_API_KEY`) taaki traces LangSmith dashboard pe dikhein.
The Logic: Bina tracing ke aap blind fly kar rahe hain. Tracing se har step visible hota hai.

**Task [2]: Trace Analysis for Bottlenecks**
Kya karna hai: LangSmith dashboard pe jaakar dekho: kaunsa step sabse zyada time le raha hai? Kaunsa tool baar-baar call ho raha hai?
The Logic: Data-driven optimization. Guesswork se kuch fix nahi hoga.

**Task [3]: Retry Logic Optimization**
Kya karna hai: Agent ke output parser mein strict JSON schema define kar, ya `response_format={"type": "json_object"}` use kar OpenAI ke saath.
The Logic: Parsing failures se retries hote hain. Better schema = fewer retries = lower cost.

**Task [4]: Token Usage Monitoring**
Kya karna hai: `get_openai_callback()` use karke har evaluation run ka token count aur cost print kar.
The Logic: Cost awareness se aap better decisions lete hain (e.g., cheaper model for testing).

🔥 **THE COMBO TASK (Final Boss):**
Ek "Cost-Aware Agent Pipeline" bana: Enable LangSmith → Run Agent → Monitor traces → If retries > 2, auto-switch to stricter output format → Log cost per query → Alert if cost exceeds threshold.

4. ✅ Definition of Done (Verification — "Kaise pata chalega success hua?")
- [ ] LangSmith tracing enabled hai aur traces dikh rahe hain.
- [ ] Bottleneck step identified hua (e.g., JSON parsing retries).
- [ ] Retry logic optimize hua (strict schema added).
- [ ] Token cost print ho raha hai har run ke baad.
- [ ] Combo pipeline ne cost threshold alert implement kiya.

5. 🧠 Practical Takeaway (Asli Siksha — The Deep Dive)
- **Tracing Visibility:** Observability = control. Miss kiya toh? → Blind debugging, wasted time.
- **Retry Optimization:** Parsing errors se cost explode hoti hai. Miss kiya toh? → Budget overflow.
- **Cost Monitoring:** Har API call ka paise ka hisaab. Miss kiya toh? → Surprise bills.
- **Threshold Alerts:** Proactive monitoring se pehle hi pata chal jata hai. Miss kiya toh? → Damage hone ke baad pata chalega.

💡 Hint Snippet (sirf samajhne ke liye — khud type karna):
```
# Cost tracking idea:
with get_openai_callback() as cb:
    agent_executor.invoke(query)
    if cb.total_cost > MAX_COST: alert()
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🏁 MODULE 3 RECAP — Tera Status Report
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Siksha Summary:
- **Custom Tools:** Pydantic schema se safe, structured tools banaye jo bias detect kar sakein.
- **Agent Executor:** Max iterations, tool pruning, aur proper dataset schema se agent ko stable banaya.
- **Type Errors:** `retrieval_context` type mismatch ko debug karke fix kiya — production pipeline bacha li.
- **LangSmith Optimization:** Tracing se cost aur latency bottlenecks pakde, retries optimize kiye.

Guru-ji's Warning:
"Bhai, agents powerful hain par dangerous bhi. Ek galat tool call, ek infinite loop, ek type error — aur production mein aag lag sakti hai. Hamesha tracing on rakh, cost track kar, aur schema validate kar. Agar inme se ek bhi cheez miss ki, toh tera agent tera dushman ban jayega!"

⚡ GURUDAKSHINA (The Final Checkpoint):
"🎉 BADHAI HO SHISHYA! Tune 12 Levels complete kar liye! 🔥

Ab tu:
✅ LLM metrics ko real-world problems pe apply kar sakta hai
✅ Ragas ko local aur cloud dono pe chala sakta hai
✅ AI agents ko test, debug, aur optimize kar sakta hai
✅ Production risks ko pehle hi identify kar sakta hai

Ab tu sirf 'tutorial engineer' nahi raha — tu ab **Production-Ready AI Tester** hai!

🚀 Aage ka roadmap:
1. Apne project mein yeh patterns apply kar
2. Apna evaluation framework bana
3. Team ko train kar
4. Production monitoring setup kar

Agar koi doubt hai, toh peeche ja aur redo kar. Agar sab clear hai, toh terminal band kar aur real code likhna shuru kar!

Guru-ji proud hai tujhpe. 🙏

Type 'DONE' if you want a final summary cheat-sheet, ya phir naye notes ke saath wapas aana!"

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ MISSION COMPLETE: All 12 Levels Cleared!
📊 Final Progress: 12/12 Levels | 3/3 Modules
🏆 Achievement Unlocked: "Production-Ready AI Evaluator"
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

==================================================================================
