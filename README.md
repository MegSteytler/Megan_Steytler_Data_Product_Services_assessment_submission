
**Submission: Megan Steytler 20/10/2025**

**City of Cape Town \- Data Science Unit Code Challenge**

# Technical Assessment: Head of Data Product Services

## 1. Product Vision & User Definition

**Product Vision Statement**

*City Pulse \- giving residents a voice, and the city the data and insights, to act now and plan for the future.*

**Three key users and their personas**

1. **Residents:** Alex is a resident of Sea point. She’s noticed a missing manhole cover outside her apartment that’s left a hazardous hole exposed for over a week. She would like to quickly report the issue to the city, ideally using her phone, without much fuss and admin.  
2. **Ward councillors:** Tshepo is a ward councillor under pressure from residents in his area who are complaining about uncollected garbage. He’d like to quickly see a service delivery report for his ward and wider sub-council area.  
3. **Senior city management:** David is a senior city manager involved in budget allocations for infrastructure projects. He’s looking for a comparative view of service delivery incidents by ward to support his decision making.

**Selected User: Senior city management**

**Primary goal**

* To make informed, data-driven budget allocation decisions that align resources with the city’s infrastructure needs.

**Pain points**

* There isn’t a unified view for all departments. He has to source data from each department and manually consolidate for a comparative view.  
* It’s not clear to him if each department has cleaned, transformed, filtered or structured the data in the same way.  
* There is no single point of contact/stewardship for concerns regarding quality and integrity of the data.

---

## 2. Strategy & Success Metrics

**The core product strategy:**

1. A user-friendly, conversational type channel for residents to quickly report service issues, with feedback on progress and resolution status.  
2. A consolidated and unified view of incident data, enabling evidence based decisions around resource allocations.  
3. An analytics capability to preempt maintenance and reduce future incident reporting.

**How will City Pulse succeed where others have failed and what is its unique value proposition?**

* **Accessibility** \- the ubiquity and large user base of WhatsApp is a critical advantage  
* **Usability** \- the conversational flow of the bot guides the user step by step through the process, reducing the friction of rigid input requirements  
* **Centralisation** \- a consolidated data management function enables standardisation, which supports solution scalability  
* **A data governance led approach** \- a strong emphasis on data governance increases the quality and integrity of the data, which instills trust and improves adoption rates

**Critical objective:** reduce user friction in incident reporting

**Measurable results:**

1. % reduction in the number of service requests abandoned  
2. Reduction in the average time it takes users to complete and submit a service request  
3. Increased participation \- sustained increase in the number of residents submitting service requests (assuming the increase is not related to an increase in service delivery issues, hence the longer term measurement)

---

## 3. The User Journey & MVP

**WhatsApp User Journey:**

<img width="1748" height="2288" alt="image" src="https://github.com/user-attachments/assets/f0cd8e10-414d-4e30-97d6-5f7c6994b4ce" />

The bot will use a conversational flow to understand intent from free text input and then ask the user for structured data inputs via selection. For example if the user at any point types “I’ve made a mistake” or “I want to make a change” then the user is presented with the steps completed up to this point and asked to select the step they would like to edit. E.g. 1\. Description, 2\. Category etc. Alternatively the user could type ‘I gave the wrong address’, and the bot would revert to the address step by asking for the address again.

Depending on the granularity of status tracking by the departments, the user would receive an update triggered by an incident status change. For example if a technician has been dispatched, or if a technician is on site. Depending on user research, receiving a periodic update regardless of status change may be preferable to no communication at all. These could be linked to departmental SLAs (service level agreements). E.g. If there is no status change after X hours, the user receives an update: "We apologise for the delay, your service request is being processed and a technician will be assigned shortly".

**Essential features for MVP:**

