# GenAI Bootcamp Solution Architecture 


### Functional Requirements

The company needs to invest in owning the infrastructure either as local or cloud-based.

The only non-negotiable requirement is that data must be completely owned by the company, as well as being auditable, compliant and governed. 

The user base could range anywhere from 1 up to 500 users at any time, which pushes us to a cloud-based scalable service. 

Since the company already owns and develops other services through AWS in their own VPC, we will use AWS.


### Technical Considerations
Let’s assume we are following the three levels of diagramming:
#### Conceptual — a high level diagram that is used to communicate to key stakeholders the business solution we are implementing
#### Logical — a mid level diagram that describes the key technical components but not requiring detailed parameters so we can quickly rearchitect and communicate to our technical team the current workload
#### Physical — a low level diagram that details all possible parameters and connections used by engineers/developers to accurately implement a solution (e.g. ARNs for resources, IP addresses, etc)


### Architectural/Design Considerations
#### Requirements, Risks, Assumptions, & Constraints:

#### Categories:
#### Business Requirements: 
Business goals and objectives
The app must be able to aid people in learning a new language. Initially it will be only japanese but should expand iteratively towards other languages.
- Learn through different activities
- Allow interaction either direct or indirect between students and teachers
- Have forum-like spaces for the students to learn together

#### Functional Requirements: 
Specific capabilities the system must have
- Use AI tools to optimize learning
- All data must be controlled and auditable
- All interactions must be auditable 
- UX oriented intercace

#### Non-functional Requirements: 
Performance, scalability, security & useability
- The app must have at most 10s response times
- The app must be as efficient as possible in resource utilization
- The app must scale to whatever user load required within the established range

#### Risks
Identified risks & how we'll mitigate them
- LLM Hallucination: RAG 
- LLM Bias: Guardrails
- User misuse of the LLM: Guardrails, golden rules and best practices of AI infographic/training

#### Tooling: 
GenAI vs ML

We will use GenAI to aid in the generation of the material and interaction with the students. ML may be used for different activities but is currently out of scope.

### Data Strategy
Develop a comprehensive data strategy that addresses:

##### Data collection and preparation
All input and output data (either user or LLM generated) has to be traced. This will be implemented through cloudwatch.

All the data that will be used within our app for the knowledge database must be categorized and governed.

##### Data quality and diversity
To ensure data quality we will source words from recognized dictionaries. Cross-verification between different dictionaries for all the words will be performed. 

To ensure data diversity, we will balance the data across different proficiency levels according to JLPT levels.

For an actually useful vocabulary, the following data categories are considered:
- Daily life vocabulary
- Academic/formal terms
- Business Japanese
- Casual expressions
- Compound words
  
We will focus on different parts of speech:
- Nouns
- Verbs
- Adjectives
- Adverbs
- Set expressions

##### Privacy and security concerns

All input data and transactions will be logged. This is to ensure auditability and compliance. All Personally Identifiable Information will be ofuscated and anonymized. 
To access the app, any user (student or teacher) must be registered and log in through our Identity and Access Management solution.

##### Integration with existing data systems


##### Model Selection and Development
Due to lack of resources, we will currently not develop a Large Language Model. Fortunately, LLM development is in an all time high and we can leverage these models without the need to invest in development.

We will select from any model that can be consumed through AWS Bedrock. The main contestants are:
- Claude Sonnet 3
- Mixtral 7x8b instruct
- Amazon Titan Text G1 - Express

For the initial scope text-to-text LLM is enough. However, for different study activities other modalities might be considered.


#### Infrastructure Design
**Design a scalable and flexible infrastructure that can support GenAI workloads:**
Since we will use AWS to host our app, we will have a scalable and flexible AI Model consumption depending on the app's traffic.
Since AWS Bedrock provides us the API directly to consume an LLM, we do not have to worry about specialized hardware. 

Architecture will be modular and depend on different services, such as:
- AWS Bedrock
- AWS API Gateway
- AWS ECS
- AWS Cloudfront 

**Integration and Deployment**

We will follow CI/CD and devops for our app. We will use four different environments, 

dev -> int -> cons -> prod

All modules will be independent from each other and will be able to function directly through API consumption.

**Ensure compatibility with legacy systems**
Since the app will be hosted on the cloud, it will be able to be accessed from any device with internet access.


**Monitoring and Optimization**
Establish robust monitoring and optimization processes:
We will log through Cloudwatch every important interaction between user and model, as well as performance metrics.

