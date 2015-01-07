---
layout: default
published: true
---

## Public API

Programmatic access to many of ZONZAs features is possible via our public API.
This allows clients to integrate ZONZA with other systems and perform reporting
tasks for example.

`http://api.zonza.tv` is a RESTful JSON-based API. Access is
controlled using your ZONZA username and API token. As of Jan 2015, it
currently supports:

### Items:
* Upload (non-accelerated, chunked)
* Download (non-accelerated, chunked)
* Metadata view and edit
* Fulltext and field-level search (including negation, sorting and pagination)
* Search faceting
* Search by date ranges
* Access to supporting files
* Still generation and view (full frame captures from video or pages from
  presentations etc.)
* Thumbnail generation and view (including custom thumbnails, e.g. For
  setting preview on a ZIP)
* Transcoding to
* Export to FTP location
* Deletion of assets, versions, transcodes
* Support for multiple item versions

### Jobs:
* Viewing the status of submitted ingests and other async tasks

### Collections:
* Create and view collections
* Deleting collections
* Item addition and removal

Full documentation is available at [http://api.zonza.tv:8080/docs]()
(password protected). Contact your Account Director for credentials.

## SSO Integration

### Why would I want this?
ZONZA has the ability to integrate with third-party authentications solution
which can simplify user management and enhance the end-user experience.

#### Terminology

| **SSO**   | <b>S</b>ingle <b>S</b>ign <b>O</b>n. An overarching term for centralized authentication where the user only has to sign in once to access many separate services |
| **SAML**  | A particular method for implementing SSO. A well supported standard. We use [SAML 2.0](http://en.wikipedia.org/wiki/SAML_2.0) |
| **IDP**   | **I**dentity <b>P</b>rovider. This is the place that ZONZA will contact if using SSO to find out whether to grant users access |
| **AD**    | **A**ctive <b>D</b>irectory. An organisational directory containing user information. Commonly used as the IDP |
| **XML**   | <b>X</b>tensible <b>M</b>arkup <b>L</b>anguage, the format in which SAML metadata configuration is exchanged |

### How does it work?
There are two options for user management in ZONZA:

1. (**We manage**, *default*) If the built-in user management is used then
   users are created, approved and deleted within a ZONZA administration panel
   by our helpdesk or optionally by users with administration privileges. If
   this option is chosen then we have the ability to automatically deactivate
   user accounts after a period of inactivity and also to force passwords to be
   reset after X number of days which ensures old users have their access
   revoked. We also block users (by IP) after X repeat failed logins for
   additional security.
2. (**Client manages**) Alternatively, ZONZA can delegate user management to a
   third party Single Sign On (SAML SSO) Identity Provider in which case all of
   this can be managed remotely. A major benefit is that the user does not have
   to remember another username and password since they can reuse the same
   credentials they use for their organizations' systems.

We recommend exploring the SSO route if a client already manages users
centrally since it means only managing users in one place and a single identity
for users across their organization and ZONZA. There is also the option of
    combining the two approaches if SSO does not work for all of the clients
    users.

### Great, how do we get started?
Setting up SAML integrations between a client and ZONZA is relatively
straightforward. The minimum we need to get started is to exchange our XML
metadata files describing our service and your IDP. Before proceeding, you will
need to have a SAML Identity Provider (IDP) already in place.

#### We provide:
* Our SAML metadata (always located at
  `https://<client_prefix.zonza.tv/saml2/metadata`,
  [example](https://zonza.tv/saml2/metadata). This should be configured into
  the client's IDP, preferably using   the URL (since the content can change
  over time)

#### You provide:
* Their corresponding SAML metadata file – This will be an `.xml` file that the
  client can download/copy from their IDP
* Confirmation as to what default user group(s) authenticated users get access
  to and what their default ingest group should be. We can also dynamically set
  this based on SAML attributes sent by the IDP
* Optional logout URL – This is the URL that end users are redirected to once
  they click logout, this for example could be a client intranet
* Option to logout of everything or just ZONZA when the user hits the logout
  button
* Option to allow NOSSO (No Single Sign On) login - This allows end users to
  bypass SAML and authenticate via the regular ZONZA login page e.g. this is
  typically required if the ZONZA instance is going to be accessed by users
  that do not not have a
  `https://<client_prefix>.zonza.tv/authentication/login/nosso/` SAML login. For
  these types of examples clients typically create a NOSSO link on their IDP
  landing page
* Option to send an email to new users (custom welcome message and title)


## Open Source

ZONZA makes use of many Open Source libraries and components and often
contributes improvements back to the community. We also selectively publish
projects created by our own team. All of our repositories can be browsed at
[{{site.github.owner_url}}]()

{% for repo in {{site.github.public_repositories}} %}
* {{repo.name}} - {{repo.description}}
{% endfor %}