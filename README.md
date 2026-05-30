<h1>Hybrid Encryption Tool</h1>

<p>
Hybrid Encryption Tool is a secure, browser-based encryption utility that implements a modern hybrid cryptography approach for protecting sensitive data. The application combines AES-256-CBC symmetric encryption, PBKDF2 key strengthening, random Salt and Initialization Vector (IV) generation, and RSA-OAEP asymmetric encryption to provide strong data confidentiality and secure key exchange.
</p>

<p>
The tool is designed to encrypt plain text or JSON payloads entirely within the browser without requiring any server-side processing. All encryption operations are performed locally using the Web Crypto API, ensuring that sensitive information, encryption keys, and generated ciphertext never leave the user's device.
</p>

<h2>Encryption Workflow</h2>

<ol>
<li>The user provides a Plain Text or JSON Payload.</li>
<li>The user provides an AES Secret Key.</li>
<li>The user provides an RSA Public Key.</li>
<li>A random 16-byte Salt is generated for the transaction.</li>
<li>The AES Secret Key and Salt are processed using PBKDF2 with SHA-256 and 120,000 iterations to derive a strengthened AES-256 encryption key.</li>
<li>A random 16-byte Initialization Vector (IV) is generated.</li>
<li>The payload is encrypted using AES-256-CBC with the derived key and generated IV.</li>
<li>The encrypted binary data is converted to Base64 format.</li>
<li>The final <strong>part1</strong> value is constructed by concatenating:
    <ul>
        <li>Salt (32 hexadecimal characters)</li>
        <li>IV (32 hexadecimal characters)</li>
        <li>Base64 Encoded Ciphertext</li>
    </ul>
</li>
<li>The original AES Secret Key is encrypted using RSA-OAEP with SHA-256 and the supplied RSA Public Key.</li>
<li>The RSA encrypted AES Secret Key becomes <strong>part2</strong>.</li>
<li>The final encrypted request packet is generated in the following format:</li>
</ol>

<pre>
{
  "part1": "Salt + IV + Base64CipherText",
  "part2": "RSAEncryptedAESKey"
}
</pre>

<h2>Features</h2>

<ul>
<li>Encrypt Plain Text or JSON Payloads</li>
<li>AES-256-CBC Encryption</li>
<li>PBKDF2 Key Derivation with SHA-256</li>
<li>120,000 PBKDF2 Iterations</li>
<li>Random Salt Generation</li>
<li>Random Initialization Vector Generation</li>
<li>RSA-OAEP SHA-256 Key Encryption</li>
<li>Automatic Part1 and Part2 Generation</li>
<li>JSON Validation and Beautification</li>
<li>Copy and Download Options</li>
<li>Advanced Encryption Debug Information</li>
<li>Fully Offline Operation</li>
<li>No Server Communication</li>
<li>Responsive Modern User Interface</li>
<li>Web Crypto API Based Implementation</li>
</ul>

<h2>Security Information</h2>

<p>
All encryption operations are executed locally within the browser. No payloads, encryption keys, generated salts, initialization vectors, or encrypted data are transmitted, stored, logged, or shared with any external server. The application is intended for authorized testing, debugging, development, and secure data exchange scenarios where strong client-side encryption is required.
</p>

<h2>Technical Specifications</h2>

<ul>
<li><strong>Encryption Algorithm:</strong> AES-256-CBC</li>
<li><strong>Key Derivation:</strong> PBKDF2</li>
<li><strong>PBKDF2 Hash:</strong> SHA-256</li>
<li><strong>PBKDF2 Iterations:</strong> 120,000</li>
<li><strong>RSA Algorithm:</strong> RSA-OAEP</li>
<li><strong>RSA Hash:</strong> SHA-256</li>
<li><strong>Salt Length:</strong> 16 Bytes</li>
<li><strong>IV Length:</strong> 16 Bytes</li>
<li><strong>Ciphertext Encoding:</strong> Base64</li>
<li><strong>Salt Encoding:</strong> Hexadecimal</li>
<li><strong>IV Encoding:</strong> Hexadecimal</li>
<li><strong>Execution Environment:</strong> Browser Only</li>
<li><strong>Crypto Engine:</strong> Web Crypto API</li>
</ul>