1. **A bot with natural language understanding (NLU):** This is core to the product to support unstructured messaging and a conversational flow. The effort is higher to set up training data for an NLU engine (versus using just keywords) but long term it offers scalability and lower maintenance.  
2. **Integration with departmental ticketing systems** (plural?). This is high effort if there are multiple ticketing systems (i.e. per department). Ideally a single single, standardised ticketing system with workflows to relevant departments for action is required.  
3. **"Smart Categorisation" using contextual understanding:** the bot dynamically filters and presents a relevant list of service categories based on contextual understanding (NLU again trained on categorization data) of the user’s initial input.
4. **Address input and verification:** the user submits the location via free text. A geocoding API is used to verify the address or suggest possible matches for selection.  
5. **Media support:** handling and storage of photos and documents. Core to providing as much information to resolve the issue.  
6. **Realtime status updates:** depending on the tracking/status granularity of the city’s ticketing system, real-time updates triggered by each status change are communicated to the user. Lower in value as it’s an auxiliary feature but important for establishing trust and better communication.  
7. **Edit or cancel existing service requests:** would prevent multiple incidents being submitted by the same user or a timeous cancellation before a technician is dispatched. Higher effort as there is consideration for overwriting versus keeping an audit log of changes and triggering alerts for operators to be notified of changes.

**Value vs. Effort matrix**

<img width="940" height="758" alt="image" src="https://github.com/user-attachments/assets/7a7aa055-049b-4e6b-aa5b-d4763d0d8719" />

The value versus effort matrix is helpful in prioritizing for:

* **Sequencing:** since they are all essential for an MVP, it’s a matter of when/how to sequence the build based on resource availability and effort. Where resources are limited, high value, low effort quick win features should be prioritized.  
* **De-risking large, core features:** high value \- high effort features core to product strategy should not be left until the end. These should be prioritized first to de-risk and allow enough time to get over the line. Lower effort and lower value features can be left for later on.

---

## 4. Data & Technical Considerations

**Key data sources City Pulse must integrate with:**

* GIS: Address geocoding after verification to integrate with GIS  
* Departmental ticketing systems  
* Legacy service request systems (call centre, web portal) and new WhatsApp system  
* City Master Data e.g. departmental categories (Levels 1, 2 and 3), ward boundaries, SLAs per department  
* Media attachment data  
* NLU training data  
* The City’s Identity/access management

**Advanced analytical use case for City Pulse**

The senior city manager involved in budget allocations for infrastructure projects could benefit from a view of forecasts of service delivery incidents based on historical data trends, to preempt future maintenance costs by investing now in long term infrastructure development.  A view, by critical department category and area, could highlight future maintenance hotspots  e.g. forecasted water leaks and the tipping point at which accumulating maintenance costs overtake once-off infrastructure expenditure.

**Risks & Mitigation: Two major data or technical risks and mitigation**

1. **NLU (natural language understanding) limitations** \- language ambiguity and failure due to edge cases.

Risk mitigation \- the interaction is designed to be conversational with NLU used to infer intent, but structured data will be requested for input or selection (e.g. select option 1, 2 or 3). This will limit misinterpretation. The risk of edge cases will be mitigated by running the system against good and bad/ambiguous test cases. Actual transcripts from the call centre (if available) could be used as a good context-specific source of training data (country/city specific context e.g. South African slang). The model will continuously be retrained based on feedback loops.

2. **WhatsApp security of sensitive data/adherence to POPIA**

The solution needs to align to the City’s privacy policy. Besides their personal information and location data, residents in some cases may submit sensitive data e.g incident requests relating to safety and security, substance abuse, reporting of incidents that put them at risk of retaliation etc.

Risk mitigation \-  a full review of WhatsApp specific security risks needs to be conducted, as well as the risks associated along the entire data pipeline of the solution, from creation, transit, storage and sharing of the data. A risk specific to this solution is that information is submitted as free-form, unstructured data, and so it is not as easily and automatically tagged as Personally Identifiable Information for example, as is done with structured inputs on the web portal. Special consideration for appropriately tagging data is needed in this context.

---

## 5. Implementation & Governance Plan

**Metadata management and documentation practices**

A single repository of metadata would be set up so that the structure, organisation, and rules around tagging and definitions of this metadata are standardised across all departments. This creates a common understanding for all stakeholders (from a business and technical perspective), making it easier to discover and set up policies regarding accessibility, security and quality standards. Ownership will be clearly defined, with data stewards maintaining and monitoring metadata from an operational perspective, and data owners (leaders of their domain, such as the Head of Water and Sanitation or Head of Customer Relations) accountable for the quality and compliance of the data needed to serve their domain.

