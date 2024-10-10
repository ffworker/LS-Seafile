# Seafile Configuration

## Seafile Details

- **Hostname**: `GH-SF`
- **IP**: `172.17.0.167`

### Web Login

- **Admin Emails**: 
  - `me@example.com`
  - `it@logserv.biz`
  - `logserv-it`
- **Password**: `!29Logserv75!`

### Linux Root Access

- **Login**: `root`
- **Password**: `29Logserv75`
- **Install Directory**: `/opt/seafile`

### Seafile Desktop Client (Windows)

- [Download Link](https://www.seafile.com/en/download/)

---

## NGINX Configuration

- **NGINX Proxy URL**: [http://172.17.3.3:81/nginx/proxy](http://172.17.3.3:81/nginx/proxy)
- **HTTP Forwarding**: Port `80` (`gh-sf.logserv.biz`)

---

## Sophos UTM Configuration

### Step 1: Log in to Sophos UTM

1. Open your browser.
2. Log in to the **Sophos UTM 9** web interface.

### Step 2: Define the Internal Server

1. Navigate to **Definitions & Users > Network Definitions**.
2. Click **New Network Definition**.
3. Fill in the following:
   - **Name**: `Internal Server - gh-sf.logserv.biz`
   - **Type**: Select `Host`
   - **IPv4 Address**: `172.17.0.167`
   - **Interface**: Leave as `Any`
4. Click **Save**.

### Step 3: Create the DNAT Rule (Network Address Translation)

1. Go to **Network Protection > NAT > DNAT/SNAT**.
2. Click **New NAT Rule**.
3. Set the following fields:
   - **Rule Type**: Choose `DNAT (Destination)`
   - **Traffic Source**: Set to `Any`
   - **Traffic Service**: Select the appropriate service (e.g., HTTP, HTTPS, or `Any`)
   - **Traffic Destination**: Select the public interface through which traffic arrives (typically `External (WAN) Address`)
   - **Destination Translation**: Choose the internal server you defined earlier (`Internal Server - gh-sf.logserv.biz`)
4. Click **Save**.

### Step 4: Configure Firewall Rule to Allow Traffic

1. Go to **Network Protection > Firewall > Rules**.
2. Click **New Rule**.
3. Set the following:
   - **Position**: Choose where to place the rule.
   - **Sources**: Select `Any`.
   - **Services**: Choose the specific service (e.g., HTTP, HTTPS) or select `Any`.
   - **Destination**: Select the internal server you defined earlier (`Internal Server - gh-sf.logserv.biz`).
   - **Action**: Set to `Allow`.
4. Click **Save**.

---

## Added to:

- **NGINX**: [http://172.17.3.3:81/nginx/proxy](http://172.17.3.3:81/nginx/proxy)
- **Sophos**: 
  - Firewall & NAT Rule
