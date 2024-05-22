
## Data repository set-up

1.  **Email (probably)**
    - To get started, please
      - get an account on GitHub: https://github.com/
      - open an issue for your data, so that we can communicate on using
        GitHub: https://github.com/openwashdata/data/issues
      - think about a name for your data package. The name should:
        - have all small letters
        - have no spaces or dashes
        - be a combination of two to three words
        - identify location and/or theme/topic
      - write down description
        - One-sentence description
            - Example: Groundwater analysis from 2016 in Kwale, Kenya
        - Detailed description
            - Example: The goal of `grdwtrsmpkwale` is to provide datasets for research and planning of water and solid waste management in Kwale, Kenya. This package includes water anlaysis data collected in 2016 combined with the geospatial data from the collection points.
2.  **Open GitHub**
    1.  If data donator has not opened an issue on [openwashdata/data issue tracker](https://github.com/openwashdata/data/issues), do it yourself
    2.  Decide on a name for the repository and corresponding R data package
    3.  Create a new repository with the following settings
        - Public
        - Do **not** add a README
        - Do **not** add a .gitignore
        - Do **not** add a LICENSE
    4.  Invite the contributor as a collaborator on this repository
    5.  Inform contributor that they need to accept the invitation to
        contribute (probably by Email)
3.  **Open RStudio IDE**
    1. Install openwashdata R package - `devtools::install_github("openwashdata/washr")`
    2. Check if R Packages \[\[{devtools}\]\] and \[\[{usethis}\]\] are
        installed. Install, if they are not.
    3.  Create a new project using the R Package \[\[{devtools}\]\]
        template and the same name you used on GitHub
        - If project folder already exists, open it and use
          - `usethis::create_package(".")`
        - If project folder does not yet exist, use
          - File -\> New Project -\> New Directory -\> R Package using
            devtools -\> Choose directory name and location of
            sub-directory
    4.  Add git version control to local directory
        - In Console, execute
          - `library(usethis)`
          - `use_git()`
            - yes, commit
            - yes, restart
    5.  Connect remote repository on GitHub with local repository
        - `git remote add origin URL`
        - `git branch -M main`
        - `git push -u origin main`
   
    

## Data Cleaning
1. Add directory for raw-data to project
   - In Console, execute `washr::setup_rawdata()`
    - Add, commit and push all changes to GitHub
    - On GitHub, open issue 1 for adding data to `data-raw/` folder
      - use an issue template (example: https://github.com/openwashdata/cbssuitabilityhaiti/issues/1#issue-1657507593)
2.  **Work on `data-raw/data_processing.R` to clean raw data and export tidy data**
3.  Once data reaches tidy state, in Console, execute `washr::setup_dictionary()`
    - Fill the description in `dictionary.csv` for each dataset and variable
5. Add, commit and push all changes to GitHub
6. On GitHub, open issue 3 for cross-checking in with data donator for correct understanding of variables in `dictionary.csv`
7. Initiatie and write documentation in `\R` folder by executing in console: `washr::setup_roxygen()`
   - Open each documentation file in `\R` to write a title and description 
9. Add an additional package documentation to Package
   - `usethis::use_package_doc()`
   - If data documentation name is the same as package name, then add the following to the \*-package.R file
   - \#’ @aliases testduplicate-package
     - sources:
          - https://github.com/DavisVaughan/testduplicate/blob/7c4c6ce09b3131d966cda91c6fb6a67fa6e0bbb5/R/testduplicate-package.R#L2
          - https://github.com/tidymodels/hardhat/issues/130#issuecomment-622438758
      - Resource
          - https://roxygen2.r-lib.org/articles/rd-other.html#datasets
10. Add, commit and push all changes to GitHub
    
## Complete package needed files
### DESCRIPTION
1. On GitHub, set up issue 4 with details to write up author information for `DESCRIPTION` file
   - Contributors (name, email, role, ORCID)
     - Include everyone here
       - Roles
         - cre = maintainer
         - aut = significant contributions
         - ctb = contributor with smaller contributions
    - Resource
      - https://r-pkgs.org/description.html
    - Add author(s): `use_author(given = "Lars", family = "Schöbitz", role = c("aut", "cre"), email = "lschoebitz(at)ethz.ch", comment = c(ORCID = "0000-0003-2196-5015"))`
2. Add dependencies (not optional if vignettes are used)
   - `use_package("dplyr")`
   - `use_package("ggplot2", "Suggests")`
4. Complete `DESCRIPTION` file by executing in Console: `washr::update_description()`
6. Use `devtools` to load, document, check, and install
   - Use keyboard shortcuts
      - `devtools::load_all()` “Cmd + Shift + L”
      - `devtools::document()` “Cmd + Shift + D”
      - `devtools::check()` “Cmd + Shift + E”
      - `devtools::install()` “Cmd + Shift + B”
   
### README

1. Create a rmd README for package, in console, execute `washr::setup_readme()`.
   - Enable `has_example=TRUE` to create an example article for the package.
3. Add, commit and push all changes to GitHub - On GitHub, open issue 5 to define who writes up which parts of the README
5. Add formal dependencies from Vignette (not necessary for article vignette?)
   - Any package used in a vignette must be a formal dependency, i.e. it must be listed in Imports or Suggests in DESCRIPTION
   - https://r-pkgs.org/vignettes.html#sec-vignettes-eval-option

### Pkgdown Website
1. Create new branch - `pkgdown`
2. In console, run `washr::setup_website()` to create an openwashdata style pkgdown website
3. Use `devtools` to load, document, check, and install
   - Use keyboard shortcuts
        - `devtools::load_all()` “Cmd + Shift + L”
        - `devtools::document()` “Cmd + Shift + D”
        - `devtools::check()` “Cmd + Shift + E”
        - `devtools::install()` “Cmd + Shift + B”
4. Add, commit and push all changes to GitHub
          
## Package Release
1. Add automated CMD BUILD check
    - `usethis::use_github_action_check_standard()?`
    - checks build for Mac, Windows, Linux
1.  **Open Zenodo**
    - login with GitHub account
    - click on dropdown next to email address in top right
      - select GitHub
      - find the repository in the list
      - and flip switch to “ON”
      - click on repo link
    - create release v0.0.1 on GitHub
      - initial package release
    - Go back to [the Zenodo GitHub overview page](https://zenodo.org/account/settings/github/)
      - Get the DOI Badge
    - Open the entry on Zenodo
      - Click on Edit
      - Remove text under Additional Notes and replace with GitHub pages
        link, e.g.
        - Visit the website of this dataset for instructions how to use
          it: https://openwashdata.github.io/fsmglobal/
      - Change upload type
        - Change from Software to Dataset
      - Open related identifiers
        - Remove current entry for release link
        - Add new entry, e.g.
          - https://openwashdata.github.io/fsmglobal/
          - is compiled/created by this upload
          - Dataset
      - Get the DOI
2. Add `CITATION.cff` by executing `washr::update_citation()`
3.  **Open RStudio IDE**
    - Add DOI badge to repository README.md
    - Edit DESCRIPTION
      - edit version number
    - Write CITATION.cff and inst/CITATION with DOI entry using \#gist
      or respective \[\[{openwashdata}\]\] R Package
      - https://gist.github.com/larnsce/dccdb26762837618c6dda82a5614b584
    - `pkgdown::build_site()`
6.  **Open ETH Research Collection (not for openwashdata, but GHE
    workflow)**
    - research data -\> dataset
    - organisational unit
      - tilley
    - license
      - creative commons attribution 4.0 International
7.  **Common items to be fixed**
    - R CMD CHECK
      - Notes
        - unable to verify current time
          - Fix: https://stackoverflow.com/a/63837547/6816220
        - Non-standard files/directories found at top level:
          - Fix:
            https://stackoverflow.com/questions/48955103/non-standard-file-directory-found-at-top-level-readme-rmd-persists-even-after
## After-Release

   - Update the openwashdata google sheet spreadsheet on the data entry
   - Update the openwashdata website by syncing the sheet
   - Create an issue in newsletter repository or similarly to prepare announcement for the next issue
   - Refine the github repository profile page
     - Add description
     - Add keywords
   - Share with the data donators 
   - Examine and close any remain issues
   - (Optional) Transfer maintainer role when the developer can no longer maintain the package

## Resources
### readme
 - https://r-pkgs.org/vignettes.html#sec-vignettes-workflow-writing
      - Prepare one or two data visualisation or table examples
### pkgdown
Edit Home Index
   - use this as template: https://github.com/Global-Health-Engineering/durbanplasticwaste/blob/main/\_pkgdown.yml
   - consider writing pkgdown template for this:https://github.com/openwashdata/book/issues/16
     - https://github.com/tidyverse/tidytemplate
     - https://pkgdown.r-lib.org/articles/pkgdown.html#home-page
     - explore: https://pkgdown.r-lib.org/articles/customise.html
