---
title: Frequently Asked Questions
description: Frequently asked questions about Drupal or WordPress sites on Pantheon.
category:
  - getting-started
keywords: getting started, faqs, sites, pantheon, plans, developing, security
---
## Getting Started

### Can I put production sites on Pantheon?

Yes. Thousands of live production sites run on Pantheon.

### What versions of Drupal does Pantheon support?

Pantheon supports Drupal 6 and 7, as well as development sandboxes for Drupal 8.

### What versions of WordPress does Pantheon support?

Pantheon supports the most recent release of WordPress via [upstream](https://github.com/pantheon-systems/WordPress), which includes platform integration plugins and a pre-configured wp-config.php.

### How much does Pantheon cost?

Pantheon is free for developers. Our live site plans currently start as low as $25 monthly for personal sites, and $100 for professional sites. Learn more on [our pricing page](https://pantheon.io/pricing).


### Where are the Pantheon servers located?

All Pantheon servers are currently located in the United States. We have plans to expand to Europe, but we don't have an ETA for when they will be available for end-users.

You can use a [CDN](/docs/articles/drupal/content-delivery-network-cdn-for-file-distribution/) for rapidly serving files from multiple locations. In most cases, sites running on Pantheon in the U.S. perform faster than sites running on local hosting, even if the user is halfway around the world.

Transatlantic hops in are usually 200-300ms, while Pantheon can usually speed up site page load times by seconds.

### Can I run non-Drupal applications on Pantheon?

This is not officially supported, but the PHP runtime is complete. Some users have experimented with running applications with custom PHP code.

### Does Pantheon have FTP or shell access?

Pantheon supports toggling between local development mode using `git push` to transfer all code changes, and an on-server development mode, which provides access to the codebase via SFTP.

Direct SSH access is not supported, but you are able to directly interface with mysql, use CLI tools ([Terminus](https://github.com/pantheon-systems/cli), [drush](/docs/articles/local/drupal-drush-command-line-utility/), [WP-CLI](#Does-Pantheon-support-WP-CLI?), and SFTP files.


### How does Pantheon work with DNS?

Pantheon can handle any internet domain name you point at it. DNS configuration is still your responsibility at this time, but our [going live](/docs/articles/going-live) instructions provide you with the necessary IP addresses and/or CNAME records to configure with your DNS provider. Also see [Domains and SSL Tool](/docs/articles/sites/domains) for more information.

In order for your site to begin "listening" for your domain, you must first become a paying customer. We consider placing a real domain on on a site to be the point at which the site starts to go live.


## Developing Sites

### Can Pantheon run sites on highly available server clusters?

Yes. Pantheon sites run on a highly available clustered infrastructure. The primary upstream provider is Rackspace.

### Can I use my own Git repository (e.g GitHub)?

Not at the moment, but we're looking for a way to support it that allows us to maintain tight integration with our workflow visualization and tools.

### Does Pantheon support Drupal Multisite?

No. Pantheon's architecture is designed to provide high performance and a rich feature set for individual Drupal sites. There are inherent risks when running multisite. Individual sites can end up in states of configuration that make module or Drupal core updates impossible to do across all the sites. The codebase also becomes a single point of failure.

Our solution is to deliver granular resources and powerful code management tools so that users who want to run a large portfolio of sites can do so easily, without running the risks inherent in multisite.

### Does Pantheon support WordPress Multisite?

No. While WordPress multisites have been successfully installed on the Pantheon platform, it is not a supported development practice due to [known issues](/docs/articles/wordpress/wordpress-known-issues#site-networks-/-multisite).

### Does Pantheon support Drush?

Yes. Pantheon comes with Drush pre-integrated and with [@alias files pre-generated](https://pantheon.io/blog/drush-aliases-available) for you to use in your local environment.

### Does Pantheon support WP-CLI?

Yes. [Terminus](https://github.com/pantheon-systems/cli) incorporates WP-CLI commands so that users can perform operations on the Pantheon platform.

### Does Pantheon support local development?

Yes. Local development is a great best practice, and Pantheon supports a wide array of local development tools (e.g. MAMP, WAMP, Homebrew, etc).

### How does cron work with Drupal on Pantheon?

The platform will use Drush to run cron on an hourly basis automatically. More fine-tuned cron control is in development. If you need to run cron more frequently, you are free to do so using your own timing system and Drush aliases.

### How does cron work with WordPress on Pantheon?

WordPress runs its own internal cron-like system as visitors load your site. You can also use external services to schedule and create tasks. For more information, see [Cron for WordPress](/docs/articles/wordpress/cron-for-wordpress).

### Do you support ffmpeg transcoding?

We don't currently have support for transcoding. We do not have plans to add this feature. However, it is possible to run a site on the platform and integrate with a third-party transcoding service.

### How do I increase the maximum execution time limit for a PHP script?

The best way to do this by calling the PHP function [set\_time\_limit()](http://php.net/manual/en/function.set-time-limit.php) in your routine that takes more time.

## Caching and Performance

### What version of Apache Solr does Pantheon run?

We're currently testing out integration strategies for Solr with our next-generation infrastructure. When we deploy it, it will almost certainly be the latest stable Solr available at that time.


## Support

### What support is available for Pantheon?

For paid customers, we provide 24x7 platform-wide monitoring for Pantheon sites and technical support via priority support tickets and IRC. We also have enterprise support plans available that offer Service Level Agreements and 24x7 on-call support.

Read more about [getting support](https://pantheon.io/docs/articles/getting-support/) and our support offerings on [our pricing page](https://pantheon.io/pricing).


## Security

### Is the Pantheon platform PCI compliant?

Because PCI certifications have yet to catch up to modern cloud infrastructures, Pantheon cannot currently offer PCI compliance out of the box. If this is a hard requirement for your project, please contact us to discuss details.
