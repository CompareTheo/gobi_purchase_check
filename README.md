# GobiChecker

GobiChecker is a program that takes a brief export of Gobi requests and searches Alma for duplicate holdings in the institution zone (IZ).

The scripts in this project are the original work of [Jeremy Hobbs](https://github.com/MrJeremyHobbs). More details about the updates to the code found in this repository and statements about coding credit can be found in the acknowledgements section below. 

## Description
GobiChecker is a program that takes a brief data export from Gobi and searches Alma for duplicate holdings in the institution zone (IZ). This program uses the Search/Retrieve via URL (SRU) protocol to query Alma using the alma.isbn (ISBN query), alma.title (Title query), and alma.all_for_ui (Keyword query) indexes. 

## Getting Started

### Dependencies

* Alma requires the setup of an SRU integration profile. More information about setting up an SRU integration profile can be found in the [Ex Libris Developer Blogs](https://developers.exlibrisgroup.com/blog/how-to-configure-sru-and-structure-sru-retrieval-queries/)
* Scripts require the creation of a "config.ini" file consisting of version numbering, download directory, Alma institution code, Alma institution zone path, and log directory. For a more complete example of the appropriate structure and format, see [Jeremy Hobbs' GobiChecker Repository](https://github.com/MrJeremyHobbs/GobiChecker).

## License

This project is licensed under the MIT License - see the LICENSE.md file for details

## Acknowledgments

The inception and a substantial portion of the codebase for this project originated from the creative mind and diligent efforts of [Jeremy Hobbs](https://github.com/MrJeremyHobbs). The fundamental ideas and structures were crafted by Jeremy, forming the foundation upon which this forked repository is built.

The current state of the code represents a 10% net increase in modifications from Jeremy's original work. All alterations and enhancements made are documented in the section below.

I wish to publicly express my gratitude to Jeremy for his invaluable contributions to this project. His openness in sharing his original code under such permissive licensing are the foundation of the improvements and customizations introduced in this fork. He has my deepest thanks and professional admiration.

## Change Log

The original GobiChecker project notes in its documentation that "currently GobiChecker is only for institutions with both an IZ and NZ." What has not been noted in detail in this change log is the work completed to establish compatibility for institutions with only an IZ. However, all other substantive changes are noted below.

**gobi/__init__.py**

Two additional parsing sections have been added:

1. The first simply defines a variable for "selector," a GOBISMART custom field label that we require from selector/liaisons and output into the PO-Line.

2. The second defines a variable for "intentional duplicate" which is an additional GOBISMART custom field label that is notated by the Ordering Assistant to clarify to Gobi our desire to duplicate a previously purchased title.

**alma/sru.py**

* A new import module was imported which references an "elookup.py" file. This file is a list of Alma Electronic Collection IDs which correspond to collections of non-owned, temporary, or subscribed electronic portfolios.

* A new class has been created called "CollectionCheck" which instantiates the necessary variables and functions needed to check the SRU's returned Electronic Collection ID (code_c) against the list of Electronic Collection IDs in elookup.py.

* Roughly 10 lines relating to a check of e-holdings in the network zone were removed as we do not participate in an Alma consortium. 

* An additional function was added to parse the SRU response, check for availability of electronic access, where an e-holding is found call the CollectionCheck function on the Electronic Collection ID (code_c), and where a match is found return a temporary holding statement with the Electronic Collection Public Name (code_m).

**GobiChecker.py**

* A function for defining relative resource paths was added to ensure file path compatibility once the program was compiled for distribution. Details about that code snipit can be found on the [auto-py-to-exe common issues blog](https://nitratine.net/blog/post/issues-when-using-auto-py-to-exe/).

* Several line references to the network zone, its needed queries, and parsed responses were removed.

* Additional parsing logic was added to check for the existence of an "intentional duplicate" label in the gobi-ordering duplicate note field.

* Parsing logic was also added to identify where the Electronic Collection ID, found in the SRU e-holding parse statement, matched against the list of temporary Electronic Collection IDs stored in the elookup.py document.

* Several output tags and results were updated to align the existing result outputs with our library's needs.

* Publisher and network zone match columns were removed as they are not needed in our workflow.

* Several column result returns were reformatted to ensure the use of "title" case upon runtime.

* The header logo was changed to better match the aesthetic of the university's other software packages.

* The min and max window sizes were also changed to accommodate additional space for "results" where multiple temporary collections were found and to accommodate the addition of a "selector" column.

* Highlight colors were modified to match the software's new aesthetic.

* Additional logic and menu items were added to allow for the "right-click" copy of the selected title and the selected ISBN.