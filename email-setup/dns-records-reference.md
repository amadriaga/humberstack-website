# DNS Records Reference for humberstack.com Email

## Email Routing Records (Auto-configured by Cloudflare)

When you enable Email Routing in the Cloudflare dashboard, these records are automatically added:

### MX Records
```
Type: MX
Name: @ (or humberstack.com)
Priority: 1
Value: isaac.mx.cloudflare.net

Type: MX
Name: @ (or humberstack.com)
Priority: 2
Value: linda.mx.cloudflare.net

Type: MX
Name: @ (or humberstack.com)
Priority: 3
Value: amir.mx.cloudflare.net
```

### SPF Record
```
Type: TXT
Name: @ (or humberstack.com)
Value: v=spf1 include:_spf.mx.cloudflare.net ~all
```

## Additional Recommended Records

### DMARC (Email Authentication & Reporting)
```
Type: TXT
Name: _dmarc
Value: v=DMARC1; p=quarantine; rua=mailto:dmarc@humberstack.com; ruf=mailto:dmarc@humberstack.com; fo=1
```

This tells receiving servers:
- `p=quarantine` - Put suspicious emails in spam (use `p=reject` for stricter policy)
- `rua=mailto:dmarc@humberstack.com` - Send aggregate reports here
- `ruf=mailto:dmarc@humberstack.com` - Send forensic reports here

### DKIM (If using third-party email service)

If you use Resend, SendGrid, Mailgun, etc., they'll provide DKIM records like:

```
Type: TXT
Name: resend._domainkey (or similar)
Value: [Provided by email service]
```

## Verification Commands

Check your DNS records from command line:

### Check MX Records
```powershell
nslookup -type=MX humberstack.com
```

### Check SPF Record
```powershell
nslookup -type=TXT humberstack.com
```

### Check DMARC Record
```powershell
nslookup -type=TXT _dmarc.humberstack.com
```

## Online Tools

Verify your email DNS setup:
- https://mxtoolbox.com/SuperTool.aspx?action=mx%3ahumberstack.com
- https://dmarcian.com/domain-checker/
- https://www.mail-tester.com/
