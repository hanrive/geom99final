# Problem Statement:
Currently, a fictitious Local Government in Ontario **creates** and prints paper maps of the surveyed boundaries for Real Estate Agents in support of properties for sale**. These maps cost real estate agents **$60 per request** and most just shared as **custom-created PDFs from a desktop GIS**. The Real Estate Agents are requesting the Local Government information be easier to **access though a website and (ideally) would cost less per request**. They would prefer a **single-fee per year for all requests**, versus paying per requests as well. Currently there are about 200 paid map requests per year, or about **$12,000 in fees collected per year for the roughly 50 real-estate agents in the city**.
You (as a newly-graduated GIS professional) are to propose a new web-GIS solution that would not cost more than the revenue generated per year over 3 years to run and maintain, meeting the needs identified (sharing parcel property maps).  Do not include labour in costs creating the solution. This is only a rough proposal so do not detail implementation steps. However you must be technically specific and your description must align with how the proposed technology works and how it was taught in the class.
Answer the questions about your solution which meet these above needs given the following criteria and resources identified:
-	Currently some individuals in the local government use QGIS as GIS desktop software but are no experts. They are open to switch to commercial software if they can have it funded by this solution.
-	The local government has **no server infrastructure and no capacity to host web sites or servers**. Their IT department is minimal and only supports windows desktop machines.
-	The real estate agents need to see **parcel ownership boundaries (4,000 parcels polygon records) over some type of aerial image**.
-	The parcels data from the province are **available as a GeoPackage download or as an ArcGIS Server Map Service**, your choice. The solution must be **updated at least each week with a fresh parcel layer** (if necessary). 
-	The city also has data for roads (2,200-line segments), parks (23 polygons), address points (5,500 points), which are updated a no more than **6 times per year and would be ideal to show those on the map** as well.
-	If there are any ongoing (monthly/yearly) costs for the proposed solution, Real Estate Agents will need to pay a fee for access to the proposed system. This can recover ongoing monthly costs incurred by the local government. If any monthly costs exists there must be a way to create accounts (security) for each agent to log in on the system to manage access. An estimate of costs is fine, exact figures are not necessary.
Research a solution meeting these requirements before the exam and create some notes to answer questions on how your proposed solution will work, its limitations, costs and technical overview. Point form will be fine for answers of questions provided during the exam and you will have access to your notes, the internet and any other resources during this portion of the exam.

## Real Estate Agent - company formats?
According to: https://www.reco.on.ca/agents-and-brokerages/becoming-a-real-estate-agent
All registered Real Estate Agents must be employed by a real estate brokerage (companies licensed to assist consumers in buying, selling, or leasing real estate). We could request the company’s branches to pay a yearly fee to allow access to the data.

If the city is highly populated an option for monetization could be what Realtor.ca does. https://airrealty.ca/5-websites-property-listed-mls/#:~:text=Realtor.ca&text=It%20is%20owned%20and%20operated,and%20rental%20properties%20across%20Canada states that Realtor.ca is owned and operated by the Canadian Real Estate Association (CREA) which agents pay to upkeep through their CREA dues. It might be possible to reach out and see if there is a similar monetization method through dues?

## Pricing
https://www.esri.ca/en-ca/store/products/buy/arcgis-developer-subscription would need ArcGIS Developer subscription, Professional Plan which is $3,340/yr
Over a 3-year period that would add up to $10,020 which is 16.5% decrease from a single yearly cost, and a 72.2% decrease from a three-year cost ($36,000). This comes out to about $66 per real estate agent in the city (50).
This plan includes access to ArcGIS Online, ArcGIS Pro, ArcGIS Enterprise (https://doc.arcgis.com/en/experience-builder/latest/get-started/faq.htm#:~:text=ArcGIS%20Experience%20Builder%20is%20included,deploy%20them%20to%20web%20servers and ArcGIS Experience Builder is included in ArcGIS Online and Enterprise)

https://aws.amazon.com/lightsail/pricing/
Host the data on AWS Lightsail. Spoke with a representative for pricing and it was recommended that I use cp3.8xlarge ($0.768/hr) - 8 vCPUs, 8GB RAM or r6g.4xlarge ($1.024/hr) - 16 vCPUs, 16GB RAM. The costs associated with this include 
-	Monthly cost = $0.768/hour * 24 hours/day * 30 days = $553.92
-	Monthly cost = $1.024/hour * 24 hours/day * 30 days = $738.56
Along with SSD Storage such as 100gb for $10 a month ($0.10 per GB-month)

Say if we go with cp3.8xlarge ($0.768/hr) - 8 vCPUs, 8GB RAM along with the SSD storage (~$570/month) that would add up to $6840 a year + $3340/year for the license plan = $10,180 a year and $30,540 for three years. That is a 15% discount with $1,820 saved per year and $5,460 saved over the course of three years. 
“The parcels data from the province are available as a GeoPackage download or as an ArcGIS Server Map Service, your choice. The solution must be updated at least each week with a fresh parcel layer (if necessary).” 
“The city also has data for roads (2,200-line segments), parks (23 polygons), address points (5,500 points), which are updated a no more than 6 times per year and would be ideal to show those on the map as well.”
Store the parcel data within an ArcGIS Server (as an ArcGIS Server Map Service) along with the city data. Upload the data to AGOL through the server link and host the data within different layers in a web map. We would upload that web map to Experience builder where the user would have to log in with their company’s log-in info (restrict access to only a few allowed users) and see the data like this: https://experience.arcgis.com/experience/d7c4882bc98d410cb216fda8927dd6a0/
Data would be stored as a hosted feature layer through the server.

## Individual Log-ins
https://doc.arcgis.com/en/arcgis-online/administer/saml-logins.htm
Would create organization-specific logins (such as SAML logins). This allows the setting up of organization-specific logins where the user wouldn’t have to create additional logins within the ArcGIS Online system.

## Limitations
Some limitations to this solution:
-	The ArcGIS Developer subscription, Professional Plan incurs ongoing costs
-	Configuring and managing ArcGIS Enterprise servers if very technical, would require additional training for their IT  departments
o	The plan does include community support and technical support
-	The cost of having cloud servers, instead of personal servers (takes up space, upfront costs, high IT experience to maintain them)
-	Hard/expensive to scale if data volumes increase or number of users needed
