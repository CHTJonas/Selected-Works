# CUADC Webmaster Handover Notes

So, I've finally managed to get around to doing a proper write up of this handover! What follows is an attempt to list everything you need to care about, as well as some stuff that inevitably you don't.

The broad list of things is as follows:

### The Main Website
The website is just a Wordpress instance running on the SRCF (I’ve set you up to be able to login, which you can do via https://cuadc.org/login/). It’s running a custom theme, which allows for some of the various custom page layout, menus etc, some custom plugins for Cambridge-specific bits (e.g. Raven login), and some off the shelf plugins for contact forms etc. There is also a sitemap plugin and an ‘anti-malware’ plugin. I have no idea what the use of these is, but Ben (CUADC Webmaster 2015-16) swore by them, and they apparently help him solve some issues that he hit with Wordpress vulnerabilities. The main website's canonical domain name is cuadc.org. We also own cuadc.co.uk and cuadc.com which should redirect to the .org domain name via HTTP 301 setup via an Apache .htaccess file.

I’ve attempted to remove all references to the previous committee (names wise) from the website, but have only hidden the profile pages for our committee to give you a template to work with. Rob Eagar very kindly produced custom image renders (from the photo shoot he did) for us to go on the page - if you want to do something similar again, you’ll have to ask him about that separately, as I’m guessing the secretary will have no idea what had to go on behind the scenes. In general the website cleaner than it was a few years ago, but could do with a complete style rewrite at some point in the future. And maybe updating to the latest Bootstrap release.

### Props Store Website
The props store website (https://propstore.cuadc.org) is another instance of Wordpress running a very simple Bootstrap theme. It's a bit of a work in progress and our SM rep, Amelia Parker, never quite finished it, however it's my understanding that she plans to continue working on it. All the props store photographs have been uploaded and are also on a Google Drive which I can share with you if you need. Each prop manifests itself as a post on the Wordpress platform with it's photo attached to the post. Posts needs to be tagged and categorised so that they can be searched using the Wordpress search functionality.

### CUADC Wiki
Again another work in progress, the wiki (https://wiki.cuadc.org) was an attempt to replace the old Camdram Infobase which had become disused of recent time and finally died sometime around the start of March. The wiki is intended to be used for technicians and actors to write helpful articles and how-to documents about the process of putting on a show in Cambridge. Any page or article on the Wiki can be edited by anyone so long as they have an account and are logged in. The login is handled by a MediaWiki plugin which integrates with the mod-ucam-webauth Apache plugin. Unfortunately the downside of this is that to view an article you need to authenticate with Raven. This will then automatically log you in. This should prove less of a problem as with the advent of Raven for Life, alumni get to keep their Raven accounts.

### Membership Management System
The MMS (https://membership.cuadc.org) can be used by Ordinary & Associate members to manage their membership options. It is currently a work in progress and the codebase is hosted on GitHub (https://github.com/CHTJonas/membership). The MMS is used to generate a list of email addresses for import into the members email list.

### Docushare
The Docushare is a website (really a collection of automatically-generated Apache indexes) that functions as a repository/object storage solution for CUADC documents and media. Currently this includes committee meeting minutes, the constitution, the job guides and a few other things. Documents should be uploaded in a standards-compliant format eg. PDF, HTML, RTF, TXT and images should be uploaded in a format that makes the most sense eg. EPS, PNG, JPEG et cetera.

### SRCF
The site runs on the SRCF web server. This runs Apache with PHP7 on Ubuntu 16.04 LTS. At the start of Michaelmas 2017 the SRCF completed an upgrade of their infrastructure which bumped the major version numbers of the software running on their web server. Everything seems to be operating normally however this is something to bear in mind. HTTPS for the website is handled by LetsEncrypt through the SRCF control panel.

The SRCF explicitly state that they are not responsible for backups. As such, there is a convenient script to backup the contents of all the CUADC websites by creating a TAR archive of the public_html folder and by dumping the MySQL databases. You will need to enter your GPG key id or generate one in order to encrypt the backups.

### DNS/Emails/Domains
DNS is managed through LoHo, which can be accessed here: https://cpanel1.loho.co.uk:2083 (login details are stored in the CUADC KeePassX database). We actually own cuadc.org, cuadc.co.uk and cuadc.com, with cuadc.org being the canonical one; the others simply 301 redirect. The emails are also all set up through LoHo as redirects. It’s done hierarchically to try and be a bit flexible - everyone has a canonical email (e.g. treasurer@cuadc.org) which redirects directly to their CRSID, and then any other emails that that person should care about (old email addresses they used to use, more general email addresses ‘e.g. jobs@cuadc.org) redirect to the canonical emails, so they only have to be changed in one place during email handovers (all of which should already have been done).


### Mailing Lists
As the result of a constitutional amendment during Lent Term 2018, the webmaster now administers all of the CUADC mailing lists. There are several mailing lists and the Committee Members responsible for them are best summarised in a table:

| List               | Used for                                     | Person responsible             |
| ------------------ | -------------------------------------------- | ------------------------------ |
| soc-adc-actors     | Actor vacancies                              | Actors' Reps                   |
| soc-adc-alumni     | Alumni contact                               | Membership Secretary           |
| soc-adc-committee  | Committee minutes and agendas                | Secretary                      |
| soc-adc-crew       | Crewing opportunities                        | TD, Technicians' Rep           |
| soc-adc-designers  | Design vacancies                             | Designers' Rep                 |
| soc-adc-freshers   | Fresher contact                              | Secretary, President           |
| soc-adc-gossip     | Shaft of Darkness discussion list            | Chief SoD                      |
| soc-adc-info       | Non-Constitutional emails and socials emails | Secretary, President           |
| soc-adc-members    | Constitutional emails __ONLY__               | Secretary                      |
| soc-adc-musicians  | Not really used                              | ???                            |
| soc-adc-panto-cast | CUADC/Footlights Pantomime                   | Panto producers                |
| soc-adc-panto-prod | CUADC/Footlights Pantomime                   | Panto producers                |
| soc-adc-production | Director & Producer vacancies                | Directors' Rep, Producers' Rep |
| soc-adc-techies    | Technical vacancies                          | Technicians' Rep, SM Rep       |
| soc-adc-writers    | Not really used                              | Directors' Rep                 |

Mailing lists should initially be set to the 'Restricted' mode, so that only Administrators and Moderators can post. The relevant reps should then have their membership status updated so that their moderated flag is set to off. There should also be some catch-all filters so that any emails from @cuadc.org or @adctheatre.com automatically get let through.

Emails that are not sent as plain text will have their HTML parts reduced or stripped, or their multipart alternative used. Emails with attachments should be automatically rejected *except* for the committee mailing list where they are allowed. This is important in order to comply with the University's Rules for the Sending of Bulk Email (https://www.uis.cam.ac.uk/about-us/governance/information-services-committee/rules-and-guidelines/other-guidelines/bulkemail)

Now would be a good time to mention that all the CUADC emails and lists attract a significant volume of spam. There is only so much that can be caught by a filter so a sizeable amount still reaches peoples' inboxes. There are some spam filters setup both at the LoHo end at in Mailman to try and mitigate this as best we can. The CUADC domains do not currently employ SPF, DMARC or any other anti-spam or -spoofing technologies.

### Freshers' Fair
As a side note to the mailing lists, I also ended up doing the subscriptions from the freshers fair. I had two tablets set up to take cam card scans (RFID) during the fair, which spit out CSVs that with a bit of python parsing can be pasted into the bulk subscription interfaces on mailman. The app was written a long time ago, has to run on fairly old android hardware as a lot of new hardware doesn’t support reading the MiFare Classic cards, and getting the files off the tablets is a pain (I ended up using bluetooth!)… It’s a bit messy! If you can come up with a better solution, by all means, but if I’m around, you’d be more than welcome to borrow the tablets (just make sure you have a USB battery bank/banks).

--

That's about it I think! If you have any questions, please just give me an email - I'll be more than happy to offer advice or help. I imagine there will definitely be some things I’ve forgotten about, but it should all be fairly simple.

__Charlie Jonas__  
*March 2018*
