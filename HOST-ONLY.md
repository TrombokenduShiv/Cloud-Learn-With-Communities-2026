# 🔒 HOST-ONLY NOTES - Build • Automate • Ship

> **Do NOT publish this file in the student repo.** It contains the quiz answer key. Keep it in a private repo, a private Drive doc, or add it to `.gitignore`.

---

## 1. FEASIBILITY VERDICT

**Your plan as originally stated is not feasible in 45 minutes for online first-years.** A trimmed version is, and it keeps your whole story: n8n + a Google API key + vibecoding + cloud deploy + Betal quiz.

| Your original idea | Problem | What the guide does instead |
| ------------------ | ------- | --------------------------- |
| Every student runs **n8n in Docker locally** | Docker Desktop is a heavy install (virtualization, restarts, RAM) and you cannot debug 100 laptops online. Also, a **cloud-deployed website cannot reach `localhost`** on a student's laptop | Students use **n8n Cloud free trial** (browser only). **You** demo Docker live and tease the Docker event |
| "GCP API keys" | A raw Google Cloud Console API key needs a project, API enablement and restrictions: too much for beginners | Use the **Gemini API key from AI Studio** (it lives in a Google Cloud project, no billing for the free tier) |
| Deploy on **Cloud Run** | Needs a billing-enabled project, so many first-years without a card are blocked. Cloud Run also needs a container for a static site | Deploy on **Firebase Hosting (Spark plan)**, no card. Cloud Run stays as the "next level" link |
| Build + connect + deploy + vibecode in 45 min | Possible only if sign-ups are pre-done | **Step 0 pre-flight** moves all sign-ups to the day before |
| Cloud Learn registration at the start | Seats are first-come and the access-code email may arrive late | Registration is done **first**, and nothing later depends on the code email |

---

## 2. RISK REGISTER (highest risk first)

| # | Risk | Likelihood | Impact | Mitigation |
| - | ---- | ---------- | ------ | ---------- |
| 1 | Students skip pre-flight, so sign-ups eat the 45 minutes | High | High | Send a pre-flight reminder 48h and 12h before. Ask for a **"I'm ready" form** and keep a late-joiner buffer |
| 2 | **n8n trial expires after 14 days** and n8n deletes the workspace, so every student site dies | Certain | Medium | Tell students on the day. Export a workflow JSON. Use it as the hook for the Docker event |
| 3 | **Gemini key creation fails** (flagged project, `403`, age verification, college account blocked) | Medium | High | Personal Gmail only. Dry-run on a fresh account. Keep 3-4 **host keys** as emergency spares (never display them) |
| 4 | Gemini **free-tier limits** hit when 100 students test at once | Medium | Medium | Limits are per project. Tell students to wait 60 seconds on `429`, and try another Flash model |
| 5 | Cloud Shell + Firebase deploy breaks for some users | Medium | High | Dry-run on a brand-new Gmail **with no card**. Time-box to 5 minutes, then the GitHub Pages rescue lane |
| 6 | CORS or a "test vs production URL" mix-up | High | Medium | URL-bar test in Step 8. Pin the Common Issues table in chat |
| 7 | UI labels differ from the guide (n8n **Publish** vs **Active**, Gemini node field names) | Medium | Medium | Rehearse on the live UI the day before and fix labels in the README |
| 8 | **Google Meet limits** (free accounts have historically had a 60-minute cap on group calls) | Medium | High | Verify the cap for your account. Use a university/Workspace account, or split into two sessions. Run Part A + B in one session, Part C in another if needed |
| 9 | Public webhook gets spammed / quota burned | Low | Low | Explained in the Safety Check. Optional Level-3 header auth |
| 10 | Privacy: free-tier prompts may be used by Google to improve products | Certain | Low | Already stated in Step 7. Tell students not to enter personal data |
| 11 | Cloud Learn seats fill before registration | Medium | Medium | Registration is first on the agenda. Post the form link 24h early so keen students register in advance |

---

## 3. TIMELINE (today is **18 Oct 2026**; Cloud Learn applications close **31 Oct 2026**)

