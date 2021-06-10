# Zowe Doc site generator and UI

![zowe-template-omp-project](https://user-images.githubusercontent.com/53327173/121530862-7e7d4a00-ca1b-11eb-80ee-9360e2d73177.png)

## Project Description
The [Zowe doc site](http://docs.zowe.org/) is built using Vuepress. With the content for the site growing in size and complexity, users need better user experience. Complete project description/requirements of the project could be found [here](https://github.com/zowe/docs-site/issues/1587).

### Why a new site generator is being considered

- Vuepress now has a limitation for the nav depth. It does not support nested sidebar thus some sections cannot be further organized. 
- We want to improve the current Vuepress site layout to be a standard three column layout supporting better navigation experience. 
- Many other functions are wanted but not available on the site now. For example, social functions like Share, Feedback, and more importantly the ability to generate a PDF file automatically. 
- Considering the growth of the community, multilingual support will be wanted for Zowe docs in the near future. 

| Folder | Description |
|---|---|
| Documentation |  Detailed description and design/architectural requirements of the project |
| Notes and Research | Relavent information useful to understand the tools and techniques used in the project |
| Status Reports | Project management documentation - weekly reports, milestones, etc. |
| src | Source code of the new prototyped website built using ReactJS based site generator |


## Project Team
- *[Ashley Li](https://github.com/nannanli)*  - *IBM* - Mentor
- *[Pluto Zhang](https://github.com/PlutoZhang/)* - *IBM* - Mentor
- *[Arijit Kundu](https://github.com/covalentbond)* - *University* - Mentee
