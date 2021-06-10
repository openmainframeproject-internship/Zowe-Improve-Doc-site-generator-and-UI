# Documentation Folder

The Zowe doc site is built using Vuepress. With the content for the site growing in size and complexity, users need better user experience. 

- [Statement of work](#statement-of-work)
- [Detailed design requirements](#detailed-design-requirements)
- [Installation guide](#installation-guide)

## Statement of work

- Vuepress now has a limitation for the nav depth. It does not support nested sidebar thus some sections cannot be further organized. 
- We want to improve the current Vuepress site layout to be a standard three column layout supporting better navigation experience. 
- Many other functions are wanted but not available on the site now. For example, social functions like Share, Feedback, and more importantly the ability to generate a PDF file automatically. 
- Considering the growth of the community, multilingual support will be wanted for Zowe docs in the near future. 

### Related issues

Some existing issues might be able to be addressed in the process. 

- [#1376](https://github.com/zowe/docs-site/issues/1376) Add 'share to social media' buttons on Zowe doc site 
- [#1259](https://github.com/zowe/docs-site/issues/1259) Doc Enhancement: Track and alert on last-updated topics 
- [#730](https://github.com/zowe/docs-site/issues/730) Enhancement - Add Slack button, other UI improvements
- [#558](https://github.com/zowe/docs-site/issues/558) Inconsistent Bold Headings in TOC
- [#533](https://github.com/zowe/docs-site/issues/553) Enhancement - Dark Theme option
- [#286](https://github.com/zowe/docs-site/issues/286) Allow Users to adjust the size of the TOC frame in the browser
- [#653](https://github.com/zowe/docs-site/issues/653) Add Home Button/Icon to the Toolbar/nav menus
- [#1672](https://github.com/zowe/docs-site/issues/1672) Large Images are small in size and not properly readable
- [#532](https://github.com/zowe/docs-site/issues/1672) Improve home page design (Home page can be customized accordingly as Docusaurus is buit on top of React
- [#538](https://github.com/zowe/docs-site/issues/1672) Enhance doc site UX
- [#1374](https://github.com/zowe/docs-site/issues/1672) Enhance Zowe doc SEO (Comes with official plugin to generate sitemaps)
- With Vuepress Limitation, all the publishing version URLs could not include `(.)` Like `v1.15.x`, this would resolve the issue stated [here](https://github.com/zowe/docs-site/blob/2b145a4126c4c0ec3f01f09c9bfa93a3bea567df/docs/.vuepress/config.js#L4)


## Detailed design requirements

- [x] More depth to sidebars (must support nested topics)
- [x] Three column layout (nav-topic-mini toc) 
- [x] Collapsible sidebar (can be changed into two column layout as per need)
- [x] Two themes (dark and light)
- [x] Algolia Search (AI-powered Search) 
- [x] Create a zoom-in effect for Doc Images 
- [x] Social module
   - [x] A "Share" button that allows users to share a topic to social platforms
   - [x] A "Discussion" button that opens Zowe Slack channels. It's in the footer section now as a resource. 
- [x] Feedback module
   - [x] Rate "Is this topic helpful" - thumbs up and thumbs down. Helpful or not helpful. When not helpful, ask users to create a Github issue. 
   - [x] "Open doc issue" for each topic that directs users to the doc site repo. 
      - [x] Better to associate the topic URL and some background information in the issue automatically.  
   - [x] "Edit this topic" link that directs users to the source file for each topic
- [x] Can print PDF (download the complete doc into PDF, not print a single topic) 
- [x] Support localization (also document how to do that for future reference)  
- [x] Support multi version of docs 
- [x] Support a home page
- [x] Google Analytics embedded - Ashley to share the account information 
- [x] Similar look and feel with zowe.org (includes footer) 
- [x] Supports Markdown syntax
- [x] Cannot change the doc URLs (to avoid broken links) 
- [x] Images are loading when you refresh the site, need to fix it.
- [x] Algolia: need to re-index the whole site and need support from Algolia team.
- [x] Optional: Support reading docs offline
- [x] Optional: Includes a "Estimated reading time: xx minutes " for each topic. 


## Installation guide

- Clone the specific branch: `git clone --branch zowe-docs-v2 https://github.com/zowe/docs-site.git`
- Install dependencies: `npm install`
- Start the server: `npm start`. Website is ready to be previewed at `localhost:3000` 🚀!