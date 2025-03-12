
**H2 Techniques and Tools for Content Discovery**  

### **Manual Discovery Techniques**  
- **`robots.txt`**:  
  - Reveals restricted paths (e.g., `/staff-portal`).  
  - Accessed via browser or `curl`.  

- **Favicon Analysis**:  
  - Use `curl` + `md5sum` to hash favicons.  
  - Match against the **OWASP Favicon Database** (e.g., identified `cgiirc` framework).  

- **`sitemap.xml`**:  
  - Lists public content (e.g., found `/s3cr3t-area`).  

- **HTTP Headers**:  
  - Use `curl -v` to view headers (e.g., uncovered `X-FLAG: THM{HEADER_FLAG}`).  

- **Framework Stack Analysis**:  
  - Check page source comments for framework clues (e.g., `/admin` portal with flag `THM{CHANGE_DEFAULT_CREDENTIALS}`).  

---

### **OSINT Tools & Methods**  
- **Google Dorking**:  
  - Use operators like `site:` to filter results (e.g., `site:example.com admin`).  

- **Wappalyzer**:  
  - Browser extension to identify tech stacks (CMS, frameworks).  

- **Wayback Machine**:  
  - Archive historical site versions (`https://archive.org/web/`).  

- **GitHub**:  
  - Search for exposed repos (passwords, source code).  

- **S3 Buckets**:  
  - Look for misconfigured AWS storage (URL format: `*.s3.amazonaws.com`).  

---

### **Automated Discovery Tools**  
- **FFUF**:  
  - Command: `ffuf -w wordlist.txt -u http://IP/FUZZ` (found `/monthly`).  

- **Dirb**:  
  - Scans directories using wordlists (e.g., `common.txt`).  

- **Gobuster**:  
  - Fast directory/file brute-forcing (discovered `/development.log`).  

- **Wordlists**:  
  - Use **SecLists** (`/usr/share/wordlists/`) for common paths.  

---

### **Key Findings**  
- Manual: `robots.txt` → `/staff-portal`, `sitemap.xml` → `/s3cr3t-area`.  
- OSINT: Google `site:` operator, S3 bucket URLs.  
- Automated: Tools like **FFUF** found `/monthly` and `/development.log`.  

**Tip**: Combine manual checks (precision) with automation (speed) for thorough discovery! 🔍









## W_hat Is Content Discovery?_

_Firstly, we should ask, in the context of web application security, what is content? Content can be many things, a file, video, picture, backup, a website feature. When we talk about content discovery, we’re not talking about the obvious things we can see on a website; it’s the things that aren’t immediately presented to us and that weren’t always intended for public access._

_This content could be, for example, pages or portals intended for staff usage, older versions of the website, backup files, configuration files, administration panels, etc._

_There are three main ways of discovering content on a website which we’ll cover._ **_Manually, Automated and OSINT_** _(Open-Source Intelligence)._

**Ques 1:** What is the Content Discovery method that begins with M?  
Ans 1: Manually

**Ques 2:** What is the Content Discovery method that begins with A?  
Ans 2: Automated

**Ques 3:** What is the Content Discovery method that begins with O?  
Ans 3: OSINT

## M_anual Discovery — Robots.txt_