Up to date versioned documentation will be maintained for each data product, detailing the agreed schemas, rules, usage conditions, performance and quality metrics, so that it’s clear to any stakeholder how each data product can and should be used.

**Governance frameworks or standards**

A metadata standard would be used to ensure standardisation in line with industry best practice. Given that the City of Cape Town offers public access to approved datasets, DCAT would be an appropriate standard to use.

**Quality assurance and validation processes**

Key quality metrics such as accuracy, consistency, timeliness and completeness would be established, and data stewards would be tasked with monitoring and reporting on these metrics. Quality thresholds would be agreed with data owners.

The validation of data would be automated where possible, as per agreed rules, and audits conducted periodically to spot check where automation does not cover. Analytics dashboards would be used to monitor and take action through continuous improvement when quality thresholds are hit.

**Cross-departmental data ownership and accountability**

Data products are to be owned by data product owners, who represent stakeholder needs and the value creation of the product for the City. Where a single data product serves multiple departments, the data product owner will need to balance conflicting requirements from domain leaders, and gain consensus on data product design and future enhancements. They will work with data stewards in operationalising the data quality standards specified by the domain leaders. The nature of the ownership and accountability is documented in the product’s data catalog.

**Proposed phased implementation of City Pulse Solution**

<img width="2272" height="1760" alt="image" src="https://github.com/user-attachments/assets/0e2455eb-102a-40d7-b6be-41ca21ae08ec" />

To ensure business continuity, and given that there is limited integration capacity and uneven data quality across departments, phase 1 would entail maintaining the existing departmental data siloes while delivering the WhatsApp solution:

<img width="1571" height="785" alt="image" src="https://github.com/user-attachments/assets/eb88ce34-4437-4174-a220-e223056049ed" />

The departmental data management practices and reports remain while the incident data from the web portal and call centre is replaced or supplemented with the WhatsApp incident data (the call centre channel should remain in place for those residents wishing to speak to a human operator, but there is a case for sunsetting the web portal once the WhatsApp channel is fully deployed)

An agile methodology would be used to deploy the WhatsApp solution iteratively in cycles, delivering and piloting an MVP before enhanced features are added. The existing incident reporting channels would remain in place until the WhatsApp product has successfully been live for an agreed period of time with performance monitoring.

The final phase towards the fully fledged City Pulse solution would involve iteratively absorbing individual departmental data management into a unified data management function, with a single data governance framework applied. It’s critical that this is also done iteratively with minimal operational disruptions. This could be implemented one department at a time, with the migration running in parallel to the existing function until City Pulse data products meet the requirements for existing departmental reports/analytics views.

<img width="1284" height="757" alt="image" src="https://github.com/user-attachments/assets/c99f3046-db47-46bf-906d-4a0485e632ea" />

**Governance Workflow**

Each data product created should adhere to a governance workflow so that the new governance framework is actively applied for each product’s life cycle. This workflow would include:

1. **Ideation and planning**  
   * Business value is defined by the data product owner  
   * A data contract is drawn up defining the measurable targets for performance, reliability and quality
   * Approval attained by a central governance committee before committing resources to the build  
2. **Development**  
   * Pipeline build
   * Quality checks are automated  
   * Metadata collection is automated  
3. **Publication and discovery**  
   * The data product is added to the data catalogue with its documentation  
   * An access policy is defined and activated  
4. **Monitoring and enhancements**  
   * Service level objectives (SLOs) are monitored  
   * User feedback is considered for enhancements  
   * Data products are periodically reviewed to ensure standards are still met  
5. **Retirement**

---

## 6. Reflection on AI Use

AI was used in the following ways:

* As a tool for research \- to summarise information on a topic/sub-topic and surface the source material for deeper investigation and validation.  
* For spitballing ideas, as if brainstorming with a colleague, by conversationally discussing and refining my ideas, filling in gaps and triggering further avenues of exploration and research.  
* For simplifying verbose sentences and fixing grammatical errors as a final sweep.

The limitation of AI is the lack of creativity, in that responses often have a generic feel to them. This is why it’s useful as a tool but not as a means to generate the final solution. Responses can be flawed and lack context. This is why a human led approach to iteratively refining an answer is needed versus dense and lazy prompting for the final answer.

