# Jekyll Workshop - Create your own online portfolio!

This template uses the [jekyll-bootstrap-resume-theme](https://github.com/nscharrenberg/jekyll-bootstrap-resume).
Specifics on the theme (such as the required data structures) can be found on that repository readme.

This workshop is split into 2 sections:
1. Basic Workshop (explained below) - Explains the basic usage of Jekyll. You don't need to know anything about programming, but it's a plus if you know git and basic programming.
2. [Advanced Workshop](https://github.com/msvincognito/static-site-workshop/wiki/Advanced-Static-Website-Generation) - Goes much more indepth and lets you create a website from scratch (or create your own gem-based theme). We expect you to know basic programming and terminal. (Preferably HTML, CSS, JS).

Furthermore, we also provide a collection of resources to help you get started here: [RESOURCES.md](RESOURCES.md)

Below we'll discuss the steps you have to take to get this template working on your own github-pages (repository/website).

## Step 1 - Clone this repository.
We made this repository available as a template. You can press the green button saying `Use this template` at the top right of this page.
You can then go through the normal repository creation by giving it a repository name, description and setting it to either public or private.

When done you can click the green button saying `Create Repository from template`.

HINT: Naming your repository `<your-username>.github.io` e.g `msvincognito.github.io` will make the website visible on that domain, else it'll be placed inside a subdirectory such as `<your-username>.github.io/<your-repository-name>`, e.g `msvincognito.github.io/static-site-workshop`.

NOTE: Your github-pages website will always be accessible, no matter your repository visibility.

## Step 2 - Setup Github Actions
If you would want your website to be deployed to github-pages each time you make a change to your master branch, then you'll need to do some additional permission/authorization steps.

First create a `personal-access-token` on github with scope "repo" (For private repositories) and "public" (for public repositories), [follow the guide provided by github](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) and copy the given access token. 

Then go to your Github repository Settings, and open the "Secrets" tab, then create a new secret and name it `JEKYLL_PAT`, and paste the `personal-access-token` that you copied to the value. Then save this, and now whenever you make a change to your master branch, an action will be started to make a new build of your website and deploy it to your github-pages site.

NOTE: This process may take a couple of minutes.

### Extra Configuration (Custom Domains or subdomains)

NOTE: For this workshop it's best **NOT** to use a custom domain, and to skip to Step 3.

We need to make some additional changes when we are using a custom domain (e.g `mydomain.com`) or use a different repository name then `<your-username>.github.io` where `<your-username>` is your github username.

Open the `_config.yml` file and change the items depending on the cases below:
#### Custom Domain (no subdirectory)
In case we have a custom domain such as `mydomain.com`) then we need to change:
`url: ""` to `url: "mydomain.com"`.

#### Custom Domain (with subdirectory)
In case we have a custom domain such as `mydomain.com/resume`) then we need to change:
`url: ""` to `url: "mydomain.com"` and `baseurl: ""` to `baseurl: "/portfolio"`.

#### Custom Repository Name
In case your repository is not `<your-username>.github.io` where `<your-username>` is your github username, then we need to change `baseurl: ""` to `baseurl: "/<your-repository-name>"`, where `<your-repository-name>` is the name of your repository. e.g `baseurl: "/static-site-workshop"`.

#### Examples
URL: msvincognito.github.io
```yaml
baseurl: ""
url: ""
```

URL: msvincognito.github.io/static-site-workshop
```yaml
baseurl: "/static-site-workshop"
url: ""
```

URL: mydomain.com
```yaml
baseurl: ""
url: "https://mydomain.com"
```

URL: mydomain.com/resume
```yaml
baseurl: "/resume"
url: "https://mydomain.com"
```

