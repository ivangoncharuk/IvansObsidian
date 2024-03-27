
# New Hire Dynamic Checklist

## Description

You're looking to develop a system where you input four fields: Store Location/Branch, Position, First and Last Name, and the Last 4 digits of the Social Security Number. Based on these inputs, a dynamic checklist specific to the new hire's position would be generated. This checklist should allow you to track completion of each step. Some roles may require access to certain applications while others do not. Additionally, each task in the checklist should have a link to relevant documentation, potentially hosted on a GitHub wiki alongside other call center documentation. You're considering implementing this as either a Python console script, a GUI application, a webpage, or exploring other application solutions.

## Option Summaries and Pros & Cons

### Python Console Script

**Pros**:

- Simple and quick to develop.
- Easy automation of backend logic.

**Cons**:

- No graphical user interface; less user-friendly for non-technical users.
- Limited in interactivity and user engagement.

### GUI Application

**Pros**:

- More interactive and user-friendly.
- Can include graphical elements like dropdowns, input fields, and checkboxes.

**Cons**:

- Requires more development time and effort.
- May face cross-platform compatibility issues.

### Webpage

**Pros**:

- Accessible from any device with a web browser.
- Easily links to external documentation; can integrate seamlessly with GitHub wiki.
- Facilitates sharing and collaboration among team members.

**Cons**:

- Needs web hosting (though many free options are available).
- Requires web development skills for both frontend and backend (if dynamic functionality is needed).

### Other Applications (e.g., Notion, Confluence)

**Pros**:

- Platforms like Notion and Confluence are designed for documentation and collaboration, offering rich text editing, databases, and task management.
- No need for development skills; configurations are mostly GUI-based.

**Cons**:

- Less customizable than a fully custom solution.
- May not support as detailed or specific workflow automation without integration with external tools.

### Conclusion

Needs to be dynamic, easily accessible, and user-friendly that integrates with Markdown documentation. A **webpage** seems to be the most advantageous approach. It balances accessibility, ease of use, and the ability to directly link to extensive documentation. Instead of a webpage, exploring platforms like Notion or Confluence might offer a viable alternative with less customization but faster deployment.


---

# Input Fields

## Stores:

Location/Dealership_Name - StoreNum/BranchNum
Some locations have multiple Dealership brands, i.e. Chrysler Dodge Jeep (Can be tuples)


- TCC/Accounting heritage - 01/Acct01
- Silver Spring/Accounting Herb Gordon - 02/Acct01
- Annapolis/Mercedes - 02/05
- Bel Air/Honda - 01/05
- Bel Air/Mazda - 01/06
- Catonsville/Subaru - 01/11
- Catonsville/Volkswagon - 01/11
- Catonsville/Mazda - 01/11
- Catonsville/Toyota Collision Center - 01/10
- Catonsville/Toyota - 01/09
- Catonsville/BMW - 02/09
- Fort Washington/BMW - 02/11
- Harrisburg/ChryslerDODGEJEEP - 01/22
- Harrisburg/Toyota - 01/23
- Parkville/ChryslerDodgeJeep - 01/15
- Parkville/Honda - 01/14
- Parkville/Volkswagon - 01/15
- Owings Mills/ChevyBuick - 01/01
- Owings Mills/ChryslerDodgeJeep - 01/03
- Owings Mills/Imports - 01/04
- Owings Mills/Toyota - 01/07
- Owings Mills/Mercedes Benz - 02/10
- Silver Spring/BMW - 02/08
- Silver Spring/Mercedes Benz - 02/04
- Silver Spring/Mileone Body Shop Express - 02/07
- Silver Spring/PorscheAudi - 02/06
- Silver Spring/Subaru - 02/02
- Silver Spring/Volvo - 02/01
- Towson/Hyundai - 01/17
- Towson/Mazda - 01/12
- Westminster/Honda - 01/16

## Positions

- AP Clerk
- AR Clerk
- Asst Parts Manager
- Asst Service/Lane Manager
- BDC/Special Finance
- Body Shop Estimator
- Body Shop Manager
- Body Shop Technician
- Cashier/Service Clerical/File Clerk
- Controller
- Customer Relations Manager
- Deal Admin
- Deal PRocessor
- Detail
- DX Driver
- F&I Manager
- GM
- GSM
- HR
- ISM
- Loaner Agent
- Lot Attendant
- Marketing (ANY POSITION)
- MIS Hardware Technician
- MIS Help Desk Call Center
- Office Manager
- Parts Advisor
- Parts Inventory/STK Clerk
- Parts Manager
- Payroll Admin
- Payroll Admin
- Receptionist
- Sales Associate
- Sales Inventory
- Sales Manager
- Service Advisor
- Service Dispatcher
- Service Manager
- Service Reception
- Technician
- Title Clerk
- Warranty Admin

## Name fields

- First Name
- Last Name

## SSN field

- Last 4 of social

# Checklist of tasks

## Set up AD Account
- AD Username (lowercase)
	- `firstname.lastname`
- Member of Groups
	- Get clarification on this

## Set up Email Username & Password

- Depends on Exchange and POP accounts

## Set up Reynolds Account
- ID
	- Weird convention (get clarification)
- Reynolds Group
- Branches

## Set up eLeads Account (single sign on)

- ID (still need it)
- Positions (If applicable, Varies on position)

## Boolean for Call Revu

- Yes or No
- ties to eleads (if they got eleads)

## CenPOS (is not single sign on)

- ID
- password
- Merchant ID Number
- Role

## Blue Screen Access Boolean
- Create a ticket if true

## DTX / Heat Sheets Boolean

- Create a ticket if true

## Commissions

- Not sure if there is anything that triggers this
- Ties to certain stores, some dont get it, some do get it
- some salary some commissions

