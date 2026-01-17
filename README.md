# SOB-2026-Genesis

**The Genesis Assignment: Proof of Identity**

This assignment tests your ability to generate cryptographic keys, sign messages, and submit a proof via a GitHub Pull Request.

## Objective
Prove that you possess a valid Secp256k1 keypair by digitally signing your GitHub handle. This confirms your identity without revealing your private key.

## Instructions

### 1. Fork & Clone
Fork this repository and clone it to your machine:
```bash
git clone https://github.com/[your-username]/SOB-2026-Genesis.git
cd SOB-2026-Genesis
```

### 2. The Challenge
Write a script (in **Python** or **TypeScript**) to:
1.  Generate a random **Secp256k1** keypair.
2.  **Sign** the following message with your Private Key:
    "SOB-2026-[Your-Exact-GitHub-Handle]"
3.  Output your **Public Key** and the **Signature**.

**Note**: Do not use high-level "wallet" libraries (like `bitcoinlib` or `ethers.js`). Use lower-level cryptographic libraries (e.g., `ecdsa` / `hashlib` for Python, `elliptic` / `crypto` for Node) to show you understand the primitives.

### 3. The Submission
Create a new file in the `submission/` directory named `[your-handle].json`.

**Path**: `submission/yogendra-17.json` (example)

**Content**:
```json
{
  "handle": "your-github-username",
  "public_key": "your_public_key_hex",
  "signature": "your_signature_hex"
}
```
*   `handle`: Your exact GitHub username (case-sensitive).
*   `public_key`: Hex verification key (compressed or uncompressed).
*   `signature`: Hex DER-encoded signature (SHA-256 hash of the message).

### 4. Verify Locally
Before pushing, verify your submission works.

**Setup**:
```bash
# Set up a virtual env (if you haven't already)
python3 -m venv venv
source venv/bin/activate
pip install ecdsa
```

**Run Verification**:
```bash
python .github/workflows/verify.py
```
If you see `SUCCESS`, you are ready.

### 5. Submit PR
Commit your changes and push to your fork:
```bash
git add submission/
git commit -m "feat: Submission for [your-handle]"
git push origin main
```
Open a Pull Request to the main repository. The automation will check your work.

## Validation Details
We use a Python script (`verify.py`) to cryptographically prove your submission:
1.  It reads your `handle`, `public_key`, and `signature`.
2.  It reconstructs the challenge message: `"SOB-2026-[handle]"`.
3.  It uses `ecdsa` to verify that `signature` corresponds to that message and your `public_key`.