## Step 3 - Changing the Profile Details & Image
### 3.1 Details
We want to change some important details that will make your site be about you.
Open `_config.yml`, here we need to change a couple of items:
1. `title` Change the title to whatever you want to name your website. (This is what SEOs and search engines will display your website as, so pick carefully e.g `Portfolio Noah Scharrenberg`.
2. `email` and `portfolio.info.email`
3. `description` Change this to whatever website description you want. SEOs and search engines will likely use this to display a short piece of text when being displayed in e.g google.
4. `baseurl` and `url` were discussed in Step `2`.
5. `portfolio.info.name.firstname` and `portfolio.info.name.lastname`
6. `portfolio.info.location` Change this to whatever you want to be displayed below your name, e.g your address, a catchy phrase, or something else.
7. `portfolio.info.phonenumber` Change this to your own phonenumber, or anything else. (Could also be left empty)

NOTE: I think these options are fairly straight forward, but feel free to ask if you are stuck or if you broke something, in these regards.

NOTE: nested items are annotated using dots e.g `portfolio.info.name.firstname`.

### 3.2 Image
Change the profile image that is displayed on the sidebar with your own picture by changing the image `assets/img/profile.jpg` with your own profile picture.

NOTE: Make sure the newly uploaded picture if in `.jpg` format and is named `profile`. (Else you need to change it in the code).

### 3.3 Social Icons
We have provided 5 social buttons for you to use, these icons can be changed in `_config.yml` by commenting or uncommenting the `portfolio.social` items.

Below an example is shown on the options that are availabe, change `your-username` with your username of the given website.

```yaml
portfolio:
  social:
    # twitter: your-username
    # facebook: your-username
    github: your-username
    linkedin: your-username
    # rss: 'your-website'
```

Note: `#` means the line is commented and won't be visible on the website.

### 3.4 About Description
If you want to change the `About` information with your own `About` information, then you can do that by going to `index.markdown` or `index.md` and replace the `Lorem Ipsum` text with your own text.

You can basically change anything below the header text:

```markdown
---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: resume
---

REMOVE ANYTHING FROM THIS POINT ON
```

Do not remove the text between `---`, as that will break the website completely.

## Step 4 - Adding Data to your website
We use data files to keep track of all the other information (experience, education, projects, ...).
These data files are located in the `_data` directory and can each be found under their own file name.

Here we make use of arrays which are indicated by the `[` and `]` at the start and end of the file.
We annotate each object in this array by `{` and `}` at the start and end of each object.
Each object has key/value items, from which we can assign any value for our supported keys.

### Step 4.1 - Add your Job Experience
Open `_data/jobs.json`.

#### Available Keys
| field name     | data type | format     | required  | description                             |
|----------------|-----------|------------|-----------|-----------------------------------------|
| function       | text      | ""         | yes       | What was your function at this company? |
| company        | text      | ""         | yes       | What company did you work at?           |
| start_date     | date      | dd-mm-yyyy | yes       | When did you start?                     |
| end_date       | date      | dd-mm-yyyy | no        | When did you finished?                  |
| description    | text      | ""         | no        | What did you do?                        |

#### Examples
Current Job without a description:
```json
  {
    "function": "Software Engineer",
    "company": "Billips",
    "start_date": "01-07-2020",
  },
```
NOTE: This example does not have a `description` and `end_date` key present.

Current Job with a description:
```json
  {
    "function": "Software Engineer",
    "company": "Billips",
    "start_date": "01-07-2020",
    "description": "Lorem ipsum"
  },
```
NOTE: this example does not have a `end_date` key present.

Previous Job with a description:
```json
  {
    "function": "Intern",
    "company": "Boogle",
    "start_date": "01-02-2020",
    "end_date": "11-11-2020",
    "description": "Lorem ipsum"
  },
```

TIP: Work with the available example data file.

### Step 4.2 - Add your Studies
Open `_data/studies.json`.

#### Available Keys
| field name     | data type | format     | required  | description                     |
|----------------|-----------|------------|-----------|---------------------------------|
| course         | text      | ""         | yes       | What course did you follow?     |
| school         | text      | ""         | yes       | What school did you attend to?  |
| degree         | text      | ""         | no        | What degree would this give?    |
| start_date     | date      | dd-mm-yyyy | yes       | When did you start this course? |
| end_date       | date      | dd-mm-yyyy | no        | When did you end this course?   |
| description    | text      | ""         | no        | What is this course about?      |

#### Examples
Current Study without description:
```json
  {
    "course": "Data Science & Artificial Intelligence",
    "school": "Maasrecht University",
    "degree": "Bachelor's Degree",
    "start_date": "01-09-2020"
  },
```
NOTE: This example does not have a `description` and `end_date` key present.

Current Study with description:
```json
  {
    "course": "Data Science & Artificial Intelligence",
    "school": "Maasrecht University",
    "degree": "Bachelor's Degree",
    "start_date": "01-09-2020",
    "description": "Lorem ipsum"
  },
```
NOTE: This example does not have an `end_date` key present.

Previous study without degree:
Current Study with description:
```json
  {
    "course": "Data Science & Artificial Intelligence",
    "school": "Maasrecht University",
    "start_date": "01-09-2020",
    "end_date": "01-04-2018",
    "description": "Lorem ipsum"
  },
```
NOTE: This example does not have a `degree` key present.

### Step 4.3 - Add volunteering work
Open `_data/volunteers.json`.

#### Available Keys

| field name     | data type | format     | required  | description               |
|----------------|-----------|------------|-----------|---------------------------|
| function       | text      | ""         | yes       | What was your function?   |
| company        | text      | ""         | yes       | Where did you volunteer?  |
| start_date     | date      | dd-mm-yyyy | yes       | When did you start?       |
| end_date       | date      | dd-mm-yyyy | no        | When did you stop?        |
| description    | text      | ""         | no        | What did you do?          |

#### Examples
Current Volunteering Work without description:
```json
  {
    "function": "Volunteer",
    "company": "Stichting LOG",
    "start_date": "01-09-2018",
  }
```
NOTE: This example does not have a `description` and `end_date` key present.

Current Volunteering Work with description:
```json
  {
    "function": "Volunteer",
    "company": "Stichting LOG",
    "start_date": "01-09-2018",
    "description": "Lorem ipsum"
  }
```
NOTE: This example does not have an `end_date` key present.

Previous Volunteering Work with description:
```json
  {
    "function": "Volunteer",
    "company": "Stichting LOG",
    "start_date": "01-09-2018",
    "end_date": "01-01-2019",
    "description": "Lorem ipsum"
  }
```

### Step 4.4 - Add your projects
Open `_data/projects.json`.

#### Available Keys
| field name          | data type | format     | required  | description                                  |
|---------------------|-----------|------------|-----------|----------------------------------------------|
| title               | text      | ""         | yes       | What was the project name?                   |
| stakeholders        | text      | ""         | no        | Who were the stakeholders/any other subtext? |
| start_date          | date      | dd-mm-yyyy | yes       | When did the project start?                  |
| end_date            | date      | dd-mm-yyyy | no        | What is the project deadline?                |
| description         | text      | ""         | no        | What is the project about?                   |

#### Examples
Current Project without description:
```json
  {
    "title": "Drawing Recognition",
    "stakeholders": "DEEPLEARNING4J",
    "link": "http://www.google.com",
    "start_date": "01-01-2021",
  },
```
NOTE: This example does not have a `description` and `end_date` key present.

Current Project with description:
```json
  {
    "title": "Drawing Recognition",
    "stakeholders": "DEEPLEARNING4J",
    "link": "http://www.google.com",
    "start_date": "01-01-2021",
    ""description": "Lorem ipsum"
  },
```
NOTE: This example does not have an `end_date` key present.

Previous Project with description:
```json
  {
    "title": "Drawing Recognition",
    "stakeholders": "DEEPLEARNING4J",
    "link": "http://www.google.com",
    "start_date": "01-01-2020",
    "end_date": "01-06-2020",
    ""description": "Lorem ipsum"
  },
```

### Step 4.5 - Add your Awards
Open `_data/awards.json`.

Just an array of strings.

#### Examples
```
[
  "This is an Award",
  "This is another award"
]
```

### Step 4.6 - Add your Skills
Open `_data/skills.json`.

Just an array of strings.

#### Examples
```
[
  "Java",
  "Microservices",
  "Blockchain",
  "Waterfall",
  "Agile / Scrum Development",
  "Spring boot Framework",
  "Laravel Framework",
  "ASP.NET",
  "VueJS",
  "ReactJS",
  "NodeJS",
  "C#",
]
```

## Step 5 - Commit Everything (if you have not yet done so)
The last thing to do is to commit all your changes (if you have not yet done this).


## Step 6 - Wait untill github actions finished deploying your website.
The only thing left for you to do is to grab something to drink and wait for Github Actions to finish his magic and deploy your website.
You can check this process by clicking the `Actions` tab on the top of your repository.

If the top task is displayed `green` then it is successfully deployed, if the top task is displayed `orange` then it's either pending or still in progress, and if the top task is displayed `red` then something went wrong.

### Step 6.2 - The deployment failed
In case the top task is displayed as `red` then we need to look into the issue. Click on the failed task and unfold the processing step where it failed (marked with a red cross), here you can see the output and possible exception stack.

#### Common errors
- You did not set your secret `JEKYLL_PAT` key yet, as described in **Step 2**.
- Syntax Error - Either your `_config.yml` or one of your `data files` has a syntax (or tabbing) issue that needs to be solved.
- Styling is not visible - This means your `url` or `basepath` is incorrect.

## Step 7 - ENJOY YOUR WEBSITE
Now go to your website and check if it is working. (See `Common Errors` in case there is a styling issue).

If you do not know you github-pages url, then go to `settings` and scroll down until you see `GitHub Pages`.
When your website has been published, you should see a green bar that displays your website url.
The text looks something like:
```
 Your site is published at https://msvincognito.github.io/static-site-workshop/
```
