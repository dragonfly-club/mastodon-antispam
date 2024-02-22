# Mastodon anti-spam patch

## Background

Recently mastoadmins have been hit by a flood of spam posts. This patch will prevent spam posts from flowing into your instance, cutting off the hazzles of reporting, suspending, and removing spam from database procedures.

## Installation

`cd` into your mastodon installation directory:

```bash
# Download patch from github
wget https://raw.githubusercontent.com/dragonfly-club/mastodon-antispam/main/antispam.patch

# Modify according to your needs (optional)
vim antispam.patch

# Apply patch
git apply antispam.patch
```

And restart ingress sidekiq queue:

```bash
# As root
systemctl restart mastodon-sidekiq

# Or, if you have modified systemd services
systemctl restart mastodon-sidekiq-ingress
```

When spam posts hit your instance, your ingress sidekiq should log something like:

```
Rejected 荒らし.com spam from https://xxx.social/users/xxx with content <p><a href="https://荒らし.com/" target="_blank" rel="nofollow noopener noreferrer" translate="no"><span class="invisible">https://</span><span class="">荒らし.com/</span><span class="invisible"></span></a></p><p><span class="h-card" translate="no"><a href="https://mast.dragon-fly.club/@abc" class="u-url mention">@<span>abc</span></a></span> <span class="h-card" translate="no"><a href="https://mast.dragon-fly.club/@def" class="u-url mention">@<span>def</span></a></span> <span class="h-card" translate="no"><a href="https://mast.dragon-fly.club/@ghi" class="u-url mention">@<span>ghi</span></a></span><br /><span class="h-card" translate="no"><a href="https://mast.dragon-fly.club/@jkl" class="u-url mention">@<span>jkl</span></a></span></p>
```

## Advantages

No need for human intervention, the instance itself will handle all the process.

## Disadvantages

The post won't be reported, and the account won't be blacklist.