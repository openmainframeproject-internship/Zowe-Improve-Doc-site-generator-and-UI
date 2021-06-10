# Source Code Folder
To be structured as needed by project team.

```
docs-site
├── sidebars.json                        # Sidebar for current version
├── docs                                 # Contains the Markdown files for the docs. 
│   ├── getting-started 
│   │   └── overview.md                  # https://docs.zowe.org/stable/getting-started/overview
│   └── hello.md                         # https://mysite.com/stable/hello
├── src                                  # Non-documentation files like pages or custom React components. 
│   ├── pages/                           # Any files within this directory will be converted into a website page.
│   │   └── index.js                     # Home page
│   └── theme/                           # Swizzled Docusaurus theme components
├── static                               # Static directory.
├── versions.json                        # File to indicate what archived versions are available
├── versioned_docs                       # Each directory in versioned_docs/ represents a documentation version.
│   ├── version-v.21.x
│   │   ├── getting-started
│   │   │   └── overview.md              # https://docs.zowe.org/v1.21.x/getting-started/overview
│   │   └── hello.md
│   └── version-v1.20.x
│       ├── getting-started
│       │   └── overview.md              # https://docs.zowe.org/v1.20.x/getting-started/overview
│       └── hello.md
├── versioned_sidebars                   # Each file represents sidebar for particular archived versions
│   ├── version-v.21.x-sidebars.json
│   └── version-v1.20.x-sidebars.json
├── docusaurus.config.js                 # Config file containing the site configuration.
├── sidebar.js                           # Specify the order of documents in the sidebar. If you have a new file to add to the site, modify this 
└── package.json
```