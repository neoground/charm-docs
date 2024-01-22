---
key:     core.mailman
title:   Mailman
section: Core Modules
nav:
  prev:
    page: core.logging
    icon: prev
    name: Logging
  next:
    page: core.bbq
    icon: next
    name: Queue (BBQ)
---

# ->>  Mailman <<-

<div class="card card-body" markdown="1">
In the digital realm, communication often traverses the ether, reaching out to far-flung entities within the digital cosmos. The Mailman module is akin to your trusty droid, adept at handling messages across various protocols and drivers. Equipped with the SMTP driver by default, it gracefully extends its capabilities to other message APIs or email service providers, ensuring your transmissions are relayed accurately across the vast expanses of the code galaxy. 
</div>

## ->> Methods

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/mailman1.jpg" alt="Section Heading Image" /></div>

Below is a table summarizing the available public methods of the `Mailman` class:

| Method          | Signature                                                                   | Description                                                                                                                                                          |
|-----------------|-----------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| setDriver       | `setDriver(string $name, mixed $data = null): self`                         | Sets the driver for the Mailman instance.                                                                                                                            |
| compose         | `compose(): Mailman`                                                        | Creates a new email, returning a cloned instance of Mailman.                                                                                                         |
| addAddress      | `addAddress(string $email, string $name = ''): self`                        | Adds a recipient to the email.                                                                                                                                       |
| addCC           | `addCC(string $email, string $name = ''): self`                             | Adds a CC address to the email.                                                                                                                                      |
| addBCC          | `addBCC(string $email, string $name = ''): self`                            | Adds a BCC address to the email.                                                                                                                                     |
| addUser         | `addUser(object $user): self`                                               | Adds a user as a recipient to the email.                                                                                                                             |
| addCurrentUser  | `addCurrentUser(): self`                                                    | Adds the authenticated user as a recipient to the email.                                                                                                             |
| addAttachment   | `addAttachment(string $path, string $name = ''): self`                      | Adds an attachment to the email.                                                                                                                                     |
| setTextContent  | `setTextContent(string $msg): self`                                         | Sets the text content of the email.                                                                                                                                  |
| setHtmlContent  | `setHtmlContent(string $msg): self`                                         | Sets the HTML content of the email.                                                                                                                                  |
| setSubject      | `setSubject(string $name): self`                                            | Sets the subject of the email.                                                                                                                                       |
| setTemplate     | `setTemplate(string $name, array $data = [], bool $combined = false): self` | Sets the HTML content by template, with an optional combined text version (this template has the same name as the HTML template, just `_html` replaced with `_text`. |
| getBody         | `getBody(): string`                                                         | Retrieves the body of the email.                                                                                                                                     |
| getTextBody     | `getTextBody(): string`                                                     | Retrieves the plain text body of the email.                                                                                                                          |
| getFrom         | `getFrom(): string`                                                         | Retrieves the "from" address of the email.                                                                                                                           |
| getUser         | `getUser(): null/object`                                                    | Retrieves the user set on the email.                                                                                                                                 |
| isSuccess       | `isSuccess(): bool`                                                         | Checks if the email was sent successfully.                                                                                                                           |
| getErrorMessage | `getErrorMessage(): null/string`                                            | Retrieves the error message, if any.                                                                                                                                 |
| send            | `send(): self`                                                              | Sends the email.                                                                                                                                                     |
| getDriver       | `getDriver(): MailmanDriverInterface`                                       | Retrieves the driver instance.                                                                                                                                       |

</div>

## ->> Crafting and Dispatching Emails: Examples

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/mailman2.jpg" alt="Section Heading Image" /></div>

In the galaxy of code, transmitting messages across the digital cosmos is a venture of both art and science. Let's embark on a voyage through different scenarios of email dispatch using the Mailman module, each with a touch of the arcane and the futuristic.

### -> Example 1: Dispatch Using Template

In this example, we transmit a notification to Duke Nukem at `forever@example.com` using a template nestled in the `notification_template` directory:

```php
C::Mailman()->compose()
            ->addAddress('forever@example.com', 'Duke Nukem')
            ->setSubject('Notification from the Code Cosmos')
            ->setTemplate('notification_template', [
                'galactic_code' => 1337
            ], true)
            ->send();
```
The templates reside in `assets/templates/email/notification_template/email_html.twig` and `assets/templates/email/notification_template/email_text.twig`, steering the HTML and text renditions of the email respectively.

### -> Example 2: Dispatch Using Text and HTML Strings

If the idea of crafting a holographic message intrigues you, here's how you can manifest it:

```php
C::Mailman()->compose()
            ->addAddress('galactic.guardian@example.com', 'Galactic Guardian')
            ->setSubject('Distress Signal from Code Planet')
            ->setTextContent('Urgent: The Code Planet seeks your aid!')
            ->setHtmlContent('<strong>Urgent:</strong> The Code Planet seeks your aid!')
            ->send();
```
This snippet forges both text and HTML contents right within the code, ready to be transmitted across the ether.

### -> Example 3: Dispatch with Attachments

In certain quests, you may find the need to transmit digital artifacts alongside your messages:

```php
C::Mailman()->compose()
            ->addAddress('artifact.retriever@example.com', 'Artifact Retriever')
            ->setSubject('Artifact Transmission: Code Scroll')
            ->setTextContent('Attached is the legendary Code Scroll.')
            ->addAttachment(C::Storage()->getDataPath() . DS . 'code-scroll.txt', 'Code Scroll.txt')
            ->send();
```
In this illustration, a precious artifact, the Code Scroll, is attached to the email, ready to traverse the digital space to its destined retriever.

### -> Twig Templates: Crafting the Message Canvas

Templates are the canvas upon which your messages are painted. Utilizing Twig, both text and HTML templates are crafted with ease, residing peacefully within the `assets/templates/email` directory. Whether it's a text template narrating the tales of code, or an HTML template painting the digital cosmos, the process remains harmonious.

Each template directory should encapsulate two files: `email_html.twig` for the HTML rendition, and `email_text.twig` for the text rendition. The text template is a humble parchment, holding just text and variables, narrating the message in a simplistic yet profound manner. On the other side, the HTML template is a vibrant canvas, capable of rendering the aesthetics of HTML alongside the narrative.

The path to the template files is a journey in itself. For instance, if your template is named `galactic_notice`, the HTML and text templates would reside in `assets/templates/email/galactic_notice/email_html.twig` and `assets/templates/email/galactic_notice/email_text.twig` respectively, ready to narrate your messages across the digital cosmos.

All your ViewExtension methods are also available in these views.

</div>

## ->> Configuring Custom Connections

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/mailman3.jpg" alt="Section Heading Image" /></div>

Navigating through the email cosmos often necessitates the establishment of 
custom relay stations (SMTP servers or configuration for any driver) to ensure your messages reach 
their destined galaxies. Here's how you configure and utilize a custom SMTP / Provider connection 
via the YAML configuration and in code.

#### -> YAML Configuration

In your `connections.yaml` file, append the following snippet to the `emails` section, 
defining a custom SMTP connection named `galactic_relay`:

```yaml
emails:
  galactic_relay:
    driver: 'smtp'
    host: 'smtp.example.com'
    port: 587
    username: 'cosmic_communicator'
    password: 'stellar$transmissions'
    encryption: 'tls'
    fromname: 'Droid Droidson'
    frommail: 'communicator@example.com'
```

#### -> Dispatching Email Using Custom SMTP Connection

Armed with a custom SMTP relay, let's manifest an email transmission through the `galactic_relay` connection:

```php
C::Mailman()->setDriver('Smtp', 'galactic_relay')
            ->compose()
            ->addAddress('starship.captain@example.com', 'Starship Captain')
            ->setSubject('Hyperdrive Activation Code')
            ->setTextContent('Activate your hyperdrive with code: N3BUL4')
            ->send();
```

In this snippet, the `setDriver` method is invoked to switch the communication
channel to `custom_smtp`, as defined in your `connections.yaml`. The email, 
bearing the hyperdrive activation code, is then crafted and dispatched,
steered by the custom SMTP settings towards the Starship Captain awaiting 
in the distant digital stars.

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

The Mailman module empowers your application with a robust and flexible emailing system,
effortlessly integrating with various email services and APIs. Its intuitive interface
and extendable nature ensure your messages reach their destinations, whether they 
reside on your local server or across the expanse in external email service providers. 
As with the reliable droids in a galaxy far, far away, the Mailman module is an 
indispensable companion in your digital odyssey.

</div>