| When | Task |
| ---- | ---- |
| **Now to 20 Oct** | Pick the workshop date, **no later than ~27 Oct**. Book your meeting link. Ask Naman/Swadha for the **Partner Referral Codes sheet** and copy your chapter's code |
| 21 Oct | **Full dry-run** (section 4). Fix labels. Export the workflow JSON |
| 22 Oct | Publish the README, share the Step 0 checklist in WhatsApp, open the "I'm ready" form |
| T-48h / T-12h | Reminders, with the pre-flight link |
| T-1h | Test mic, screen share, a spare internet connection (mobile hotspot) |
| T+1 day | Share the recording, a **resource thread**, and a badge-race leaderboard idea |

---

## 4. DRY-RUN PROTOCOL (non-negotiable)

Do the **entire student path** on a **brand-new Gmail account with no card and no prior Google Cloud use**, on a normal laptop with a mobile hotspot. Time each step.

| Check | Pass if |
| ----- | ------- |
| AI Studio key creation | Works without billing, with no age/prepaid prompt |
| n8n Gemini node | The credential saves and a Flash model answers |
| Output field name | You can drag the generated-text field into **Respond to Webhook** |
| Publish/Active | The label in the guide matches the UI |
| URL-bar test | Plain text shows with `?topic=...` |
| Browser call from a local `index.html` | No CORS error |
| Cloud Shell on a card-less account | Opens and runs `npx firebase-tools` |
| Firebase deploy | `Hosting URL` prints in under 5 minutes |
| Total | Part B finishes in **50 minutes or less** |

After the dry-run: **export the workflow** (n8n workflow menu → Download) and save it as `workflow/betal-bot.json`. Do not hand-write it. Use it as the "instant import" rescue for stuck students.

**Docker demo command** (copy the current version from the n8n docs, *Hosting → Docker*, before the event):

```bash
docker volume create n8n_data
docker run -it --rm --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
```

Then open `http://localhost:5678`. Practise this once, **with Docker already running and the image already pulled**, to avoid a 5-minute download on stage.

---

## 5. ROLES (online)

| Person | Job |
| ------ | --- |
| **You (Host/Betal)** | Share screen, teach, play Betal |
| **Scorekeeper** | Tracks chat timestamps and points, posts the scoreboard |
| **3 Helpers** (Cloud team + Event & Outreach) | Each owns a chat segment, replies "send a screenshot of your console" and pulls complex cases into a breakout room |
| **Timekeeper** | Calls "T-2 minutes" on every step |

Chat protocol for help: **"Step number + screenshot + one sentence"**, nothing else.

---

## 6. ASSETS TO PREPARE

- [ ] Chapter referral code (from the Partner Referral Codes sheet) pasted into README
- [ ] Registration link pasted into README
- [ ] Final screenshots of each n8n step added to the README
- [ ] `workflow/betal-bot.json` (exported)
- [ ] Fallback `index.html` and a **pre-deployed host demo site**
- [ ] 3-4 spare Gemini keys
- [ ] Slides: only the architecture picture, the Betal title card and the scoreboard
- [ ] Reward for Vikramaditya / Navratnas

---

## 7. THINGS I COULD NOT VERIFY (check these in the dry-run)

- Exact **Gemini node** field names and which **Flash** models are free-tier available on the day (limits are shown only inside AI Studio per project)
- Whether new AI Studio users in India are asked for a **prepaid** plan before creating a key (some sources suggest this may apply to new users)
- Whether **Cloud Shell** runs for a project with no billing attached
- The exact **Publish vs Active** label in your n8n version
- The Google Skills **profile settings** path (UI changes often)

---

## 8. 🦇 THE BETAL SCRIPT + ANSWER KEY

**Opening line (dramatic voice):**
> *"Raja Vikram... main Betal hoon. Main ek kahaani sunaunga. Agar tune jawab jaante hue bhi chup rehna chuna, toh tera sar tukde-tukde ho jayega. Par agar tu galat bolega... toh bhi Betal ko mazaa aayega. Sunne ke liye taiyaar ho?"*