_There are multiple places we can manually check on a website to start discovering more content.  
The robots.txt file is a document that tells search engines which pages they are and aren’t allowed to show on their search engine results or ban specific search engines from crawling the website altogether. It can be common practice to restrict certain website areas so they aren’t displayed in search engine results. These pages may be areas such as administration portals or files meant for the website’s customers. This file gives us a great list of locations on the website that the owners don’t want us to discover as penetration testers.  
Take a look at the robots.txt file on the Acme IT Support website to see if they have anything they don’t want to list — To do this open Firefox on the AttackBox, and enter the url:_ [_http://MACHINE_IP/robots.txt_](http://machine_ip/robots.txt) _(this URL will update 2 minutes from when you start the machine in task 1)_

Ques 1: What is the directory in the robots.txt that isn’t allowed to be viewed by web crawlers?  
Ans 1: /staff-portal

## Manual Discovery — Favicon

_The favicon is a small icon displayed in the browser’s address bar or tab used for branding a website._

![](https://miro.medium.com/v2/resize:fit:275/0*4F5-ge-SzJMJtnu1.png)

_Sometimes when frameworks are used to build a website, a favicon that is part of the installation gets leftover, and if the website developer doesn’t replace this with a custom one, this can give us a clue on what framework is in use. 

OWASP host a database of common framework icons that you can use to check against the targets favicon_ [_https://wiki.owasp.org/index.php/OWASP_favicon_database_](https://wiki.owasp.org/index.php/OWASP_favicon_database)_. 

Once we know the framework stack, we can use external resources to discover more about it.  
_**_Practical Exercise:  
_**_On the AttackBox, open firefox and enter the url_ [_https://static-labs.tryhackme.cloud/sites/favicon/_](https://static-labs.tryhackme.cloud/sites/favicon/) _here you’ll see a basic website with a note saying “Website coming soon…”, if you look at your tabs you’ll notice an icon that confirms this site is using a favicon.  
Viewing the page source you’ll see line six contains a link to the images/favicon.ico file._

![](https://miro.medium.com/v2/resize:fit:582/0*30pj1pDTT8BW6lu0.png)

_If you run the following command on the AttackBox, it will download the favicon and get its md5 hash value which you can then lookup on the  
_[_https://wiki.owasp.org/index.php/OWASP_favicon_database_](https://wiki.owasp.org/index.php/OWASP_favicon_database)_._

user@machine$:
==curl [https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico](https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico) | md5sum==

Ques 1: What framework did the favicon belong to?  
Ans 1: cgiirc

## M_anual Discovery — Sitemap.xml_

_Unlike the robots.txt file, which restricts what search engine crawlers can look at, the sitemap.xml file gives a list of every file the website owner wishes to be listed on a search engine. These can sometimes contain areas of the website that are a bit more difficult to navigate to or even list some old webpages that the current site no longer uses but are still working behind the scenes._

_Take a look at the sitemap.xml file on the Acme IT Support website to see if there’s any new content we haven’t yet discovered:_ [_http://MACHINE_IP/sitemap.xml_](http://machine_ip/sitemap.xml) _(open this in the FireFox browser on the AttackBox)._

Ques 1: What is the path of the secret area that can be found in the sitemap.xml file?  
Ans 1: /s3cr3t-area

## M_anual Discovery — HTTP Headers_

_When we make requests to the web server, the server returns various HTTP headers. These headers can sometimes contain useful information such as the webserver software and possibly the programming/scripting language in use. In the below example, we can see the webserver is NGINX version 1.18.0 and runs PHP version 7.4.3. Using this information, we could find vulnerable versions of software being used. Try running the below curl command against the web server, where the_ **_-v_** _switch enables verbose mode, which will output the headers (there might be something interesting!)._

==Command: curl [http://MACHINE_IP](http://MACHINE_IP) -v==

Ques 1: What is the flag value from the X-FLAG header?  
Ans 1: THM{HEADER_FLAG}

## M_anual Discovery — Framework Stack_

_Once you’ve established the framework of a website, either from the above favicon example or by looking for clues in the page source such as comments, copyright notices or credits, you can then locate the framework’s website. From there, we can learn more about the software and other information, possibly leading to more content we can discover._

_Looking at the page source of our Acme IT Support website (_[_http://_](http://10.10.28.226/)<ip>_), you’ll see a comment at the end of every page with a page load time and also a link to the framework’s website, which is_ [_https://static-labs.tryhackme.cloud/sites/thm-web-framework_](https://static-labs.tryhackme.cloud/sites/thm-web-framework)_. Let’s take a look at that website. Viewing the documentation page gives us the path of the framework’s administration portal, which gives us a flag if viewed on the Acme IT Support website._

Ques 1: What is the flag from the framework’s administration portal?  
Ans 1: THM{CHANGE_DEFAULT_CREDENTIALS}




## OSINT Google Hacking  Dorking:

_There are also external resources available that can help in discovering information about your target website; these resources are often referred to as OSINT or (Open-Source Intelligence) as they’re freely available tools that collect information:  
Google hacking / Dorking utilizes Google’s advanced search engine features, which allow you to pick out custom content. You can, for instance, pick out results from a certain domain name using the_ **_site:_** _filter, for example (site:_[_tryhackme.com_](http://tryhackme.com/)_) you can then match this up with certain search terms, say, for example, the word admin (site:tryhackme.com admin) this then would only return results from the_ [_tryhackme.com_](http://tryhackme.com/) _website which contain the word admin in its content. You can combine multiple filters as well. Here is an example of more filters you can use:_



Ques 1: What Google dork operator can be used to only show results from a particular site?  
Ans 1: site:

## O_SINT — Wappalyzer:_

_Wappalyzer (_[_https://www.wappalyzer.com/_](https://www.wappalyzer.com/)_) is an online tool and browser extension that helps identify what technologies a website uses, such as frameworks, Content Management Systems (CMS), payment processors and much more, and it can even find version numbers as well._

Ques 1: What online tool can be used to identify what technologies a website is running?  
Ans 1: wappalyzer

O_SINT — Wayback Machine:_

_The Wayback Machine (_[_https://archive.org/web/_](https://archive.org/web/)_) is a historical archive of websites that dates back to the late 90s. You can search a domain name, and it will show you all the times the service scraped the web page and saved the contents. This service can help uncover old pages that may still be active on the current website._

Ques 1: What is the website address for the Wayback Machine?  
Ans 1: [https://archive.org/web/](https://archive.org/web/)

O_SINT — GitHub:_

_To understand GitHub, you first need to understand Git. Git is a_ **_version control system_** _that tracks changes to files in a project. Working in a team is easier because you can see what each team member is editing and what changes they made to files. When users have finished making their changes, they commit them with a message and then push them back to a central location (repository) for the other users to then pull those changes to their local machines. GitHub is a hosted version of Git on the internet. Repositories can either be set to public or private and have various access controls. You can use GitHub’s search feature to look for company names or website names to try and locate repositories belonging to your target. Once discovered, you may have access to source code, passwords or other content that you hadn’t yet found._

Ques 1: What is Git?  
Ans 1: version control system

O_SINT — S3 Buckets:_

_S3 Buckets are a storage service provided by Amazon AWS, allowing people to save files and even static website content in the cloud accessible over HTTP and HTTPS. The owner of the files can set access permissions to either make files public, private and even writable. Sometimes these access permissions are incorrectly set and inadvertently allow access to files that shouldn’t be available to the public. The format of the S3 buckets is http(s)://_**_{name}._**[**_s3.amazonaws.com_**](http://s3.amazonaws.com/) _where {name} is decided by the owner, such as_ [_tryhackme-assets.s3.amazonaws.com_](http://tryhackme-assets.s3.amazonaws.com/)_. S3 buckets can be discovered in many ways, such as finding the URLs in the website’s page source, GitHub repositories, or even automating the process. One common automation method is by using the company name followed by common terms such as_ **_{name}_**_-assets,_ **_{name}_**_-www,_ **_{name}_**_-public,_ **_{name}_**_-private, etc._

Ques 1: What URL format do Amazon S3 buckets end in?  
Ans 1: .s3.amazonaws.com

A_utomated Discovery:_

**_What is Automated Discovery?_**

_Automated discovery is the process of using tools to discover content rather than doing it manually. This process is automated as it usually contains hundreds, thousands or even millions of requests to a web server. These requests check whether a file or directory exists on a website, giving us access to resources we didn’t previously know existed. This process is made possible by using a resource called wordlists._

**_What are wordlists?_**

_Wordlists are just text files that contain a long list of commonly used words; they can cover many different use cases. For example, a password wordlist would include the most frequently used passwords, whereas we’re looking for content in our case, so we’d require a list containing the most commonly used directory and file names. An excellent resource for wordlists that is preinstalled on the THM AttackBox is_ [_https://github.com/danielmiessler/SecLists_](https://github.com/danielmiessler/SecLists) _which Daniel Miessler curates._

**_Automation Tools_**

_Although there are many different content discovery tools available, all with their features and flaws, we’re going to cover three which are preinstalled on our attack box, ffuf, dirb and gobuster._

_On the AttackBox execute the following three commands, targeting the Acme IT Support website and see what results you get._

**Using ffuf:**

user@machine$ ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -u http://10.10.28.226/FUZZ

**Using dirb:**

user@machine$ dirb http://10.10.28.226/ /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt

**Using Gobuster:**

user@machine$ gobuster dir --url http://10.10.28.226/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt

Ques 1: What is the name of the directory beginning “/mo….” that was discovered?  
Ans 1: /monthly

![](https://miro.medium.com/v2/resize:fit:700/1*rZ8RpiWHluG3UUhoXu-G7A.png)

Ques 2: What is the name of the log file that was discovered?  
Ans 2: /development.log

![](https://miro.medium.com/v2/resize:fit:700/1*1FiY3IqbHhPOyYtIAgDShQ.png)