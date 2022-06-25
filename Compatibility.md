# TODO
 - Choose "Browser vendor" vs "Relying Party"

# Summary

Each browsers should create Certificate Authorities (let's call them "Compatibility CA") for the sole purpose of signing certificates for "real" Certificate Authorities. The Compatibility CAs should have long validity period (e.g., multiple decades), but they should be used solely to sign short-term intermediate certificates for the "real" CAs. This will acheive two goals:
1. New "real" CAs can be created and they will immediatelly be trusted by old browser installations
2. Browser vendors can enforce regular CA audits by mandating successful audit pass for issuance of the new certificate

