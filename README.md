# March for Malayshia — Petition Hub

A public petition and resource hub for **Jalayshia "Malayshia" Alford, age 10**, and for Philadelphia's and Pennsylvania's missing children. Our goal is **100,000 signatures** calling for missing children to be treated as the emergency they are.

A Think Tank Solutions AI community effort.

## Live links

Both addresses serve the same page from the same files:

- **https://march-for-malayshia.web.app** (main address; the page's canonical link points here)
- https://think-tank-solutions-ai.web.app

## Stack

- **Firebase Hosting** for the static site (`public/`)
- **Cloud Firestore** for signatures, read and written directly from the page with the Firebase web SDK
- No accounts or logins: anyone can sign

The Firebase web config inside `public/index.html` is public by design. Access is controlled by `firestore.rules`, not by keeping that config secret.

## How signatures work

- **Public timeline:** each signature's name, city/location, relationship and message is saved to the `signatures` collection and shown on the public timeline. The count is the same on every phone, tablet and computer.
- **Private emails:** emails go to a separate `signature_contacts` collection that nobody can read from the web. They are never shown or shared.
- **No edits or deletes:** the rules allow creating a signature but never updating or deleting one, so no visitor can change or remove anyone's signature.
- The rules also check every field's type and length and reject anything with extra fields.

## Privacy note

As shown under the Sign button:

> Your name, city, relationship and message appear publicly on the timeline. Your email is kept private and never shown or shared. Signatures can't be edited or removed by anyone. Please don't include a child's full name, school, or address in your message unless you're their parent or guardian.

## Repository layout

| Path | What it is |
|---|---|
| `public/index.html` | The live petition hub page |
| `public/share.png` | Link-preview image (Open Graph / social cards) |
| `public/march-post.png`, `public/march-post-v2.png` | Shareable poster images |
| `firebase.json` | Hosting (two targets) and Firestore config |
| `.firebaserc` | Project and hosting-target mapping |
| `firestore.rules` | Security rules for signatures and private contacts |
| `firestore.indexes.json` | Firestore indexes |

## Deploying

Requires the [Firebase CLI](https://firebase.google.com/docs/cli) and access to the `think-tank-solutions-ai` Firebase project.

```bash
npm install -g firebase-tools
firebase login
# Site only (deploys to both addresses):
firebase deploy --only hosting
# Security rules and indexes:
firebase deploy --only firestore
```

Hosting targets in `.firebaserc`:

- `primary` → think-tank-solutions-ai.web.app
- `community` → march-for-malayshia.web.app

After deploying, check that both addresses return the same page.

## Credits

Built and maintained by **Think Tank Solutions AI** for the Alford family and every family still waiting for a call. The family's preferred spelling is **Malayshia**.

## License

See [LICENSE](LICENSE).
