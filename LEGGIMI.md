# Secret Santa – Via del Bianco Spino V&P

Nel pacchetto ci sono tre file:

- `index.html`: la pagina (intro, Babbo Natale, iscrizioni, estrazione)
- `face.jpg`: la foto di Babbo Natale
- `setup.sql`: lo script che prepara il database

Ti servono circa 15 minuti. Supabase e GitHub sono gratuiti.

---

## 1. Crea il database (Supabase)

1. Vai su **supabase.com**, registrati (va bene anche con l'account GitHub) e crea un **nuovo progetto**. Scegli un nome e una password del database (quella non ti servirà qui) e come regione una in Europa.
2. Aspetta un paio di minuti che il progetto sia pronto.
3. Nel menu a sinistra apri **SQL Editor** e poi **New query**.
4. Apri `setup.sql`, copia **tutto** e incollalo nell'editor.
5. **In fondo allo script** sostituisci `CAMBIAMI` con la password che userai come organizzatore, per esempio `'PanettoneSegreto24'`.
6. Premi **Run**. Deve comparire "Success".

## 2. Prendi i due codici del progetto

Premi il pulsante **Connect** in alto, oppure apri *Project Settings → API Keys / Data API*. Ti servono due valori:

- il **Project URL** (tipo `https://abcdefgh.supabase.co`)
- la chiave **pubblica**: la *publishable key* (`sb_publishable_…`) oppure, nei progetti più vecchi, la *anon public key* (una stringa lunga che inizia con `eyJ…`)

⚠️ **Non** usare mai la *secret key* o la *service_role key*.

Apri `index.html` con un editor di testo (Blocco note va bene). In cima trovi:

```js
const SUPABASE_URL = 'INCOLLA_QUI_PROJECT_URL';
const SUPABASE_KEY = 'INCOLLA_QUI_LA_CHIAVE_PUBBLICA';
```

Incolla i due valori tra gli apici e salva.

La chiave pubblica può stare nella pagina senza problemi: con lei si possono solo usare le funzioni del Secret Santa. Le tabelle non si leggono direttamente, e gli abbinamenti li vede solo chi ha il proprio codice personale.

## 3. Metti la pagina online (GitHub Pages)

1. Su **github.com** crea un nuovo repository **pubblico**, per esempio `secret-santa`.
2. Premi **Add file → Upload files** e carica `index.html` (quello modificato) e `face.jpg`. Poi premi **Commit**.
3. Vai in **Settings → Pages**. In *Build and deployment* scegli **Deploy from a branch**, poi il branch **main** e la cartella **/ (root)**. Salva.
4. Dopo un minuto circa il sito è online su `https://TUONOME.github.io/secret-santa/`.

In alternativa a GitHub puoi trascinare i due file su **Netlify** (account gratuito).

La foto e la pagina saranno pubbliche su internet per chiunque abbia l'indirizzo.

## 4. Usala

| Chi | Che link usa |
|---|---|
| **Tutti** | `https://TUONOME.github.io/secret-santa/` → lo mandi nel gruppo WhatsApp |
| **Tu (organizzatore)** | lo stesso link con `?admin` in fondo: `…/secret-santa/?admin` → chiede la password del punto 1.5 |

- Ognuno apre il link, preme **"Accendi sto cazzo di Natale"** e scrive il nome. Non servono account né email.
- Dopo l'iscrizione la pagina mostra un **link personale** con il pulsante **Copia**. La pagina si ricorda la persona su quel telefono, ma conviene salvare il link (per esempio mandandolo a sé stessi su WhatsApp). Serve se si apre la pagina da un altro telefono o browser, o dal browser interno di WhatsApp invece che da Chrome o Safari.
- Quando ci sono tutti, entri con `?admin`, premi **"Chiudi iscrizioni ed estrai"** e avvisi il gruppo: *"Estrazione fatta, riaprite il link!"*.
- Ognuno riapre il link e Babbo Natale gli dice a chi fare il regalo. Lo vede solo lui.

Se qualcuno si iscrive in ritardo: dal pannello premi **"Annulla e riapri iscrizioni"**, poi estrai di nuovo.

## Buono a sapersi

- **Supabase gratuito mette in pausa i progetti** dopo circa una settimana senza attività. Se la pagina dice "Non riesco a raggiungere il database", entra su supabase.com e riattiva il progetto: i dati restano.
- **Per cambiare la password organizzatore**: nell'SQL Editor riesegui solo l'ultima istruzione `update public.settings …` con la nuova password.
- **Chi perde il link personale** dopo l'estrazione non può più vedere il suo abbinamento. In quel caso l'unica soluzione è annullare e rifare l'estrazione.
