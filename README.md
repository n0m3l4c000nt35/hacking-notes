# 💀 Hacking Notes 📝

## Assessment Methodologies: Information Gathering

### Passive Information Gathering

#### Website Recon & Footprinting

- Buscar: Direcciones IP, directorios escondidos de los motores de búsqueda, nombres, direcciones de email, números de teléfonos, direcciones físicas, tecnologías web usadas.
- `host <dominio>`
- Archivo `robots.txt`
- Sitemap
- Add-ons: `BuiltWith`, `Wappalyzer`
- `whatweb`
- [https://www.httrack.com](https://www.httrack.com)

#### Whois Enumeration

- `whois <dominio>`
- [https://who.is/](https://who.is/)

#### Website Footprinting With Netcraft

- [https://www.netcraft.com/](https://www.netcraft.com/)

#### DNS Recon

- `dnsrecon -d <dominio>`
- [https://dnsdumpster.com/](https://dnsdumpster.com/)

#### WAF With wafw00f

- `wafw00f <dominio>`

#### Subdomain Enumeration With Sublist3r

- `sublist3r -d <dominio>`

#### Google Dorks

- [Google Hacking Database](https://www.exploit-db.com/google-hacking-database)

#### Email Harvesting With theHarvester

- `theHarvester -d <dominio>`

#### Leaked Password Databases

- [https://haveibeenpwned.com/](https://haveibeenpwned.com/)

### Active Information Gathering

#### DNS Zone Transfers

- `dnsenum`
- Archivo hosts: `/etc/hosts` (Linux), `C:\Windows\System32\drivers\etc\hosts` (Windows)
- `dig axfr @<dns-server> <dominio>`
- `fierce -dns <dominio>`

#### Host Discovery With Nmap

- `sudo nmap -sn <direccion-ip>`
- `sudo netdiscover -i <interface> -r <direccion-ip>`
 
#### Port Scanning With Nmap

- `nmap <direccion-ip>`

## Introduction to Web Application Security Testing

### Introduction to Web App Security Testing

- 
