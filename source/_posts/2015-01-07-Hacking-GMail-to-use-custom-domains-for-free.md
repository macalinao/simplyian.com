title: Hacking Gmail to use custom domains for free
date: 2015-01-07 13:00:22
tags:
- hack
- mailgun
- gmail
- frugal
---

It's pretty much common knowledge that Gmail is awesome. It's fast, connects seamlessly with the rest of your Google services such as Drive, has a cool app called [Inbox][inbox], and is overall an extremely powerful email service. However, to use it with a custom domain, you need to purchase [Google Apps][google-apps] for either $5 or $10/month, which for casual users is a bit unnecessary. On top of that, you don't even get all of the features a personal account gets, e.g. Inbox.

However, there's a free way to use your Gmail account with a custom domain: [Mailgun][mailgun].

![Mailgun Logo][mailgun-logo]

[Mailgun][mailgun] advertises itself as a set of "powerful APIs that enable you to send, receive and track email effortlessly." Reading that description, you may be wondering how a developer tool could allow you to use **Gmail with custom domains for free.** Basically, Mailgun has two components that allow you to do this: an email forwarding service and an SMTP server.

## Setup

First, [sign up with Mailgun][signup] using your Gmail email. **Do not** use your email with your custom domain, as it will cause problems later when you want to verify your account. Once you have clicked the confirm link, log in to the Mailgun website. You should be presented with a dashboard. Now on the right under "Custom Domains", click "Add Domain".

![Add Domain][add-domain]

Follow the instructions and set your DNS records with whoever manages your DNS.

Once you've done this, click on the "Routes" link on the top to set up email forwarding.

## Forwarding

![Routes][routes]

On this page, you want to click "Create New Route".

![Create New Route][create-new-route]

Then, on this page, enter the following information:

![Setup Routes][setup-routes]

Replace the emails within the quotation marks with the desired emails.

## Sending with SMTP

Next, we will set up our SMTP configuration so we can send emails from an actual server.

Underneath the "Domains" tab, click on your domain name.

![Domains][domains]

On this page, click "Manage your SMTP credentials" then "New SMTP Credential" on the next page.

![SMTP][smtp]

Type in the desired SMTP credentials.

Next, go to [the Accounts tab in your Gmail Settings][gmail-settings-accounts] and click "Add another email address you own". Once you open this window, enter the email address you wish to send from.

![Add Email][add-email]

Then, set the SMTP settings as follows.

![Email SMTP Settings][email-smtp-settings]

* Server: smtp.mailgun.org
* Port: 587
* Username: The full email address, e.g. "me@ian.pw"
* Password: Whatever you set in Mailgun

After clicking "Add Account", now you're done! Enjoy your free email service for up to 10,000 emails a month!

[inbox]: http://www.google.com/inbox/
[google-apps]: https://www.google.com/work/apps/business/
[mailgun]: https://mailgun.com/
[signup]: https://mailgun.com/signup
[gmail-settings-accounts]: https://mail.google.com/mail/u/0/#settings/accounts
[mailgun-logo]: https://raw.githubusercontent.com/mailgun/media/master/Mailgun_Primary.png

[add-domain]: /img/add-domain.png
[routes]: /img/routes.png
[create-new-route]: /img/create-new-route.png
[setup-routes]: /img/setup-routes.png
[domains]: /img/domains.png
[smtp]: /img/smtp.png
[add-email]: /img/add-email.png
[email-smtp-settings]: /img/email-smtp-settings.png
