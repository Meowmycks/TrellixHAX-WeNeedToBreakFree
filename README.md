# Trellix HAX Write-Up - *We Need to Break Free*

## Challenge Description

Our large-scale scans of possible networked machines used by the opposite coast have produced an interesting result: an unprotected repository which bears the same telltale fingerprint of known enemy hosts. However, the contents of the repository appear to be arbitrary, lacking in any significance... A honeypot, perhaps? You'd better have a poke around this system, just to make sure.

## Step 1 - Reconnaiscance

Running an Nmap scan on the provided address, ```trellixhax-we-need-to-break-free.chals.io``` reveals open ports,
