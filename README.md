# WordPress Hosting cPanel: How Do You Install WordPress, Where Is WP Toolkit, and Which Plan Do You Actually Need? (Plan Table + the Limits Nobody Puts on the Sales Page)

cPanel hosting and WordPress hosting are usually the same server sold under two labels. Plenty of WordPress plans run on cPanel, with WordPress either pre-installed or one Softaculous click away. RackNerd's shared accounts work that way, and the cPanel version behind your account decides which install route you see when you log in.

What follows covers the three places people get stuck: finding the cPanel login, getting WordPress into the root directory instead of a `/wordpress` subfolder, and deciding whether a cPanel account or managed WordPress fits. RackNerd's stack, backups, billing cycles and cancellation terms are in the back half.

> **Quick pick:** one WordPress site and no appetite for server work? Take RackNerd's smallest shared cPanel tier, install through Softaculous, and leave the install directory field blank. Disk size is the main thing separating the tiers, and domains and databases are listed as unlimited across the shared range. 👉 [See RackNerd's current shared cPanel plans](https://bit.ly/RacKnerd)

## RackNerd's shared cPanel plans

RackNerd sells shared hosting in disk-sized tiers, all on cPanel, all with Softaculous and a free SSL certificate. The 200 GB tier is the one with a price that a public plan tracker has re-checked recently, so that's the one pinned below. Smaller tiers exist at lower prices, and the live number is whatever the cart shows after you pick a billing cycle.

| Plan | Disk and what's included | Price | Billing | Best for | Order |
| --- | --- | --- | --- | --- | --- |
| Shared, 200 GB | 200 GB disk, unlimited domains and databases, cPanel + Softaculous, free SSL, daily JetBackup | $15.59/mo (tracked 13 Nov 2026) | Monthly, annual, biennial, triennial | Several WordPress sites, image-heavy blogs, small agency portfolios | [Check the 200 GB tier](https://bit.ly/RacKnerd) |
| Smaller shared tiers | Same cPanel stack and limits, less disk | Shown in the cart | Monthly through triennial | A single blog, brochure site or test install | [See the entry tiers](https://bit.ly/RacKnerd) |

Two things about that table. The annual promotional rate often only appears after you switch the billing dropdown from Monthly to Annually, so a first glance at the cart can look more expensive than the plan actually is. And every tier sits on the same software stack:

- **LiteSpeed Enterprise with the LSCache plugin.** Caching happens at the server level, before a request reaches PHP, which is why a fresh WordPress install on this stack tends to feel quicker than the price suggests.
- **CloudLinux with PHP Selector.** You choose the PHP version per account rather than inheriting whatever the server runs globally. Useful when a plugin needs 8.2 and another site on your account still needs 7.4.
- **cpGuard WAF.** Filters malicious traffic before it reaches WordPress.
- **JetBackup, daily, stored off-site**, with roughly 30 days of retention.
- **A choice of locations at checkout**, including Los Angeles, New York, Germany, France and Singapore. Pick by where your visitors are, not where you are.
- **Free migration** from another cPanel host if you open a ticket with your old login details.

## What you can actually manage from cPanel

cPanel is a browser interface sitting on top of the server, and six areas cover almost everything a WordPress site needs. Nothing here requires SSH.

- **Files.** File Manager uploads, edits, compresses and permission-fixes files in the browser. FTP works too if you prefer a desktop client.
- **Databases.** MySQL databases with phpMyAdmin for direct table access. The MySQL Database Wizard creates the database, the user and the privileges in one pass.
- **Email.** Create accounts, set forwarders, tune spam filtering, read mail in webmail.
- **Domains.** Addon domains, subdomains, redirects and DNS records all live here.
- **SSL.** The SSL/TLS Manager installs and renews certificates.
- **Backups and security.** Backup creation and restore, password-protected directories, IP blocking and hotlink protection.

The panel's own Quick Start bar puts the five or six tools people actually open (WP Toolkit, Email Accounts, File Manager, phpMyAdmin, SSL/TLS) on the home screen, largely because the full feature list is long enough to be disorienting on first login.

## Three ways into cPanel, and why the login link keeps moving

The login path changes far more often than the panel does, and most "cPanel has disappeared" tickets turn out to be a moved button.

1. **From the client area.** In RackNerd's client area there's a direct "Login to cPanel" link once the account is active. Elsewhere the pattern is Manage Services → pick the domain → Manage → Control Panel → Login.
2. **From the welcome email.** The activation email carries a direct link plus the cPanel username and password. Keep it; the password isn't shown again in the panel.
3. **From a direct URL.** Many hosts still answer on `yourdomain.com:2082` (HTTP) or `:2083` (HTTPS), and some set up a `/cpanel` alias. This route is the least reliable of the three, since hosts increasingly disable port access in favour of single sign-on from the billing area.

If none of them work, the account may still be provisioning. RackNerd activates automatically, usually within minutes of payment, and the welcome email lands when it's done.

## Three ways to install WordPress

Softaculous is the fastest route on RackNerd. WP Toolkit is the newer cPanel-native option but only exists on cPanel & WHM version 92 and later. Manual installation is for odd setups, or for hosts that don't ship an installer.

### Softaculous, the one-click route

Open cPanel, find Softaculous Apps Installer under the Software section, click WordPress, then Install Now. Fill in the domain, site name, admin username, admin email and a strong password. Leave the install directory field blank if you want WordPress at the root of the domain. The install finishes in under a minute and your dashboard is at `yourdomain.com/wp-admin`.

Install the LiteSpeed Cache plugin straight afterwards. It's free, it's maintained by LiteSpeed, and it switches on the server-level caching the stack is built around.

### WP Toolkit, and why you may not see it

On cPanel & WHM 92 or later, WP Toolkit sits under Tools → Domains → WP Toolkit, and usually has an icon in the Quick Start bar. Older accounts on older builds still show the Softaculous installer or a Web Applications section instead. If a tutorial's menu doesn't match your screen, check the cPanel version before assuming you clicked wrong.

WP Toolkit handles more than installation: core and plugin updates, theme setup, admin password resets, security scans, backup and restore, and a one-click login to the WordPress dashboard without typing credentials.

### Manual installation, and the two steps people get wrong

Manual installs run in four stages: download WordPress, upload it, create a MySQL database and user, then visit the domain to finish. Two details account for most of the failures.

**The files land in a subfolder.** The zip extracts to a `WordPress` directory inside `public_html`. Select everything inside it, use File Manager's Move tool to shift the files up one level, then delete the empty folder. Skip this and your site lives at `yourdomain.com/wordpress` while the bare domain shows nothing.

**Privileges get missed.** In the MySQL Database Wizard, step three attaches the user to the database. Tick **All Privileges**. Without it WordPress will ask for database details in a loop.

When the installer prompts for a database host, use `localhost`.

One more thing worth checking before any of this: if you bought a plan sold as managed WordPress on cPanel, a working site is often already installed and waiting. Log in first, then decide whether you need a second install at all.

## cPanel hosting vs managed WordPress: decide by what you want to touch

The two aren't opposites, and treating them as a binary choice is where most comparison shopping goes wrong. Many WordPress plans ship with cPanel included, opened straight from the host's portal.

Sort yourself into one of three groups:

- **One WordPress site, no interest in files, databases or custom email.** Managed WordPress is the honest answer. Updates and caching get handled for you, and you'll never open cPanel unless something breaks.
- **Several sites, custom email addresses, a non-WordPress app in the same account, or hands-on control of databases.** A cPanel account is the better fit, and the skills transfer if you change hosts later.
- **Both.** Buy a WordPress plan that includes cPanel. Bluehost's web and WordPress plans both work this way, with cPanel opened from its portal at no extra login.

RackNerd's shared hosting sits firmly in the cPanel camp, not the managed WordPress camp. Review coverage of the stack notes there are no host-pushed core updates and no built-in staging environment, so WordPress maintenance stays your job. That's fine for anyone comfortable with Softaculous and a backup schedule, and a poor fit for someone who wants updates handled without thinking about it.

> 👉 [Start with a RackNerd shared plan and keep full control of the stack](https://bit.ly/RacKnerd)

## The costs and limits that don't make the sales page

**cPanel licensing is not always free.** Some hosts bill cPanel or specific panel features separately; on RackNerd's shared plans it's part of the account rather than a line item. Worth confirming on any host you're comparing.

**Server density affects your site.** Shared cPanel servers hold many accounts, and an overloaded box drags every site on it. The published resource policy limits shared space to public-facing websites, which rules out using it as cloud storage, backup storage or a video streaming box.

**Misconfiguration is the real security risk.** Password-protected directories, IP blocking and SSL are all there, but they only help if you use them. A weak cPanel password or a publicly accessible backup file undoes the rest.

**Backups are best-effort, not guaranteed.** RackNerd runs JetBackup daily to off-site storage with about 30 days of retention, free on shared plans. The terms describe it as a courtesy on a best-effort basis, with availability, frequency and restorability varying, and tell you to keep your own off-site copies. Restores are self-service from cPanel. Believe the terms over the marketing bullet.

**Cancellation needs notice.** Written notice through the client area, five days before the renewal date. Server data is removed immediately on cancellation. There's no money-back window in what's publicly documented, so treat the first payment as final and confirm current terms before checkout. Non-payment triggers a 10% late fee after three days, with termination seven days past the due date.

**The uptime SLA covers power and network transit, not your website.** The commitment is 99.9% monthly, with a credit of 2% of the monthly fee per additional completed hour, capped at 50% a month, claimed by ticket within 30 days. Scheduled maintenance of up to 180 minutes a month is excluded.

> 👉 [Check RackNerd's plan terms and current pricing before you commit](https://bit.ly/RacKnerd)

## FAQ

### Does installing WordPress on cPanel cost extra?

No. cPanel is part of the hosting account, and Softaculous or WP Toolkit installs cost nothing. You're paying for the plan, the disk and the resources.

### Where is WP Toolkit in my cPanel?

Tools → Domains → WP Toolkit on cPanel & WHM 92 and later. On older builds it isn't there, and Softaculous or the Web Applications installer is the route you have.

### How many WordPress sites can one cPanel account run?

Domains and databases are listed as unlimited on RackNerd's shared plans, so the practical ceiling is disk space, CPU and memory. The terms include an excessive-resource clause even though no numeric limit is published.

### Are backups automatic?

Daily JetBackup snapshots run on shared plans and are stored off-site for about 30 days, but they're described as a best-effort courtesy rather than a guarantee. Keep your own copies of anything you can't rebuild.

### Can I have cPanel and managed WordPress at the same time?

Yes, and it's common. Many WordPress hosting plans include cPanel, so you get the host handling WordPress updates alongside panel access for files, databases and email.

## Which one to buy

Match the plan to what you'll actually do with it:

- **A single blog or brochure site** → the smallest shared cPanel tier, WordPress via Softaculous, LiteSpeed Cache installed straight after. Bigger disks add capacity you won't fill.
- **Three or more WordPress sites, or custom email on the same account** → the 200 GB tier, where disk stops being the constraint before CPU does.
- **No interest in touching a control panel** → managed WordPress elsewhere. RackNerd's shared plans are self-managed by design, and that's the one expectation worth settling before you pay.

Three things to confirm in the cart before you enter card details: the billing cycle you've selected (switch it to Annually to see the promotional rate), the cancellation and refund terms as they stand today, and whether you need a migration ticket for an existing site. Everything else is reversible; those three aren't.

> 👉 [Pick a RackNerd shared cPanel plan and confirm the cart price](https://bit.ly/RacKnerd)