**Reminder:** nobody answers until you say *"Vikram, jawab do!"*

---

### 🍛 Tale 1 - The Midnight Biryani (autoscaling / serverless)

**Betal:** *"Ek hostel ke bahar ek bhaiya ne apna biryani-order website banaya. Ek chhota sa server, bas. Exam ki raat, 11 baje, poore hostel ne ek saath 'order' dabaya. Website ka dum nikal gaya. Bhaiya ro pade, aur biryani thandi ho gayi."*

**Riddle:** What should the bhaiya do so this never happens again, without paying for a giant server all year?

- A) Buy the biggest server and keep it on 24×7
- B) Ask the hostel to order in 5-minute slots
- C) Move to a serverless platform like **Cloud Run** that adds copies when busy and shrinks when quiet
- D) Delete the order button

✅ **Answer: C.** *Moral:* pay for what you use, and let the platform scale with demand. (A works but he pays all night for an empty kitchen.)

---

### 🔑 Tale 2 - The Leaked Key (secrets)

**Betal:** *"Ek student ne apna Gemini key seedha apni website ke code mein likh diya, aur GitHub pe daal diya. Agle din uska quota khatam, website band. Usne Gemini ko gaali di."*

**Riddle:** What was the *real* mistake?

- A) Using AI at all
- B) Choosing a dark theme
- C) Putting a secret where **every visitor can read it**
- D) Using GitHub

✅ **Answer: C.** *Moral:* secrets live in the **backend** (like n8n), never in the website. If one leaks, **delete and recreate** it immediately.

---

### 🌍 Tale 3 - The Faraway Kitchen (region / latency)

**Betal:** *"Ek startup ke saare users Mumbai mein the. Par unhone paisa bachane ke chakkar mein app ek door desh ke server pe daal di. Users bole: 'Bhai, itna slow kyun?'"*

**Riddle:** What is the best first fix?

- A) Add more emojis
- B) Deploy the service in the **region nearest the users** (e.g., `asia-south1`)
- C) Tell users to buy faster Wi-Fi
- D) Rewrite everything in a faster language

✅ **Answer: B.** *Moral:* distance is **latency**. Put compute close to users, and close to the data it talks to.

---

### ⏳ Tale 4 - The Trial That Vanished (quotas / lifecycle)

**Betal:** *"Raju ne ek free trial pe apni viral website banayi. Chaudah din tak sab mast. Pandrahvein din: sannata. Workspace gayab."*

**Riddle:** What should Raju have done on **Day 1**?

- A) Prayed
- B) **Exported his workflow** and planned where to host it long-term (paid plan or self-hosting)
- C) Created 50 trial accounts
- D) Blamed the cloud

✅ **Answer: B.** *Moral:* free tiers have **expiry dates and quotas**. Always plan your exit and keep your backups.

---

### 🌙 Tale 5 - The 2 AM Bug (revisions / rollback)

**Betal:** *"Raat ke 2 baje, ek developer ne naya version deploy kiya. Subah exam-portal pe error ka toofan. Usne ghabra ke poora code dobara likhna shuru kar diya."*

**Riddle:** What is the safest *first* move?

- A) Rewrite the code from scratch
- B) **Switch traffic back to the previous working revision**, debug later
- C) Delete the whole service
- D) Turn off the phone

✅ **Answer: B.** *Moral:* **rollback first, debug later.** Cloud Run keeps every revision for exactly this reason.

---

### ⚔️ Tie-breaker (sudden death)

**Betal:** *"Cloud ka matlab kisi aur ka computer. Toh batao: tumhara password strong rakhne ki zimmedari kiski?"*

- A) Google
- B) **You**
- C) The Wi-Fi
- D) Betal

✅ **Answer: B.** *Moral:* **shared responsibility.** The provider secures the data centre, you secure your account.

---

### 👑 Crowning line

> *"Shabash, Vikram! Tune Betal ko haraya. Aaj se tu hai... **Vikramaditya of GDG CU**."*
